### Git

### Clone the Repository
```
git clone https://github.com/<USERNAME>/<project>.git
cd <project>
```

### Create and Checkout New Branch
```
git checkout -b dev-feature
```

### Stage a specific file for the next commit
```
git add <filename>
```

### Check which files have changed on a remote server 
You need to fetch the latest commits from the remote repository without merging them
```
git fetch origin
```

After fetching, you can compare your local branch with the remote branch to see which files have changed
```
git diff --name-only origin/main
```

If you want to see the actual changes in the files
```
git diff origin/main
```

### Commit staged changes to the local repository
```
git commit -m "<message>"
```

### Pushing the Local Branch to the Remote Repository
```
git push --set-upstream origin dev-feature
```

### Switch to the Main Branch:
```
git checkout main
```

### Update the Main Branch:
```
git pull origin main
```
 
### Merge Your Feature Branch into Main:
```
git merge dev-feature
```

### Push the Merged Changes to the Remote Repository:
```
git push origin main
```

### [Optional] Delete Your Local Feature Branch:
```
git branch -d dev-feature
```

### [Optional] Delete the Remote Feature Branch:
```
git push origin --delete dev-feature
```

### Keep Your Branch Up to Date
```
git checkout main
git fetch origin
git pull origin main
git checkout dev-feature
git rebase main
```

### Resolve Conflicts if Any During Rebase
Manually resolve the conflict in the given file
```
git add <conflicted-file>
git rebase --continue
```

### Push Changes to Your Branch
```
git push origin dev-feature
```
or, if you’ve rebased:
```
git push origin dev-feature --force
```

### Keep Main Branch Up to Date Post-Merge
```
git checkout main
git pull origin main
```

### Starting a New Feature or Bugfix
```
git checkout main
git pull origin main
git checkout -b dev-newfeatureorbugfix
```

### Unstage a single file
```
git reset HEAD <filename>
```

### Unstage all changes
```
git reset
```

### Check Differences Between Local and Remote Branch
To see if your local branch is ahead or behind the remote branch:
```
git fetch
git status
```

### See Detailed Differences in Files
To see differences between your local branch and the remote branch:
```
git fetch
git diff origin/main
```
Replace main with your branch name.

### Check Differences in Commits
To see commits in your local branch that are not on remote:
```
git log origin/main..HEAD --oneline
```

To see commits on remote that are not in your local branch:
```
git log HEAD..origin/main --oneline
```

### Check if Local and Remote Are Different
A quick way to check if local and remote are different:
```
git diff --stat origin/main
```

### List Changed Files Between Local and Remote
```
git fetch
git diff --name-status origin/main
```
This will show:
M (Modified files)  
A (Added files)  
D (Deleted files)  

### Show Only Added and Modified Files
If you only want added or modified files (excluding deletions):
```
git diff --name-only origin/main
```

### Check Staged and Unstaged Changes
Unstaged changes: Files modified but not staged
```
git status -s
```
Or
```
git diff --name-only
```

Staged changes: Files added to the staging area:
```
git diff --cached --name-only
```

### Check Differences in Commits
To see which files have changed in commits not pushed to the remote:
```
git diff --name-status origin/main..HEAD
```
This shows file differences between your last commit and the remote branch.

### Undo Unstaged Changes (Revert modified files)
If you have modified files but haven't staged them yet, restore them to their last committed state:

```
git restore <file>
```

To restore all unstaged changes:
```
git restore .
```

### Undo Staged Changes (Unstage files but keep modifications)
If you've already staged changes with git add, but want to unstage them:
```
git restore --staged <file>
```

To unstage all files:
```
git restore --staged .
```

### Undo Local Changes and Reset to Remote (Discard all local changes)
If you want to completely reset your branch to match the remote:
```
git reset --hard origin/main
```

(Replace main with your branch name.)

⚠ Warning: This will delete all local changes, including uncommitted work.

### Undo the Last Commit (Keep changes unstaged)
If you've committed but haven’t pushed yet and want to undo the commit but keep the changes:
```
git reset --soft HEAD~1
```

### Undo the Last Commit (Discard changes completely)
If you want to remove the last commit and discard the changes completely:
```
git reset --hard HEAD~1
```

### Restore a Deleted File
If you accidentally deleted a file and want to restore it:
```
git checkout -- <file>
```
or
```
git restore <file>
```

### Revert a Pushed Commit
If you've already pushed a commit and need to undo it:
```
git revert <commit-hash>
```
This creates a new commit that undoes the changes, keeping history intact.

### Reset to a Specific Commit
If you need to reset your branch to a specific commit:
```
git reset --hard <commit-hash>
```
⚠ This will erase commits after the specified commit.



















