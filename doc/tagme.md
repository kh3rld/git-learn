# Tag Me

restore first snapshot
```
git tag v1
```

tagging previous version
```
git log --oneline --skip=1 -n 1
git tag v1-beta HEAD~1
```

Navigating tagged versions
```
git checkout v1
git tag
git checkout master
git checkout v1-beta
git checkout master
```

list all tags
```
git tag -n
```
