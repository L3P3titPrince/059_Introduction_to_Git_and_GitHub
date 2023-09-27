## Table of Contents
- [Initialize Git](#initialize-git)
    - [Skip Staging](#skip-staging)
    - [delete and rename](#5delete-and-rename)
- [Initialize GitHub](#initialize-github)
- [End](#end)


copy the orignial one with a new underscore copy for comparsine
`cp 020_disk_usage.py 020_disk_usage_original.py'
and another one with underscore fixed to modify 
`cp 020_disk_usage.py 020_disk_usage_fixed.py`
we modify the "fixed" version, then find the difference between then

![diff](/100_images/01.png)

`diff -u 020_disk_usage_original.py 020_disk_usage_fixed.py`

write the difference into *.diff file
`diff -u 020_disk_usage_original.py 020_disk_usage_fixed.py > 021_disk_usage.diff`


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
From the screenshot, you can see most of files are not tracked by git
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


`git log` can present pasted commit history.
<br></br>

### Skip Staging
`git commit -a -m 'message sentence'` only works only old file. If the file is untracked yet, we can't use this command to commit. If the file has never been commited to the repo, we'll stil need to use git add to track it first.
For example, **README.md** has already been add to repo and we need to modify it a little bit from time to time. After make some small change or modifacation, you can use `git commit -a -m 'dddddddd'` to quick commit this single file.


### 4.diff
`git log -p` = `diff-u`
Press `q` to quit long list.
Git uses the HEAD alias to represent the current checked-out snapshot of your project

`git show <commit id>`
`git show 8babf58b27ecf2ac6a9e6d7b0dfe61033521ed07`
will present commit history.
`git log -p`
`git log --stat`

if I want to know which files are committed and ready to push, I need to following commandss
```
# find out the commit id
git show HEAD --name-only
# the details can be see by commit_id
git show 1c4ebc2
```
![diff](/100_images/09.png)
<br></br>


### 5.delete and rename
`git mv disk_usage.py check_free.space.py`
try to delete this file from repository
`git rm 023_test.py`
this will physically remove this file.
if you only want to cancel the add action, you can use `git reset <filename>`


`git add` untracked -> staging, file is in the staging area from working tree
`git reset <fileanme>` staging -> untracked, remove file from staging area
'git commit -m` staging -> directory, 
`get reset HEAD` directory -> untracked

[git commit rules](https://gist.github.com/turbo/efb8d57c145e00dc38907f9526b60f17)


### 6.Undoing change before commmiting
After you modify a little bit about code but code lead to a running fail. 

`git checkout <filename>` undo the modification for this file, it reverts changes to modifed files before they are staged.

You can use `git checkout <filename>` to undo the modifed you did in the IDE. and it will also change the modified in the staging area.

Previous example is undoing before staging. What if you alreday add the file to staging area and then don't want to commit. We can unstage changes by using `git reset`
I added **024_test.py** into staging area
![didd](/100_images/022.png)
But I don't want to commit it. I use `git reset HEAD 024_test.py`. Then you can see the file removed from staging area
![023](/100_images/023.png)


### 7.Amending Commits
Previous we try to undo/remove about staging area. But what if you already commit and want to undo/remove? 

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
git revert HEAD
# check the past two commit
git log -p -2 
git log -p -2 --name-only
```
For example, we add new line in all_check.py but that will cause a fail.
![024](/100_images/024.png)
commit the py file into staging area
![025](/100_images/025.png)
Now we need rollback this incorrect code part with `git revert HEAD`
After that your default IDE will poump out like this. You can see the previous commit number and the first line represent the commit message.
We better add the reson why we want to revert, like ***disk_full() function is not defined***
![027](/100_images/027.png)

After completed the revert commit, you will see the following output
![028](/100_images/028.png)

If you go back to see you code, you will find the undefined function has been removed.
![029](/100_images/029.png)


You can use `git log -p -2` to review the most recent 2 commit. For the screentshot you can see two commit history: 1c3* and 203*. 1c3 is the revert commit 
![026](/100_images/026.png)

<br></br>

### 9.Identifying a Commit
`git log -1` present the recent one record for repository
Find the recent two records `git log -2` and `git show 




## Branching and Merging


### Create new Branches
show the branch list of your repository. I only have one master branch in current repository
`git branch`
 ![029](/100_images/030.png)

`git branch 02_feature` we can create a new brancn ***02_feature*** in this way. But we still on the master branch
 ![031](/100_images/031.png)

 Use `git checkout` to switch to new branch
 We can also use `git checkout -b xxxxx` to combine create and switch command into one 
 ![031](/100_images/033.png)







### merge conflict

`git merge 02_feature`
will cause a CONFILICT
![diff](/100_images/11.png)
we can use `git status` to check the conflit, and use IDE (Vscode) to accept both changes
![diff](/100_images/10.png)
check current merge status
![diff](/100_images/012.png)


graph show merge
`git log --graph --oneline`
![diff](/100_images/013.png)

### Initialize GitHub



https://gist.github.com/bsara/5c4d90db3016814a3d2fe38d314f9c23

before we modify the remote 
![diff](/100_images/013.png)

`git remote -v`

```
# show remote status
git remote show origin
```
After I add **LICENSE.md** directly from browser, the remote master repo has changed. You can see **out of date** the remote change has not reflected on local repo.
![diff](/100_images/015.png)

git fetch fetchs remote updates but doesn't merge 
git pull fetches remote updates and merge

git fetch copy the remote repo to remote branch
![diff](/100_images/017.png)

use git check out to see the working tree
![diff](/100_images/018.png)


git log origin/master -2
the newest is the remote commit and belong to (origin/master)
our local repo is fall behind and assigned as HEAD
![diff](/100_images/019.png)


git status
![diff](/100_images/020.png)


git merge origin/master
![diff](/100_images/021.png)






After you install a new OS environment, and you need setup the Git envrionment to 
sync your repo on local and remote. Here is a few steps you need to do:
1. (Mandatory) [Check for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys) and you might don't have the following folders under C:/User/
![diff](/100_images/034.png)

2. (Optional) [Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) You can copy old SSH key from `D:\OneDrive\03_Academic\22_AWS_putty\15_github` or you can check your github keys settings https://github.com/settings/keys to confirm whether you have the old key or add a new key which generated in next [Add a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) section
   
3.  add ssh key into user file and use command to load
4.  Config globle for git initiation






### End

```
git pull origin master

echo "# xyz_repo" >> README.md

git init

git add README.md

git commit -m "first commit"

git branch -M main

git remote add origin https://github.com/mikeyj777/Coursera_DataStructsAndAlgos.git

git push -u origin main
```
