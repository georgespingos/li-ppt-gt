![](https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png)
--------------

##Git

* Distributed version control system
	
* Really fast and efficient

* Branches are cheap and encouraged

* Knows how to merge

* Encourages agile practices

Note:

Frictionless Context Switching
Disposable Experimentation.
Feature Based Workflow

--------------

Please stay calm and do not panic!

---

# **Git does not support file locking by design**

---

--------------
## Git setup (windows)

msysgit 

![](https://msysgit.github.io/img/gwindows_logo.png)


Note:

###pdf with installation instructions via email

--------------

Git Extensions

![](http://0install.de/feed-icons/GitExtensions.png)

*Git Extensions is the only graphical user interface for Git that allows you control Git without using the commandline.*


--------------
## Git Tools/Integration

![](http://files.cyberciti.biz/cbzcache/3rdparty/terminal.png)

You don't really need anything else!

v--------------

* Microsoft Visual Studio (even 2005)
* Sublime Text 2/3
* notepad++
* eclipse
* Oracle Solaris Studio
* Anything from this decade...

--------------

## Notables Settings (1)
    $ git config --global user.name "Your Name Here"
 
    $ git config --global user.email "email@xyz.com"

--------------

## Notables Settings (2)

Unix/Mac users:


	$ git config --global core.autocrlf input
	$ git config --global core.safecrlf true

Windows users:

	$ git config --global core.autocrlf true
	$ git config --global core.safecrlf true



--------------

## Architecture

![](http://i.imgur.com/l4PlC9x.png)

--------------

## Definitions 

### Working tree
A directory in your filesystem that is associated with a repository, containing files & sub-directories.

--------------

## Definitions... 
 
### Repository
A collection of commits & branches, saved in the .git directory.

--------------

## Definitions... 

###Commit

A snapshot of your working tree at a certain point in time

--------------

## Definitions... 

###Branch

An active line of development.

A repository has a default master branch.

Branches are just pointers to various commits.

--------------


## Definitions... 
 
###HEAD
The name for the commit thats currently checked out in the working tree.

--------------

# A "master repository" is a policy decision, not a technical one.

--------------

## Setup Local repository

To set up a git repository locally:


    $ git init

Git uses globally unique identifier (SHA-1) extensively
 
> 93ae4a12f286da8bdf24b041c2e8dfc4e3b


Note:
git works with snapshots not revisions
SAH is a unique cryptographic hash, chances of collisions are practically 0

--------------

## Staging area / The index

When you edit/add/remove files, only **your** working tree changes.

--------------

## File life cycle
![](http://i.imgur.com/kBD4Q8v.png)

--------------

## Staging area / The index (cont.)

### File Classifications in Git

* Ignored
* Tracked
* Untracked

Note:

tracked: any file already in the repository or any file that is staged in the index. 

ignored: must be explicitly declared invisible or ignored in the repository even though it may be present within your working directory

untracked: is any file not found in either of the previous two categories

.gitignore special file

per stack case

--------------

#### Staging area / The index (cont.)

To show the current index state
 
	$ git status 

To add a file to the index
	
	$ git add my-new-file.ext

To add all changes

	$ git add . [--all]

v--------------

### Staging area / The index (cont.)

**Oops!**

Unstaging a staged file:

	$ git reset HEAD my-file.ext

Unmodifying a modified file

	$ git checkout -- my-file.ext

--------------

### Staging area / The index (cont.)

Removing a file

	$ git rm [--cached] my-file.ext

Removing a file from your directory and the index does not remove the file's existing history from the repository. 


Note:
* git rm --cached removes the file from the index and leaves it in the working directory

* git rm removes the file from both the index and the working directory

--------------

### About Removing a file

---

### Warning: Nuclear option 

	$ git filter-branch --tree-filter 'rm -f file-doeradicate.ext'HEAD

---

Note:
Any versions of the file that are part of its history already
committed in the repository remain in the object store and retain that history.

--------------

### Staging area / The index (cont.)


View commit history	

	$ git log

	$ git log --abbrev-commit --pretty=oneline

*has a gazillion switches to make it display everything*

To see what is staged
	
	$ git diff --staged

To commit the changes saved in the index

	$ git commit

v--------------

Under the hood of the index
	
	$ git ls-files --stage

--------------

### Commiting changes

## Every Git commit represents a single, atomic changeset

	$ git commit

--------------

## A commit is a two-step process

* stage your changes 
* commit the changes

--------------

### 0. New file created in the working tree 

![](http://i.imgur.com/xK5i9CS.png)

--------------

### 1. File added to index

![](http://i.imgur.com/qdeE44C.png)

--------------

### 2. File commited to repository

![](http://i.imgur.com/7ACc9aF.png)

--------------

### Commiting changes (cont)

* Commits are local

* git commit affects **only ** your repository 

* Commits are cheap & fast

* **Commit as often as possible!**

--------------

### Undoing commits - **Oops!**

#### Safe Option

make a new commit which undoes all the changes
	
	$ git revert SHA-I-hash

More advnaced
	
	$ git revert -m 1 HEAD

--------------

### Undoing commits - **Oops!**

---

## Warning! Danger! 

	$ git reset

---

--------------

### Undoing commits - **Oops!**


* remove the specified file from the staging area

* leave the working directory unchanged

* unstages a file without overwriting any changes


	$ git reset <file>

--------------

### Undoing commits - **Oops!**

* reset the staging area to match the most recent commit

* leave the working directory unchanged 

* unstages **all ** files without overwriting any changes


	$ git reset

--------------

### Undoing commits - **Oops!**


* Reset the staging area and the working directory to match the most recent commit

* overwrite **all changes in the working directory**

---

### this obliterates all uncommitted changes 
### (throws away local work)

	$ git reset --hard

---

--------------


### Reposity history

shows repo/branch history
	
	$ git log --pretty=format:'%h %s'--graph

*rember what we said about gazillion switches* 

--------------

### Rufiano

Who's to blame

	$ git blame my-file.ext

	$ git blame -L 12,22 my-file.ext

loads of switches: regex, commit range, line numbers...

---

Hidden trick:

	$ git gui blame my-file.ext

	$ git difftool start-commit-sha end-commit-sha my-file.ext


	
--------------

## Branching

A branch is essentially another way the repository takes (parallel universe).

--------------

### Branching

![](http://image.slidesharecdn.com/git-branching-model-130205024231-phpapp01/95/git-branching-model-7-638.jpg?cb=1360032415)

--------------

# SVN/TFS vs Git

--------------

### SVN/TFS

every branch (or tag) you check out resides in a **separate ** folder. 

--------------

### In Git

*files and folders of the previous branch are **replaced** with those in the new branch (using magic and fairy dust).*

--------------

### In a Git repository, you are always in a branch

	$ git branch


Note: 

#### detached HEAD

v--------------

### Examinig branches

List remote branches

	$ git branch -r

List all tracked branches

	$ git branch -a

Hardcore details

	$ git show-branch

--------------

### Branch Management 

Creating a new branch

	$ git branch my-new-branch [start-point]

Creating and switching to new branch all in one

	$ git checkout -b my-new-branch [start-point]

Switching from branch to branch

	$ git checkout my-new-branch

--------------

### Branch Management (cont.)

Delete local branch

	$ git branch -d the_local_branch

Delete Remote Branches
	
	$ git push origin --delete remote-branch


Note:
Git prevents you from deleting the current branch, switch somewhere else first!

### Git won’t allow you to delete a branch that contains commits that are not also present on the current branch. Unreachable commits :(

--------------

### Merging 

brings the contents of another branch  into the current branch.

### * To merge two branches, we have to start from the target branch *  

--------------

### Merging - Happy path

*Switch(checkout) to target branch

	$ git checkout target-branch

*Apply the merge

	$ git merge my-new-feature-branch

*We are done!

Note:

### Fast-Forward merges

--------------

### Merging - Sad path (conflicts - 1)

*Switch(checkout) to target branch

	$ git checkout target-branch

*Apply the merge

	$ git merge my-new-feature-branch
	
	Auto-merging my-file.cpp
	CONFLICT (content): Merge conflict in my-file.cpp
	Automatic merge failed; fix conflicts and then commit the result.

*Check your status

	$ git status

	On branch master
	You have unmerged paths.
	(fix conflicts and run "git commit")

--------------
### Merging - Sad path (conflicts - 2)

*Resolve conflicts
	
	$ git mergetool

*Check status

	$ git status
	
	On branch master
	All conflicts fixed but you are still merging.
	(use "git commit" to conclude merge)

*Conclude merge

	$ git commit

--------------

### Comparing Branches

Difference between branches

 	$ git diff source-branch..target branch

Another:

	$ git log my-branch..master


--------------

## Conflicts
A conflict-marked area begins with
<<<<<<< 

and ends with >>>>>>>.
 
The two conflicting blocks themselves are divided
by a sequence of =======. 

--------------

### Tags

###**Tags are immutable references**

* Point to a specific commit and thereafter does not change, even if the branch moves on.

* Good for marking releases. 
 
--------------

### Two flavours

Simple:

	$ git tag some-descriptive-tag

Annotated (preferrable):

	$ git tag -a v1 -m "Version 1 release"

--------------

### Tag Operations

Listing Tags

	$ git tag

Searching for a tag

	$ git tag -l 'v1.8.5*'

Arbitary Taging 

	$ git tag -a v1.2 9fceb02
v--------------

##Important

Tags are ***not*** pushed by default to remote repositories

	$ git push --tags

Tags are fetched when checking out a branch, ***not*** of the entire repository

	$ git fetch --tags

--------------

### Remote Repositories

A Remote Repository is the starting point for working with existing code. 

    $ git clone repository-url

v--------------

By default you'll only have the "origin" remote repository, which is the repository you did git clone from.

Show details with
 
	$ git remote show NAME

Add new remotes using

	$ git remote add NAME URL

--------------


### Pushing a new branch to the remote

	git push -u origin new-branch

-u: tracks the remote branch

v--------------


## Push beaviour

* Matching (Git 1.x.)

* Simple (Git 2.x)


	$ git config --global push.default matching/simple


Note:

Matching (Git 1.x.): will push all your local branches to the ones with the same name on the remote.

Simple (Git 2.x): will push only the current branch to the one that git pull would pull from, and also checks that their names match.

--------------
### Get all changes from remote
### (for paranoid devs)

	$ git fetch

downloads differences from the remote, but **does not
apply them!**

v--------------

### Notes on fetch:

* any time to update your remote-tracking branches
* never changes any of your own local branches
* safe to do without changing your working copy
* to integrate the commits into your master branch, use merge.

--------------

### Get all changes from remote 
### (for trusting devs)

	$ git pull

**It is context sensitive** 

Note:
###Beware: automatically merges the commits without letting you review them first

--------------

## Advanced features

* git rebase

* git cherry-pick

* git bisect

* git stash/apply

* git rev-list

* git grep

LOADS more...

v--------------

# Git workflow



--------------

# Questions/Demo