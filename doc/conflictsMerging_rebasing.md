Conflicts, merging and rebasing
- merge master into greet branch
```
git checkout greet
git merge master
 git log --graph --oneline --all
```
switch to master branch
```
git checkout master
 update hello.sh file
 git add hello.sh
 git commit -m "refactor(hello): Add name variable"
```
-merging main into greet branch
```
git checkout greet
git merge master
 resolve conflict manually
git add hello.sh
git commit -m "fix(hello): Resolve merge conflict"
```
- rebasing greet branch

```
git log --graph --oneline --all
git reset --hard f968bec
git rebase master
git log --graph --oneline --all
```
- merging greet into master
```
git checkout master
git merge greet
```


