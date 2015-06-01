### Setting up git
    $ git config --global user.name "Your Name Here”
 
    $ git config --global user.email "your_email@youremail.com"



#### Setup Line Ending Preferences

Unix/Mac users:


	git config --global core.autocrlf input
	git config --global core.safecrlf true

Windows users:

	git config --global core.autocrlf true
	git config --global core.safecrlf true



### Architecture

![](http://i.imgur.com/l4PlC9x.png)




#### Definitions

* Working tree: A directory in your filesystem that is associated with a repository, containing files & sub-directories.

* Repository: A collection of commits & branches, saved in the .git directory.
 
* Commit: A snapshot of your working tree at a certain point in time, identified by a revision number.
 
* HEAD: The name for the commit thats currently checked out in the working tree.

> **A "master repoistory" is a policy decision, not a technical one**

By default you’ll only have the “origin” remote repository, which is the repository you did git clone from.

Show details with 

> git remote show NAME

Add new remotes using

> git remote add NAME URL



### Setup Local repository

To set up a git repository locally:


    $ git init

Every commit gets a globally unique identifier (SHA-1 hush), not a simple revision number 
> 00de993ae4a12f286da8bdf24b041c2e8dfc4e3b

For commands you can cut off the end of the identifier, as long as that is still unique within your repository



### Remote Repositories

A Remote Repository is thestarting point for working with existing code. It creates a local repository copying & tracking the master branch from the specified location.

    git clone

* Commits are local

* git commit only affects your repository, not the origin or any other remote repository

* Commits are cheap & fast

* **Commit as often as possible!**

*git push in order to share your commits*

AGAIN:
> **A "master repoistory" is a policy decision, not a technical one**



### Staging area/The index

When you edit/add/remove files, only your working tree changes

To commit changes, you first save them in the index with git add or git rm

To show the current index state
 
	git status 

To add a file to the index
	git add my-new-file.ext

To add all changes

	git add . [-all]

To commit the changes saved in the index, and clear the index afterwards:

	git commit



### Branching

A branch is essentially another way your repository takes (parallel universe).

> **In SVN and TFS, every branch (or tag) you checked out resides in a separate folder.** 

> **In Git, every time you check out a branch, files and folders of the previous branch are replaced with those contained in the new branch. essentially you have ONE (1) to manage**




When in a Git repository, you are always in a branch
(warning: detached HEAD)

Branches in the current repository:

	git branch
	git branch -r
	git branch -a

Creating a new branch

	git branch my-new-branch

Creating a switching to new branch all in one

	git checkout -b my-new-branch

Switching from branch to branch

	git checkout my-new-branch



### Merging branches

**Really Imprtand:** To merge two branches, we have to move to the branch that contains the other branch commits

Switch(checkout) to target branch

	git checkout target-branch-to-incorporate-changes

Apply the merge

	git merge my-new-feature-branch

Either resolve potential conflicts or we are done!

*(Note on Fast-Forward)*



### Difference between branches

 	git diff source-branch..target branch

GUI clients work best here:

	git mergetool
*(Might need setup/can use custom)*

Another way would be:

	git log my-branch..master



#### Note on conflicts
A conflict-marked area begins with
<<<<<<< and ends with >>>>>>>. The two conflicting blocks themselves are divided
by a sequence of =======. 
