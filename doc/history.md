# History
## Show history of working directory
history of commits
```
git log
```
more compact view
```
git log --oneline
```
controlled entries
```
git log --since="5 minutes ago" -n 2 --oneline
```
personalized format
```
git log --pretty=format:"%h %ad | %s (%d) [%an]" -- date=short
