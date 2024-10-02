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


