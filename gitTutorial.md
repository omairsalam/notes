## Git stuff

- Git is a distributed version control and source code management system.
- It does this through a series of snapshots of your project, and it works with those snapshots to provide you with functionality to version and manage your source code.
- A git repository is comprised of the .git directory & working tree.
    - The .git directory contains all the configurations, logs, branches, HEAD, and more.
    - Working tree is basically the directories and files in your repository. It is often referred to as your working directory.
- Index
    - The Index is the staging area in git.
    - It’s basically a layer that separates your working tree from the Git repository. This gives developers more power over what gets sent to the Git repository.
- Commit
    - A git commit is a snapshot of a set of changes, or manipulations to your Working Tree.
    - For example, if you added 5 files, and removed 2 others, these changes will be contained in a commit (or snapshot). This commit can then be pushed to other repositories, or not!
- Branch
    - A branch is essentially a pointer that points to the last commit you made. As you commit, this pointer will automatically update and point to the latest commit.
- HEAD and head
    - HEAD is a pointer that points to the current branch. A repository only has 1 active HEAD.
    - head is a pointer that points to any commit. A repository can have any number of heads.
- Stages of Git
    - Modified
    - Staged
    - Committed


###Commands

init
- Create an empty Git repository. The Git repository’s settings, stored information, and more is stored in a directory (a folder) named “.git”.
```sh
$ git init
```
config
- To configure settings. Whether it be for the repository, the system itself, or global configurations.
```sh
# Print & Set Some Basic Config Variables (Global)
$ git config --global user.email
$ git config --global user.name

$ git config --global user.email "MyEmail@Zoho.com"
$ git config --global user.name "My Name"
```
status
- To show differences between the index file (basically your working copy/repo) and the current HEAD commit.
```sh
# Will display the branch, untracked files, changes and other differences
$ git status

# To learn other "tid bits" about git status
$ git help status
```
add
- To add files to the staging area/index. If you do not git add new files to the staging area/index, they will not be included in commits!
```sh
# add a file in your current working directory
$ git add HelloWorld.java

# add a file in a nested dir
$ git add /path/to/file/HelloWorld.c

# Regular Expression support!
$ git add ./*.java
```
branch
- Manage your branches. You can view, edit, create, delete branches using this command.
```sh
# list existing branches & remotes
$ git branch -a

# create a new branch
$ git branch myNewBranch

# delete a branch
$ git branch -d myBranch

# rename a branch
# git branch -m <oldname> <newname>
$ git branch -m myBranchName myNewBranchName

# edit a branch's description
$ git branch myBranchName --edit-description
```
checkout
- Updates all files in the working tree to match the version in the index, or specified tree.
```sh
# Checkout a repo - defaults to master branch
$ git checkout
# Checkout a specified branch
$ git checkout branchName
# Create a new branch & switch to it, like: "git branch <name>; git checkout <name>"
$ git checkout -b newBranch
# git checkout checks out (i.e., restores) an old version of a file.
$ git checkout HEAD mars.txt
# or using a unique commit ID
$ git checkout f22b25e mars.txt
```
clone
- Clones, or copies, an existing repository into a new directory. It also adds remote-tracking branches for each branch in the cloned repo, which allows you to push to a remote branch.
```sh
# Clone learnxinyminutes-docs
$ git clone https://github.com/adambard/learnxinyminutes-docs.git
```
commit
- Stores the current contents of the index in a new “commit.” This commit contains the changes made and a message created by the user.
```sh
# commit with a message
$ git commit -m "Added multiplyNumbers() function to HelloWorld.c"

# automatically stage modified or deleted files, except new files, and then commit
$ git commit -a -m "Modified foo.php and removed bar.php"
```
diff
- Shows differences between a file in the working directory, index and commits.
```sh
# Show difference between your working dir and the index
$ git diff

# Show differences between the index and the most recent commit.
$ git diff --cached

# Show differences between your working dir and the most recent commit
$ git diff HEAD

# Show the difference between the last committed change and what’s in the staging area
$ git diff --staged

# To see what we changed at different steps, we can use git diff with the notation HEAD~1, HEAD~2, and so on, to refer to old commits
# The most recent end of the chain is referred to as HEAD; we can refer to previous commits using the ~ notation, so HEAD~1 (pronounced “head minus one”) means “the previous commit”,
#   while HEAD~123 goes back 123 commits from where we are now
$ git diff HEAD~1 mars.txt
$ git diff HEAD~2 mars.txt

# Doing diff using unique IDs
$ git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b mars.txt
$ git diff f22b25e mars.txt
```
grep
- Allows you to quickly search a repository.
```sh
# Thanks to Travis Jeffery for these
# Set line numbers to be shown in grep search results
$ git config --global grep.lineNumber true

# Make search results more readable, including grouping
$ git config --global alias.g "grep --break --heading --line-number"
# Search for "variableName" in all java files
$ git grep 'variableName' -- '*.java'

# Search for a line that contains "arrayListName" and, "add" or "remove"
$ git grep -e 'arrayListName' --and \( -e add -e remove \) 
```
log
- Display commits to the repository.
```sh
# Show all commits
$ git log

# Show X number of commits
$ git log -n 10

# Show merge commits only
$ git log --merges
```
merge
- “Merge” in changes from external commits into the current branch.
```sh
# Merge the specified branch into the current.
$ git merge branchName

# Always generate a merge commit when merging
$ git merge --no-ff branchName
```
mv
- Rename or move a file
```sh
# Renaming a file
$ git mv HelloWorld.c HelloNewWorld.c

# Moving a file
$ git mv HelloWorld.c ./new/path/HelloWorld.c

# Force rename or move
# "existingFile" already exists in the directory, will be overwritten
$ git mv -f myFile existingFile
```
pull
- Pulls from a repository and merges it with another branch.
```sh
# Update your local repo, by merging in new changes
# from the remote "origin" and "master" branch.
# git pull <remote> <branch>
# git pull => implicitly defaults to => git pull origin master
$ git pull origin master

# Merge in changes from remote branch and rebase
# branch commits onto your local repo, like: "git pull <remote> <branch>, git rebase <branch>"
$ git pull origin master --rebase
```
push
- Push and merge changes from a branch to a remote & branch.
```sh
# Push and merge changes from a local repo to a 
# remote named "origin" and "master" branch.
# git push <remote> <branch>
# git push => implicitly defaults to => git push origin master
$ git push origin master

# To link up current local branch with a remote branch, add -u flag:
$ git push -u origin master
# Now, anytime you want to push from that same local branch, use shortcut:
$ git push 
```
stash
- Stashing takes the dirty state of your working directory and saves it on a stack of unfinished changes that you can reapply at any time.
- Let’s say you’ve been doing some work in your git repo, but you want to pull from the remote. Since you have dirty (uncommited) changes to some files, you are not able to run git pull. Instead, you can run git stash to save your changes onto a stack!
```sh
$ git stash
Saved working directory and index state \
  "WIP on master: 049d078 added the index file"
  HEAD is now at 049d078 added the index file
  (To restore them type "git stash apply") 
#Now you can pull!
$ git pull
  ...changes apply...
  Now check that everything is OK
$ git status
  On branch master
  nothing to commit, working directory clean
  You can see what “hunks” you’ve stashed so far using git stash list. Since the “hunks” are stored in a Last-In-First-Out stack, our most recent change will be at top.
$ git stash list
  stash@{0}: WIP on master: 049d078 added the index file
  stash@{1}: WIP on master: c264051 Revert "added file_size"
  stash@{2}: WIP on master: 21d80a5 added number to log
  Now let’s apply our dirty changes back by popping them off the stack.
$ git stash pop
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#
#      modified:   index.html
#      modified:   lib/simplegit.rb
#
# git stash apply does the same thing
```
rebase
- Take all changes that were committed on one branch, and replay them onto another branch. Do not rebase commits that you have pushed to a public repo.
```sh
# Rebase experimentBranch onto master
# git rebase <basebranch> <topicbranch>
$ git rebase master experimentBranch
```
reset
- Reset the current HEAD to the specified state. This allows you to undo merges, pulls, commits, adds, and more. It’s a great command but also dangerous if you don’t know what you are doing.
```sh
# Reset the staging area, to match the latest commit (leaves dir unchanged)
$ git reset

# Reset the staging area, to match the latest commit, and overwrite working dir
$ git reset --hard

# Moves the current branch tip to the specified commit (leaves dir unchanged)
# all changes still exist in the directory.
$ git reset 31f2bb1

# Moves the current branch tip backward to the specified commit
# and makes the working dir match (deletes uncommited changes and all commits
# after the specified commit).
$ git reset --hard 31f2bb1
```
rm
- The opposite of git add, git rm removes files from the current working tree.
```sh
# remove HelloWorld.c
$ git rm HelloWorld.c

# Remove a file from a nested dir
$ git rm /pather/to/the/file/HelloWorld.c
```

###Extra notes
- Use "bare double dash" (--) to separate options from a list of arguments. For example, here if we have both a file and a tag named main.c, then we will get different results
```sh
$ git checkout main.c
$ git checkout -- main.c
```
- To configure Git to open your favorite editor during `git commit`, set this environment variable
```sh
$ export GIT_EDITOR=vim
```






### Sources
- http://learnxinyminutes.com/docs/git/