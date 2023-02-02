# Notes for Git and GitHub
https://www.geeksforgeeks.org/ultimate-guide-git-github/

Git Repository Structure consists of 4 parts:  

1. Working directory: This is your local directory where you make the project (write code) and make changes to it.
2. Staging Area (or index): this is an area where you first need to put your project before committing. This is used for code review by other team members.
3. Local Repository: this is your local repository where you commit changes to the project before pushing them to the central repository on Github. This is what is provided by the distributed version control system. This corresponds to the .git folder in our directory.
4. Central Repository: This is the main project on the central server, a copy of which is with every team member as a local repository.

All the repository structure is internal to Git and is transparent to the developer. 

// Initialze the project directory as a local git repository

git init

Some commands which relate to repository structure:  

// transfers your project from working directory to staging area.

git add .

git add --all

// transfers your project from staging area to Local Repository.

git commit -m "your message here"

git commit -a -m "Add and Committ changes on one line."

git status --short
 >M index.html

Short status flags are:

?? - Untracked files

A - Files added to stage

M - Modified files

D - Deleted files


//To view the history of commits for a repository, you can use the log command:

git log
>commit 09f4acd3f8836b7f6fc44ad9e012f82faf861803 (HEAD -> master)
>Author: w3schools-test 
>Date:   Fri Mar 26 09:35:54 2021 +0100
>
>    Updated index.html with a new line
>
>commit 221ec6e10aeedbfd02b85264087cd9adc18e4b26
>Author: w3schools-test 
>Date:   Fri Mar 26 09:13:07 2021 +0100
>
>    First release of Hello World!

//Git Help
//There are a couple of different ways you can use the help command in command line:

//git command -help -  See all the available options for the specific command
//git help --all -  See all possible commands


## Branches

//In Git, a branch is a new/separate version of the main repository.

//Create a new branch:

git branch hello-world-images

//Created a new branch called "hello-world-images"

//Note: Using the -b option on checkout will create a new branch, and move to it, 
if it does not exist




git branch
>  hello-world-images
>* master
//The new branch with the name "hello-world-images", but the * beside master 
//specifies that we are currently on that branch.

//checkout is the command used to check out a branch. Moving us from the 
//current branch, to the one specified at the end of the command:

git checkout hello-world-images

> Switched to branch 'hello-world-images'

//Make changes to the new branch

git add --all

git commit -m "Committ changes to the images branch"

git checkout -b emergency-fix
> Switched to a new branch 'emergency-fix'

//Make emergency fixes in the new branceh
//When ready, Committ the change to emergency-fix
//and merge them back into the master branch.

git commit -a -m "Fixed the problem."

git checkout master

git merge emergency-fix

//Remove the emergency-fix branch

git branch -d emergency-fix


# Working with GitHub

## Workout the GitHub ssh login stuff

Go to Github and create a Repository that you can push the local project to and
make it the origon/master.

//git remote add origin URL specifies that you are adding a remote repository, with the specified URL, as an origin to your local Git repo.

git remote add origin https://github.com/w3schools-test/hello-world.git


//Now we are going to push our master branch to the origin url, and set it as the default remote branch:

git push --set-upstream origin master


//git pull is a combination of fetch and merge
//git fetch gets all the change history of a tracked branch/repo.

git fetch origin

//Check the git status

git status

//View the log to see any changes.

git log origin/master

//Show the differences between our local master and origin/master:

git diff origin/master

//Merge our current branch (master) with origin/master:

git merge origin/master

git status
>On branch master
>Your branch is up to date with 'origin/master'.
>
>nothing to commit, working tree clean

//But what if you just want to update your local repository, without going through all those steps?
//pull is a combination of fetch and merge. It is used to pull all changes from a remote repository into the branch you are working on.

git pull origin

//Make some changes
//or add some files
//Then push to GitHub
//Note the -a to add the files in one command

git commit -a -m "Added some files and made some changes."

git status
>On branch master
>Your branch is ahead of 'origin/master' by 1 commit.
>  (use "git push" to publish your local commits)
>
>nothing to commit, working tree clean

git push origin
>Enumerating objects: 9, done.
>Counting objects: 100% (8/8), done.
>Delta compression using up to 16 threads
>Compressing objects: 100% (5/5), done.
>Writing objects: 100% (5/5), 578 bytes | 578.00 KiB/s, done.
>Total 5 (delta 3), reused 0 (delta 0), pack-reused 0
>remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
>To https://github.com/w3schools-test/hello-world.git
>   5a04b6f..facaeae  master -> master

## Branches

Creating branches on GitHub is fairly straightforward using their web interface.
After using git pull to make sure you are uptoday with GitHub
use:

git branch -a

To see the branches available on GitHub you can also use
git branch -r to see remote branches.

To switch to a branch in the remote repository

git checkout RobsNotes

git status

Create a new local branch and push it to GitHub

git checkout -b robs_git_notes

git status

Make any changes required.

git add --all

git status

git commit -m "Updated robs_git_notes branch"

git push origin robs_git_notes

You can now use GitHubs web interface to check the changes and merge them in to origin/master

Compare and Pull Request

Create Pull Request

Merge Pull Request

To keep the repo from getting overly complicated, you can delete the now unused branch by clicking "Delete branch".

## GitHub Flow

The GitHub flow works like this:

* Create a new Branch
* Make changes and add Commits
* Open a Pull Request
* Review
* Deploy
* Merge

## Create a New Branch
Branching is the key concept in Git. And it works around the rule that the master branch is ALWAYS deployable.

That means, if you want to try something new or experiment, you create a new branch! Branching gives you an environment where you can make changes without affecting the main branch.

When your new branch is ready, it can be reviewed, discussed, and merged with the main branch when ready.

When you make a new branch, you will (almost always) want to make it from the master branch.

## Make Changes and Add Commits
After the new branch is created, it is time to get to work. Make changes by adding, editing and deleting files. Whenever you reach a small milestone, add the changes to your branch by commit.

Adding commits keeps track of your work. Each commit should have a message explaining what has changed and why. Each commit becomes a part of the history of the branch, and a point you can revert back to if you need to.

## Open a Pull Request
Pull requests are a key part of GitHub. A Pull Request notifies people you have changes ready for them to consider or review.

 You can ask others to review your changes or pull your contribution and merge it into their branch.

## Review
When a Pull Request is made, it can be reviewed by whoever has the proper access to the branch. This is where good discussions and review of the changes happen.

Pull Requests are designed to allow people to work together easily and produce better results together!

## Deploy
When the pull request has been reviewed and everything looks good, it is time for the final testing. GitHub allows you to deploy from a branch for final testing in production before merging with the master branch.

If any issues arise, you can undo the changes by deploying the master branch into production again!

## Merge
After exhaustive testing, you can merge the code into the master branch!

Pull Requests keep records of changes to your code, and if you commented and named changes well, you can go back and understand why changes and decisions were made.



git remote -v
> origin  https://github.com/ConnorTech/Git-and-GitHub.git (fetch)
> origin  https://github.com/ConnorTech/Git-and-GitHub.git (push)


Git Ignore
When sharing your code with others, there are often files or parts of your project, you do not want to share.

Examples

* log files
* temporary files
* hidden files
* personal files
* etc.

Like this:
# ignore ALL .log files
*.log
# ignore ALL files in ANY directory named temp
temp/


## Git Revert
revert is the command we use when we want to take a previous commit and add it as a new commit, keeping the log intact.

Step 1: Find the previous commit:
    First thing, we need to find the point we want to return to. To do that, we need to go through the log.

    To avoid the very long log list, we are going to use the --oneline option, which gives just one line per commit showing:

    The first seven characters of the commit hash
    the commit message


    So let's find the point we want to revert:

    git log --oneline
    > 52418f7 (HEAD -> master) Just a regular update, definitely no accidents here...
    > 9a9add8 (origin/master) Added .gitignore
    > 81912ba Corrected spelling error
    > 3fdaa5b Merge pull request #1 from w3schools-test/update-readme
    > 836e5bf (origin/update-readme, update-readme) Updated readme for GitHub Branches
    > daf4f7c (origin/html-skeleton, html-skeleton) Updated index.html with basic meta
    > facaeae (gh-page/master) Merge branch 'master' of https://github.com/w3schools-test/hello-world
    > e7de78f Updated index.html. Resized image
    > ...

Step 2: Use it to make a new commit:
    We revert the latest commit using git revert HEAD (revert the latest change,  and then commit), adding the option --no-edit to skip the commit message editor (getting the default revert message):

    git revert HEAD --no-edit
    > [master e56ba1f] Revert "Just a regular update, definitely no accidents here..."
    ? Date: Thu Apr 22 10:50:13 2021 +0200
    > 1 file changed, 0 insertions(+), 0 deletions(-)
    > create mode 100644 img_hello_git.jpg

    //Check out the change.
    git log --oneline
    > e56ba1f (HEAD -> master) Revert "Just a regular update, definitely no accidents here..."
    > 52418f7 Just a regular update, definitely no accidents here...
    > 9a9add8 (origin/master) Added .gitignore
    
    Note: To revert to earlier commits, use git revert HEAD~x (x being a number. 1 going back one more, 2 going back two more, etc.)

## Git Reset
reset is the command we use when we want to move the repository back to a previous commit, discarding any changes made after that commit.

Step 1: Find the previous commit:
    
    First thing, we need to find the point we want to return to. To do that, we need to go through the log.

    To avoid the very long log list, we are going to use the --oneline option, which gives just one line per commit showing:

        * The first seven characters of the commit hash - this is what we need to refer to in our reset command.

        * The commit message

    git log --oneline
        > e56ba1f (HEAD -> master) Revert "Just a regular update, definitely no accidents here..."
        > 52418f7 Just a regular update, definitely no accidents here...
        > 9a9add8 (origin/master) Added .gitignore
        > 81912ba Corrected spelling error
        > ...

    We want to return to the commit: 9a9add8 (origin/master) Added .gitignore, the last one before we started to mess with things.

Step 2: Move the repository back to that step:

    We reset our repository back to the specific commit using git reset commithash (commithash being the first 7 characters of the commit hash we found in the log):

    git reset 9a9add8

    git log --oneline
        > 9a9add8 (HEAD -> master, origin/master) Added .gitignore
        > 81912ba Corrected spelling error
        > 3fdaa5b Merge pull request #1 from w3schools-test/update-readme
        > ...

    Warning: Messing with the commit history of a repository can be dangerous. It is usually ok to make these kinds of changes to your own local repository. However, you should avoid making changes that rewrite history to remote repositories, especially if others are working with them.

Git Undo Reset
Even though the commits are no longer showing up in the log, it is not removed from Git.

If you know the commit hash you can reset to it:

git reset e56ba1f

git log --oneline
    > e56ba1f (HEAD -> master) Revert "Just a regular update, definitely no accidents here..."
    > 52418f7 Just a regular update, definitely no accidents here...
    > 9a9add8 (origin/master) Added .gitignore