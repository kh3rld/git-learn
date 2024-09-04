# Changed your mind?
reverting changes
- modify the file hello.sh
```
git status
git restore hello.sh
cat hello.sh
```

staging and cleaning
- introduce unwanted changes
```
git add hello.sh
git status
git restore --staged hello.sh
git restore hello.sh
```

committing and reverting
 - introduce unwanted changes to hello.sh file
 ```
 git add hello.sh
 git commit -m "docs: Add Unwanted comment"
 git log --oneline
 git reset HEAD~1
 git restore hello.sh
 ```

 tagging and removing commits
 ```
 git tag oops
 git show v1
 git reset --hard v1
 ```

 displaying logs with deleted commits

 ```
 git reflog
 git log --oneline --decorate --all | grep oops
 ```

 cleaning unreferenced commits
```
git reflog
git fsck --lost-found
git gc --prune=now
git fsck--lost-found
```

author information
- modify the file then:
```
git add hello.sh
git commit -m "docs(hello): Add Author info to hello.sh"
```

- modify file with email
```
git add hello.sh
git commit --amend --no-edit
```