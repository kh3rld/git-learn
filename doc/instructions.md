## History

### Show the History of the Working Directory
```bash
git log
```

### Show One-Line History
```bash
git log --oneline
```

### Customize Log Output
- **Last 2 Entries:**
  ```bash
  git log -n 2 --oneline
  ```
- **Commits Made Within the Last 5 Minutes:**
  ```bash
  git log --since="5 minutes ago" --oneline
  ```

### Personalized Format
```bash
git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
```

---

## Check it Out

### Restore First Snapshot
```bash
git checkout $(git rev-list --max-parents=0 HEAD)
cat hello.sh
```

### Restore Second Recent Snapshot
```bash
git checkout HEAD~1
cat hello.sh
```

### Return to Latest Version
```bash
git checkout main
cat hello.sh
```

---

## TAG me

### Referencing Current Version
```bash
git tag v1
```

### Tagging Previous Version
```bash
git tag v1-beta HEAD~1
```

### Navigating Tagged Versions
- **Checkout v1:**
  ```bash
  git checkout v1
  ```
- **Checkout v1-beta:**
  ```bash
  git checkout v1-beta
  ```

### Listing Tags
```bash
git tag
```

---

## Changed Your Mind?

### Reverting Changes (Unstaged)
```bash
sed -i '/# This is a bad comment. We want to revert it./d' hello.sh
git checkout -- hello.sh
```

### Staging and Cleaning
```bash
# Add unwanted changes
echo "# This is an unwanted but staged comment" >> hello.sh
git add hello.sh
git reset
```

### Committing and Reverting
```bash
# Add unwanted changes again
echo "# This is an unwanted but committed change" >> hello.sh
git add hello.sh
git commit -m "Add unwanted comment"
# Revert the commit
git revert HEAD
```

### Tagging and Removing Commits
```bash
git tag oops
git reset --hard v1
```

### Displaying Logs with Deleted Commits
```bash
git log --oneline --decorate --graph
```

### Cleaning Unreferenced Commits
```bash
git reflog expire --expire=now --all-ref
git gc --prune=now --aggressive
```

### Author Information
```bash
sed -i '/# Default is World/a # Author: Jim Weirich' hello.sh
git add hello.sh
git commit --amend --no-edit
```

---

## Move it

### Moving hello.sh
```bash
git mv hello.sh lib/
git commit -m "Move hello.sh to lib/ directory"
```

### Create and Commit Makefile
```bash
echo 'TARGET="lib/hello.sh"

run:
	bash ${TARGET}' > Makefile
git add Makefile
git commit -m "Add Makefile"
```

---

## Blobs, Trees, and Commits

### Exploring `.git/` Directory
- **objects/**: Contains all the data of your repository.
- **config**: Configuration file for your repository.
- **refs/**: Contains references to commit objects.
- **HEAD**: Points to the current branch or commit.

### Latest Object Hash
```bash
ls -1 .git/objects | tail -n 1
# Replace <object_hash> with the latest object hash
git cat-file -p <object_hash>
```

### Dumping Directory Tree
```bash
git ls-tree HEAD
# To dump contents of lib/ and hello.sh
git ls-tree HEAD lib/
git cat-file -p $(git ls-tree HEAD lib/ | grep hello.sh | awk '{print $3}')
```

---

## Branching

### Create and Switch to New Branch
```bash
git checkout -b greet
echo '#!/bin/bash

Greeter() {
    who="$1"
    echo "Hello, $who"
}' > lib/greeter.sh
git add lib/greeter.sh
git commit -m "Add greeter.sh"
```

### Update `lib/hello.sh`
```bash
echo '#!/bin/bash

source lib/greeter.sh

name="$1"
if [ -z "$name" ]; then
    name="World"
fi

Greeter "$name"' > lib/hello.sh
git add lib/hello.sh
git commit -m "Update hello.sh to use greeter.sh"
```

### Update Makefile
```bash
echo '# Ensure it runs the updated lib/hello.sh file
TARGET="lib/hello.sh"

run:
	bash ${TARGET}' > Makefile
git add Makefile
git commit -m "Update Makefile"
```

### Switch Back and Compare Branches
```bash
git checkout main
git diff greet -- Makefile lib/hello.sh lib/greeter.sh
```

### Generate README.md
```bash
echo 'This is the Hello World example from the git project.' > README.md
git add README.md
git commit -m "Add README.md"
```

### Draw Commit Tree Diagram
```bash
git log --graph --oneline --all
```

---

## Conflicts, Merging, and Rebasing

### Merge Main into Greet Branch
```bash
git checkout greet
git merge main
```

### Make Changes in Main and Commit
```bash
git checkout main
echo '#!/bin/bash

echo "What\'s your name"
read my_name

echo "Hello, $my_name"' > hello.sh
git add hello.sh
git commit -m "Update hello.sh for name input"
```

### Merge Main into Greet (Conflict)
```bash
git checkout greet
git merge main
# Resolve the conflict manually or using a tool
git add hello.sh
git commit -m "Resolve conflict with main"
```

### Rebase Greet Branch
```bash
git checkout greet
git rebase main
```

### Merge Greet into Main
```bash
git checkout main
git merge greet
```

### Fast-Forwarding and Differences
- **Fast-Forwarding**: When the branch being merged can be applied directly on top of the target branch.
- **Merging vs. Rebasing**: Merging creates a new commit, while rebasing re-applies commits on top of the target branch.

---

## Local and Remote Repositories

### Clone Repository
```bash
git clone hello work/cloned_hello
```

### Show Logs for Cloned Repository
```bash
cd work/cloned_hello
git log
```

### Display Remote Information
```bash
git remote -v
```

### List Remote and Local Branches
```bash
git branch -a
```

### Make Changes and Commit in Original Repository
```bash
echo 'This is the Hello World example from the git project.
(changed in the original)' > README.md
git add README.md
git commit -m "Update README.md in original repository"
```

### Fetch Changes in Cloned Repository
```bash
cd work/cloned_hello
git fetch
git log
```

### Merge Changes from Remote Main Branch
```bash
git checkout main
git merge origin/main
```

### Add Local Branch Tracking Remote Branch
```bash
git checkout -b greet origin/greet
```

### Add Remote and Push Branches
```bash
git remote add shared <url-to-bare-repository>
git push shared main
git push shared greet
```

### Git Command Equivalent for Fetching Changes
```bash
git pull
```

---

## Bare Repositories

### What is a Bare Repository?
A bare repository is a repository without a working directory. It is typically used as a central repository to which other repositories push their changes.

### Create a Bare Repository
```bash
git clone --bare hello hello.git
```

### Add Bare Repository as a Remote
```bash
git remote add shared ../hello.git
```

### Change README.md and Push
```bash
echo 'This is the Hello World example from the git project.
(Changed in the original and pushed to shared)' > README.md
git add README.md
git commit -m "Update README.md"
git push shared main
```

### Pull Changes in Cloned Repository
```bash
cd work/cloned_hello
git pull shared main
```

