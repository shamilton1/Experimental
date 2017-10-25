# Prerequisites
You require a GitHub account with an associated and verified email address before you can fork/edit repositories or create pull requests.

Visit the GitHub [homepage][] to register.

# Procedure
After registration, use the following procedure to guide you through each step from initial GitHub login, to closing your pull request. There are three main stages:
#### 1. Creating a fork repository
  Creates an independent copy of a respository which you can manage without risk of affecting the original.
#### 2. Editing fork
  Making required technical edits/style changes to the markdown content, or structurally changing the repository.
#### 3. Creating and submitting a pull request 
  Making a request to the original repository owner for the changes you made to be incorporated into the original repository.

## Creating a fork repository
1.  Login to GitHub.
2.  Use the **Search** feature at the top of the page to navigate to the upstream respository you've been asked to review/edit.
    **Note**: Search results count can be huge. Try to use the full respository name <orgname/repositoryname>.
3.  Click ![](/images/fork.PNG) to create a copy of the repository. 

    A fork is a copy of the original repository. You can make changes to a fork without without affecting the original repository. Using your fork, you can fetch updates from or submit changes to the original repository with *Pull Requests*.

## Editing the fork
After the forking process completes (this may take some time), the newly forked repository will display in the **Code** tab. 

 4. Open a markdown file by clicking on the filename. The file will open in read only mode. Use the ![](/images/edit.PNG) icon to switch to editing mode.
 
 5. Edit markdown files as required (for full instructions on formatting and editing command, see [Editing Markdown][]).
 
If you know the changes to be made, you can navigate directly to the appropriate MD files and make the edits (see [Editing Markdown][]). If you want to review the full repository from scratch, open the README.md file first. This typically provides an overview of the purpose of the repository and may also include a ToC, providing a good starting point to get a feel for the file structure. See [Editing Markdown][] for more details.

  As you make changes, you should commit then to your master branch at regular intervals using the ![](/images/commit.PNG) button at the bottom of the edit screen.
  Commits are analagous to Saves - except each commit gets an assigned a unique ID to help you track them.
  As you edit files you can preview your changes withour making commits by clicking the Preview changes tab at the top of your editing window.
  
 5.   When you are happy with your edits, make a final commit to your master branch.
 
 ## Creating and submitting a pull request
 By creating a pull request, you are asking the upstream repository to accept the changes you have made, and merge them into the original repository. Once a pull request is opened, you can discuss and review the potential changes with collaborators and add follow-up commits before the changes are merged into the repository.
 
 6. Navigate to the original repository you created your fork from.
 7. To the right of the Branch menu, click ![](/images/pull_request.PNG).
 8. On the Compare page, click **Compare across forks**.
 9. Use the **base** branch drop-down menu to select the branch of the upstream repository you'd like to merge changes into.
 
10. Use the **head** fork drop-down menu to select your fork, then use the compare branch drop-down menu to select the branch you made your changes in.
 
 11. Deselect **Allow edits from maintainers** if you don't want any other contributers changing your pull request.
 12. Click **Create pull request**.
 
 At this point, your pull request is sent to the owner of the upstream repository. They will decide whether to merge (accept) or close (reject) your pull request. Alternatively they may decide to open a conversation to discuss your pull request. You will be notified accordingly.
 
 
 
 
  




[Editing Markdown]:markdown.md

[homepage]:https://github.com/
