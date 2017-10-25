# Prerequisites
A GitHub account with a verified email address is required to allow you to fork repositories and create pull requests.

# Procedure
Following is a procedure to guide you through every step from GitHub login to closing your pull request.

## Create a new fork
1.  Login to GitHub.
2.  Use the **Search** feature at the top of the page to navigate to the upstream respository you've been asked to review/edit.
    **Note**: Try to use the full respository path <orgname/repositoryname>, otherise the search results count may be huge.
3.  Click ![](/images/fork.PNG) to create a copy of the repository. 

    A fork is a copy of the original repository. You can make changes to a fork without without affecting the original repository. Using your fork, you can fetch updates from or submit changes to the original repository with *Pull Requests*.

## Editing your fork

 4.   Edits markdown files as required. See [Editing Markdown][] for more details.
  As you make changes, you should commit then to your master branch at regular intervals using the **Commit Changes** button at the bottom of the edit screen.
  Commits are analagous to Saves - except each commit gets an assigned a unique ID to help you track them.
     ** ADD NOTE ABOUT PREVIEW?**
 5.   When you are happy with your edits, commit the changes to your master branch a final time.
 
 ## Create a Pull Request from your fork
 By creating a pull request, you are asking the upstream repository to accept the changes you have made, and merge them into the original repository. Once a pull request is opened, you can discuss and review the potential changes with collaborators and add follow-up commits before the changes are merged into the repository.
 
 6. Navigate to the original repository you created your fork from.
 7. To the right of the Branch menu, click **New pull request**.
 8. On the Compare page, click **Compare across forks**.
 9. **IMPORTANT**: Confirm that the base fork is the repository you'd like to merge changes into:
 
    Use the **base** branch drop-down menu to select the branch of the upstream repository you'd like to merge changes into.
 
    Use the **head** fork drop-down menu to select your fork, then use the compare branch drop-down menu to select the branch you made your changes in.
 
 11. Deselect **Allow edits from maintainers** if you don't want any other contributers changing your pull request.
 10. Click **Create pull request**.
 
 At this point, your pull request is sent to the owner of the upstream repository. They will decide whether to merge (accept) or close (reject)  your pull request. Alternatively they may decide to open a conversation to discuss your edit request. You will be notified accordingly.
 
 
 
 
 
  




[Editing Markdown]:markdown.md

