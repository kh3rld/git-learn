# Local and remote repositories

```
cd ..
git clone hello/ cloned_hello
cd cloned_hello
git log
git remote -v
git remote show
git branch
git branch -a
cd  hello
 edit README.md
git add README.md
git commit -m "Docs(README): Update README"
cd cloned_hello
git fetch origin
git log --oneline --graph --decorate --all
git checkout master
git merge origin
git fetch origin
git checkout -b greet origin/greet
git branch -vv
git remote add master https://learn.zone01kisumu.ke/git/khahussein/git
git remote -v
git push master master
git push master greet


```

## bare repositories

cd work
git clone --bare hello hello.git
cd hello.git
ls
cd hello
git remote add shared ../hello.sh 

 edit README.md file
git add README.md
git commit -m "Docs(REAME): Update README"
git push shared master

cd cloned_hello
git remote -v
git pull main master
git log --oneline -n 5