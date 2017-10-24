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
This code sample calls the API's `playlists.list` method. Use command-line flags to define the parameters you want to use in the request as shown in the following examples:

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
