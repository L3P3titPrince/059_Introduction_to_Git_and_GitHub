## Table of Contents
- [Initialize Git](#initialize-git)
- [Initialize GitHub](#initialize-github)


copy the orignial one with a new underscore copy for comparsine
`cp 020_disk_usage.py 020_disk_usage_original.py'
and another one with underscore fixed to modify 
`cp 020_disk_usage.py 020_disk_usage_fixed.py`
we modify the "fixed" version, then find the difference between then

![diff](/100_images/01.png)

`diff -u 020_disk_usage_original.py 020_disk_usage_fixed.py`

write the difference into *.diff file
` diff -u 020_disk_usage_original.py 020_disk_usage_fixed.py > 021_disk_usage.diff`


### Initialize Git

show the global configrations
`git config --global --list`
We can also set differnet username and email for different repository

Initialize a fresh new repository with `git init`
![diff](/100_images/02.png)

A database for your Git project
`ls -l .git/`
![diff](/100_images/03.png)


To make file on track `git add <filename>` and then we added this file from working tree/work brenche to staging area. A staging area(index) is a file maintained by Git that contains all of the information about files and changes are going to go into your next commit.

Use `git status` to check current working tree and pending changes.
![diff](/100_images/04.png)

Directly use `git commit`

Three stage: Git directory, working tree and staging area.
Threr stage, modifed, modifed, commiteed
Before we modified
![diff](/100_images/05.png)
After we modifed file a little bit we will see the file stauts has changed to **modified**
![diff](/100_images/06.png)

when we add again, we told Git that we want to add the current chagnes in that file to the list of changes to be commited.
![diff](/100_images/07.png)

Also, we can use `git commit -m message` to directy add sentences
![diff](/100_images/08.png)


`git add` = modifed file > staging file (from working tree to staging area)
`git commit` = staging file > commited file (from staging area to Git directory)

```
git init
# 
git add script.py
#
git commit -m 'message sentences'
# after add new code to commited file, we need add the file back to staging again
git status
git add script.py
# add commit message
git commit -m 'add new function'
```

`git commit -a 'message sentence'` only works only old file. If the file is untracked yet, we can't use this command to commit 


`git log` can present pasted commit history.

Git uses the HEAD alias to represent the current checked-out snapshot of your project

`git show <commit id>`
`git show 8babf58b27ecf2ac6a9e6d7b0dfe61033521ed07`
will present commit history.
'git log -p`
`git log --stat`

if I want to know which files are committed and ready to push, I need to following commandss
```
# find out the commit id
git show HEAD --name-only
# the details can be see by commit_id
git show 1c4ebc2
```
![diff](/100_images/09.png)



#### delete and rename
`git mv disk_usage.py check_free.space.py`

`git rm 023_test.py`
this will physically remove this file.
if you only want to cancel the add action, you can use `git reset <filename>`


`git add` untracked -> staging, file is in the staging area from working tree
`git reset <fileanme>` staging -> untracked, remove file from staging area
'git commit -m` staging -> directory, 
`get reset HEAD` directory -> untracked

[git commit rules](https://gist.github.com/turbo/efb8d57c145e00dc38907f9526b60f17)

`git checkout <filename>` undo the modification for this file, it reverts changes to modifed files before they are staged.

You can use `git checkout <filename>` to undo the modifed you did in the IDE. and it will also change the modified in the staging area.

change the commit message by `git commit --amend` override the previous commit message **DON'T USE IN GITHUB**


### Rollback
```
# change a file but result is broken
nano 025_disk_usage.py
# add to stageting
git add 025_disk_usage.py
# commit a broken file
git commit -m 'test'
# rollback and modify the rollback commimt message
git revert
# check the past two commit
git log -p -2 
git log -p -2 --name-only
```

### Branch
git branch 
`git branch 02_feature`
`git



### Initialize GitHub



https://gist.github.com/bsara/5c4d90db3016814a3d2fe38d314f9c23
