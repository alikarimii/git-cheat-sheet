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


