## Git Cheatsheet

### Config

```
# Set name and email so that commits can associate with it
git config --global user.name "NAME"
git config --global user.email "<email id>
```

### init, add, commit
```
# Initialize a directory as a git repo
git init

# Create a local copy of remote repo
git clone <repo>

# Add all files in current dir
git add .
git add file1 file2

# Save the current index and commit it to project history
git commit -m "<message>"

# Modify most recent commit, logg message and files
git commit --amend

# Add and commit in one command
git commit -am "<message>"
```

### branch, checkout, delete
```
# Create new branch
git branch <branch name>

# Checkout branch
git checkout <branch name>
git branch --list

# Delete local branch
git branch -d <branch name>

# Delete remote branch
git push origin -d <branch name>


# Create and

```

