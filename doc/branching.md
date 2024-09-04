# Branching

create and switch to new branch
```
git checkout -b greet
```
create a new file in the lib directory
``` 
cd lib/
vim greeter.sh
git add greeter.sh
git commit -m "feat(greeter): implement greeter.sh"
```

update hello.sh file
```
git add hello.sh
git commit -m "refactor(hello): add and update source"
```

update the Makefile
```
git add Makefile
git commit -m "docs(makefile): Add comment"
```
switch back to master branch
```
git checkout master
```
compare differences
```
git diff master..greet -- Makefile
git diff master..greet -- lib/hello.sh
git diff master..greet -- lib/greeter.sh
```
create README.md file
```
vim README.md 
git add README.md
git commit -m "docs(README): Implement README.md"
```

draw a commit tree diagram 
```
git log --graph --oneline --all
```

