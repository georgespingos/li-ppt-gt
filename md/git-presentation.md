![](https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png)
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
### Git Integration

**bash**

You don't really need anything else!

v--------------

* Microsoft Visual Studio (even 2008)
* Sublime Text 2/3
* notepad++
* eclipse
* Oracle Solaris Studio
* Anything from this decade...

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
A snapshot of your working tree at a certain point in time, identified by a revision number.

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

## Setup Local repository

To set up a git repository locally:


    $ git init

Every commit gets a globally unique identifier (SHA-1 hush)
 
> 93ae4a12f286da8bdf24b041c2e8dfc4e3b


Note:
git works with snapshots not revisions

--------------

### Commits are local

* git commit affects **only ** your repository 

* Commits are cheap & fast

* **Commit as often as possible!**

*git push in order to share your commits*

--------------

## Staging area / The index

When you edit/add/remove files, only **your** working tree changes.

--------------

## File life cycle
![](http://i.imgur.com/kBD4Q8v.png)

--------------

#### Staging area / The index (cont.)

To show the current index state
 
	$ git status 

To add a file to the index:
	
	$ git add my-new-file.ext

Note:
#### .gitignore special file
#### per stack case

--------------

#### Staging area / The index (cont.)

**Oops!**

Unstaging a staged file:

	$ git reset HEAD my-file.ext

Unmodifying a modified file

	$ git checkout -- my-file.ext
--------------

#### Staging area / The index (cont.)

To add all changes

	$ git add . [--all]

To commit the changes saved in the index:

	$ git commit

View commit history	

	$ git log

To see what is staged and will go into next commit
	
	$ git diff --staged

--------------

## Branching

A branch is essentially another way your repository takes (parallel universe).

--------------

SVN/TFS vs Git

--------------
### SVN/TFS

every branch (or tag) you check out resides in a **separate ** folder. 

--------------

### In Git

*files and folders of the previous branch are **replaced** with those in the new branch (using magic and fairy dust).*

--------------

![](http://anishjoshi.github.io/Starting-with-Git-and-GitHub/images/git_branch_strategy.png)

--------------


When in a Git repository, you are always in a branch

	$ git branch


Note: 

#### detached HEAD

v--------------

### Examinig branches

Lists remote branches

	$ git branch -r

List all tracked branches

	$ git branch -a

--------------

Creating a new branch

	$ git branch my-new-branch

Creating and switching to new branch all in one

	$ git checkout -b my-new-branch

Switching from branch to branch

	$ git checkout my-new-branch

--------------
### Merging 

brings the contents of another branch (possibly from an external repository) into the current branch.

### To merge two branches, we have to move to the branch that contains the other branch commits

--------------

### Merging - Happy path

Note:

### Fast-Forward merges

*Switch(checkout) to target branch

	$ git checkout target-branch

*Apply the merge

	$ git merge my-new-feature-branch

*We are done!



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

Tags are fetched when checking out a branch, ***not*** the entire repository

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

# A "master repoistory" is a policy decision, not a technical one.

--------------


### Pushing a new branch to the remote

	git push -u origin new-branch

-u: tracks the remote branch

v--------------


Push beaviour

* Matching (Git 1.x.): will push all your local branches to the ones with the same name on the remote.

* Simple (Git 2.x): will push only the current branch to the one that git pull would pull from, and also checks that their names match.



	$ git config --global push.default matching/simple


--------------
### Checking for modifications

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

	$ git pull

**It is context sensitive** 

v--------------

### Notes on pull:


### **Beware: automatically merges the commits without letting you review them first**

--------------

