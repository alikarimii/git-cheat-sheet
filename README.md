## Git Cheat Sheet
How to undo mistakes with Git

### 1. Discarding All Local Change in a File
- git status
  - show unstage file
- git diff index.html
  - show what is changed after local change
- git restore index.html
  - Discarding local change

**Warning: All local changes will be gone**

### 2. Restoring a Deleted File
- git status
  - show deleted/modified file
- git restore index.html

### 3. Discard chunks / lines in a File
- git diff index.html
  - show changes
- git restore -p index.html
  - choose which chunks would be Discard [y,n]

### 4. Discarding all local changes
- git status
  - see all deleted / modified file
- git restore .
  - Discard all local change

**Warning: All local changes will be gone**

### 5. Fixing the last commit
- git commit --amend -m "new commit message here"
  - this is for rewrite commit message
  - for add new file to this commit, can add (git add file) file to staging area and do command again

**amend rewrite git history, so Never change history for commit that have already been pushed to remote repository**

### 6. Reverting a commit in the middle
- git revert #hash_number 
  - undo the effect of old commit

### 7. Resetting to an old revision
- git reset --hard #hash_number
  - reset commit and discard all local changes that those commit have
- git reset --mixed #hash_number
  - reset commit but keep local changes

### 8. Resetting a file to an old revision
- git log --follow -p -- index.html
  - show file history.use follow to show history of file before it was renamed
- git restore --source #hash_number index.html
  - reset file to old version base on hash_number

### 9. Recovering deleted commits
you think you want to reset, you reset, but notice it was a bad idea
- git reflog
  - show all history of git, get hash_number of step before bad idea,stable state
- git branch newBranchName #hash_number
  - now all commit that have been deleted, restore in newBranchName

### 10. Recovering deleted branches
- git branch -d branchName
  - delete branch and notice it's bad idea
- git reflog
  - show all history, get hash_number of stable state before bad idea
- git branch branchName #hash_number
  - all commit back to branchName

### 11. Moving a commit to a new branch
you commiited to master,but notice this last commit must go to new branch
- git branch newBranchName
  - set current state of master to newBranchName
- git checkout master && git reset --hard HEAD~1
  - go to master branch and hard reset last commit to clean history and discard last commit

### 12. Moving a commit to a different branch
we have a commit that not belong to master and must go to feature branch
- git checkout feature
  - go to considered branch
- git cherry-pick #hash_number
  - get commit from pre-branch and add to this branch
- git checkout master && git reset --hard HEAD~1
  - go to master and clean it

### 13. Editing old commit messages with Interactive Rebase
if we want change some later commit,not last one, we can't use --amend.
- git rebase -i HEAD~3
  - select 3 last commit in reverse order,older commit at the top, newer commit at bottom
  - in opened editor page, you can choose what do you want,"reword" for edit commit message
  - don't change commit message in place
  - after choose "reword" for considered commit, close editor page
  - another editor page opened and you can edit commit message

### 14. Deleting commits with Interactive Rebase
- git rebase -i HEAD~2
  - select 2 last commit in revese order again
  - just like 13th tip, but instead "reword", use "drop"

### 15. Squashing multiple commits into one with Interactive Rebase
combine some commits
- git rebase -i HEAD~3
  - select last 3 commit
  - use "squash" keyword for combine.
  - each line that you rewrite with keyword "squash", combine with commit **above** it

### 16. Adding changes to an old commit with Interactive Rebase
- git add file
  - add changes to stagging area
- git commit --fixup #hash_number
  - hash number of considered commit
- git rebase -i --autosquash HEAD~4
  - use interactive rebase 
  - git rearange and mark some line with "fixup" keyword,just save and close editor page

### 17. Splitting/editing an old commit with Interactive Rebase
- git log --oneline
  - show commit hash in one line,copy considered commit hash
- git rebase -i #hash_number
  - editor page open and list commit in reverse order(older in top,newer in bottom)
  - rewrite "pick" keyword with "edit" for considered commit, save and close
  - rebase procedure has began
- git reset HEAD~1
  - reset the current state
  - Now all the changes done in that commit are unstaged and need to be committed again
  - This is the step where you create new smaller commits
- git add file && git commit
  - Commit the pieces individually in the usual way
- git rebase --continue
  - When you are done with your surgery, invoke this
  - You can start over again instead with `git rebase --abort` in case something goes wrong.

**Be careful when doing that on branches other people are working on**

## Reference
1. [How to Undo Mistakes With Git Using the Command Line](https://youtu.be/lX9hsdsAeTk)
