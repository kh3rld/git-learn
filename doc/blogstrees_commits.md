# Blobs, trees and commits
Exploring .git/ directory
```
cd .git/
ls
```
latest object hash
```
cd ..
find .git/objects -type f
git rev-parse HEAD
git cat-file -p 81a32264124886fb9a718a21cb28793061a6c53d
```
dumping directory
```
git log --oneline
git cat-file -p 8ecb0081fa6fb79a6c56b516ad0d599bd2ab4de7 
git ls-tree 659a7d30221aa3501fb9740e8f965e5ca46b15d5
git show 659a7d30221aa3501fb9740e8f965e5ca46b15d5:hello.sh
```
