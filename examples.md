# Authorization Credentials
To run any sample that does not require user authorization, such as search_by_keyword.go, you need to replace the value of the `developerKey constant` with a valid API key:
```const developerKey = "YOUR DEVELOPER KEY"```

# Running Samples
```
   go run search_by_keyword.go errors.go
   go run my_uploads.go errors.go oauth2.go
   go run upload_video.go errors.go oauth2.go --filename="sample_video.flv" --title="Test video" --keywords="golang test"
   ```

# Samples in this repository
## Authorize a request
This code sample performs OAuth 2.0 authorization by checking for the presence of a local file that contains authorization credentials. If the file is not present, the script opens a browser and waits for a response, then saves the returned credentials locally.

## Lists
This code sample calls the API's `playlists.list` method. Use command-line flags to define the parameters 
want to use in the request as shown in the following examples:

```
# Retrieve lists for a specified channel
go run lists.go oauth.go errors.go --channelId=UC_x5XG1OV2P6uZZ5FSM9Ttw

# Retrieve authenticated user lists
go run lists.go oauth.go errors.go --mine=true
```

## Retrieving Uploads
This code sample calls the API's `listItems.list` method to retrieve a list of videos uploaded to the channel associated with the request. The code also calls the `channels.list` method with the mine parameter set to true to retrieve the playlist ID that identifies the channel's uploaded videos.

## Search by Keyword
This code sample calls the API's `search.list` method to retrieve search results associated with a particular keyword.

```
package main

import (
  "log"
)

func handleError(err error, message string) {
  if message == "" {
    message = "Error making API call"
  }
  if err != nil {
    log.Fatalf(message + ": %v", err.Error())
  }
}
```

Or try this...
```
package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"log"
	"net"
	"net/http"
	"net/url"
	"os"
	"os/exec"
	"os/user"
	"path/filepath"
	"runtime"

	"golang.org/x/net/context"
	"golang.org/x/oauth2"
	"golang.org/x/oauth2/google"
)

const launchWebServer = false

const missingClientSecretsMessage = `
Please configure OAuth 2.0
To make this sample run, you need to populate the client_secrets.json file
found at:
   %v
with information from the {{ Google Cloud Console }}
{{ https://cloud.google.com/console }}
For more information about the client_secrets.json file format, please visit:
https://developers.google.com/api-client-library/python/guide/aaa_client_secrets
`

// getClient uses a Context and Config to retrieve a Token
// then generate a Client. It returns the generated Client.
func getClient(scope string) *http.Client {
	ctx := context.Background()
	
	b, err := ioutil.ReadFile("client_secret.json")
	if err != nil {
		log.Fatalf("Unable to read client secret file: %v", err)
	}
	
	config, err := google.ConfigFromJSON(b, scope)
	if err != nil {
		log.Fatalf("Unable to parse client secret file to config: %v", err)
	}
	
	config.RedirectURL = "http://localhost:8090"
	// Use the following redirect URI if launchWebServer=false in oauth2.go
	// config.RedirectURL = "urn:ietf:wg:oauth:2.0:oob"
	
	cacheFile, err := tokenCacheFile()
	if err != nil {
		log.Fatalf("Unable to get path to cached credential file. %v", err)
	}
	tok, err := tokenFromFile(cacheFile)
	if err != nil {
		authURL := config.AuthCodeURL("state-token", oauth2.AccessTypeOffline)
		if launchWebServer {
			fmt.Println("Trying to get token from web")
			tok, err = getTokenFromWeb(config, authURL)
		} else {
			fmt.Println("Trying to get token from prompt")
			tok, err = getTokenFromPrompt(config, authURL)
		}
		if err == nil {
			saveToken(cacheFile, tok)
		}
	}
	return config.Client(ctx, tok)
}

// startWebServer starts a web server that listens on http://localhost:8080.
// The webserver waits for an oauth code in the three-legged auth flow.
func startWebServer() (codeCh chan string, err error) {
	listener, err := net.Listen("tcp", "localhost:8090")
	if err != nil {
		return nil, err
	}
	codeCh = make(chan string)

	go http.Serve(listener, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		code := r.FormValue("code")
		codeCh <- code // send code to OAuth flow
		listener.Close()
		w.Header().Set("Content-Type", "text/plain")
		fmt.Fprintf(w, "Received code: %v\r\nYou can now safely close this browser window.", code)
	}))

	return codeCh, nil
}

// openURL opens a browser window to the specified location.
// This code originally appeared at:
//   http://stackoverflow.com/questions/10377243/how-can-i-launch-a-process-that-is-not-a-file-in-go
func openURL(url string) error {
	var err error
	switch runtime.GOOS {
	case "linux":
		err = exec.Command("xdg-open", url).Start()
	case "windows":
		err = exec.Command("rundll32", "url.dll,FileProtocolHandler", "http://localhost:4001/").Start()
	case "darwin":
		err = exec.Command("open", url).Start()
	default:
		err = fmt.Errorf("Cannot open URL %s on this platform", url)
	}
	return err
}

// Exchange the authorization code for an access token
func exchangeToken(config *oauth2.Config, code string) (*oauth2.Token, error) {
	tok, err := config.Exchange(oauth2.NoContext, code)
	if err != nil {
		log.Fatalf("Unable to retrieve token %v", err)
	}
	return tok, nil
}

func getTokenFromPrompt(config *oauth2.Config, authURL string) (*oauth2.Token, error) {
	var code string
	fmt.Printf("Go to the following link in your browser. After completing " +
		"the authorization flow, enter the authorization code on the command " +
		"line: \n%v\n", authURL)

	if _, err := fmt.Scan(&code); err != nil {
		log.Fatalf("Unable to read authorization code %v", err)
	}
	fmt.Println(authURL)
	return exchangeToken(config, code)
}

func getTokenFromWeb(config *oauth2.Config, authURL string) (*oauth2.Token, error) {
	codeCh, err := startWebServer()
	if err != nil {
		fmt.Printf("Unable to start a web server.")
		return nil, err
	}

	err = openURL(authURL)
	if err != nil {
		log.Fatalf("Unable to open authorization URL in web server: %v", err)
	} else {
		fmt.Println("Your browser has been opened to an authorization URL.",
			" This program will resume once authorization has been provided.\n")
		fmt.Println(authURL)
	}

	// Wait for the web server to get the code.
	code := <-codeCh
	return exchangeToken(config, code)
}

// tokenCacheFile generates credential file path/filename.
// It returns the generated credential path/filename.
func tokenCacheFile() (string, error) {
	usr, err := user.Current()
	if err != nil {
		return "", err
	}
	tokenCacheDir := filepath.Join(usr.HomeDir, ".credentials")
	os.MkdirAll(tokenCacheDir, 0700)
	return filepath.Join(tokenCacheDir,
		url.QueryEscape("tube-go.json")), err
}

// tokenFromFile retrieves a Token from a given file path.
// It returns the retrieved Token and any read error encountered.
func tokenFromFile(file string) (*oauth2.Token, error) {
	f, err := os.Open(file)
	if err != nil {
		return nil, err
	}
	t := &oauth2.Token{}
	err = json.NewDecoder(f).Decode(t)
	defer f.Close()
	return t, err
}
```
# Quickstart Go
```
func channelsListByUsername(service *tube.Service, part string, forUsername string) {
  call := service.Channels.List(part)
  call = call.ForUsername(forUsername)
  response, err := call.Do()
  handleError(err, "")
  fmt.Println(fmt.Sprintf("This channel's ID is %s. Its title is '%s', " +
              "and it has %d views.",
              response.Items[0].Id,
              response.Items[0].Snippet.Title,
              response.Items[0].Statistics.ViewCount))
}


func main() {
  ctx := context.Background()

  b, err := ioutil.ReadFile("client_secret.json")
  if err != nil {
    log.Fatalf("Unable to read client secret file: %v", err)
  }

  // If modifying these scopes, delete your previously saved credentials
  // at ~/.credentials/tube-go-quickstart.json
  config, err := google.ConfigFromJSON(b, tube.tubeReadonlyScope)
  if err != nil {
    log.Fatalf("Unable to parse client secret file to config: %v", err)
  }
  client := getClient(ctx, config)
  service, err := tube.New(client)

  handleError(err, "Error creating Tube client")

  channelsListByUsername(service, "snippet,contentDetails,statistics", "GoogleDevelopers")
}
```

