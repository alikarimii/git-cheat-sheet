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


