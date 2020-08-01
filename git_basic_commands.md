> 1. Go to the folder 
> 2. **git init** > this will make sure the files are going to be tracked see there is a file created with .git
> 3. **git status** > on branch master no commit untracked files
> 4. **git add** > local directory to staging index
>    - **git add helloworld.txt** and check status again
> 5. **git commit** > staging index to local repository
>    - **git commit -m "initial commit"**
> 6. **git remote add origin <url>** > just added a remote named origin

------

This remote is your connection to your remote repository in GitHub. You can add as many remotes as you want.

Now that we have linked up our local repository with our remote one, we’re ready to push our code. But first, we have to add branches. Don’t worry about what branches are for now, we’ll go over them in a little bit. Just know that when you created your GitHub repository, it added a branch called master by default. 

Now, in your local machine, there will be two versions of all of your branches, remote and local. In your local machine, Git created a branch called master by default, so we will have to pull the remote master branch that has been made for us in our remote repository. So go ahead and run the following command

> **git push -u origin master**

We are now left with remote branches. The remote repository that we created in GitHub maintains its own set of branches. In order to stay up do date with them, our local repository maintains a remote version of all the local branches. Go ahead and run the following command in your terminal

> **git branch --all**
>
> - **git branch**
>
> **git pull origin master**

But wait, we still need to know what branches are. Right. Basically, you can think of a branch as a parallel universe. Say you want to try out a new feature in your cool mobile app but do not want to mess up the work that’s already been done. In this scenario, you can create a separate branch and do that. If things start going south, you can ditch that entire branch and come back to your original branch like nothing happened. But if you feel that the new feature would be a great addition to the app, you can merge that new branch with the original one. By default, Git names its main branch as master. It can’t do version control without a main branch. So let’s create and delete some branches, shall we

> **git branch *test_branch*** > for creating branches here it created a branch named as ***test_branch***
>
> **git checkout *test_branch*** > for switching pointer/head
>
> **git checkout -b *test_branch*** > both the above commands can be merged  creating and checkout 

There are two important Git commands that you need to understand when it comes to remote branches because you’ll be using them pretty often. They are pull and fetch . We used pull a little while ago, remember? They essentially do the same thing, but there’s a small difference. When you do a fetch, Git updates origin/master (or whatever remote branch you are fetching). But when you do a pull , Git updates origin/master and merges master with it.

> **git log** > for watching the history of commits
>
> **git log --stat** > gives statistics which files are changed
>
> **git diff *commit_id1 commit_id2***  > Comparing two commits found from git log command >> here order of these commit is important > better user most resent id in between two as second commit id green line with + sign is added, red line with - sign is removed whereas black lines are intact.
>
> - **git diff** > If  any parameter is not provided, it provides the difference between files present at staging area and  workspace area it will help you to detect bug which been introduced to any file that is not in the staging area, the staging area contains the changes of the most recent commit
> - **git diff --staged** > shows the difference between files in staging area and the most recent commit, verifying what we are going to commit
>
> **git clone <url>** > copying a repository >> other than this earlier we use SCP command

This is true for cloning a repository, but not for copying a directory. The main reason to use git clone rather than copying the directory is because git clone will also copy the commit history of the repository. However, copying can be done on any directory, whereas git clone only works on a Git repository. 

> **git checkout** > checkout to the previous commits if any issue arises, better to learn to switch between commits without knowing their commit id's
>
> **git init** > As came earlier initialize a repository but we don't have any commit yet, can be verified by running below command
>
> **git log** > checking all the commit available
>
> **git reset --hard** > If a file have been changed unintentionally in workspace and differ for staging area so after committing to the intentional change for a different file we run following command setting every thing back to normal 

> Before committing any changes also check if you have detach head(commit without label i.e branches) issue buy running :: 
> ***git status***
> if it is so run ::
> ***git checkout branch_name(or master)***
>
> ***git log --graph --oneline master coins***

ls -a >> shows hidden files

git is map with keys and values
You give value to git(content of file) it will calculate its hash (sha1)
SHA1 are 20 bytes in hexadecimal format, so they are sequence of 40 hex digit
these will be treated as git key

echo "Apple Pie" | git hash-object --stdin >> will give the hash for Apple Pie
echo "Apple Pie" | git hash-object --stdin -w >> generating and writing the hash if repository exist

Every object in Git has its own sha1

just type ls .git/objects > every folder inside will be named as starting sha1 digits of some objects

Now write  git cat-file 02f9d73215f79a41e3870881e4beabbc6c917bab -t/-p for knowing the type of the file it is blob

After one commit run git log you will get to know the recent commit hash
Write git cat-file -p <hash of the new commit>
you may get the sha of a tree, using this hash we can reach to the content again list of sha's of blob and tree

commit point to a tree that is root and then the points to blob or another tree.

A blob is not really a file it is content of a file and the file name and file permission are stored in tree not 
in blob

git count-objects  >> no. of objects in entire git structure

A tag is like a label for the current state of the project.
There are two types of tags >> regular tags and annotated tags

An annotated tag comes with a message >> git tag -a mytag -m "I love cheese cake"

git tag > to see all tags

Git normally puts branches(nothing but a reference a pointer to a commit actually) in a directory called ref(inside .git) and a subdirectory called heads(inside ref)

write > cat .git/refs/heads/master > this file contains a single line one sha1 and this  is sha1 of current commit

in .git there is one file HEAD(reference to a branch pointer to a pointers) > write cat .git/HEAD > ref/head/master that is it is pointing to the current branch which is master branch in our case

When you create a new commit, the new commit contains the information about the parent commit and now git see what is inside the HEAD file that is which branch information it is containing currently and it moved that branch to the new commit,head is still pointing at master

when you checkout new branch now head will point to the newly checked out branch can be verified by > 
 cat .git/HEAD, Now our content in the workspace will be changed same as the commit the new branch is pointing



if you run git cat-file -p <sha1 of merged commit> >> you will see two sh1 of two parents' commit

Remember references between commits are used to track history whereas all other references are used to track content

What is fast-forward merge??

Suppose you merged lisa in master, then you checkout lisa and try to merge master in this case fast forward happens and no more commits occurs now lisa will also point to master

At the time of detached head commits head itself moves alone not branch, if you don't want to loose those commits create branch at that time stamp after than you can again checkout the master again

Now suppose your current branch is spaghetti and you run the command git rebase master then git detaches the complete spaghetti branch from the lowest common ancestor between master and spaghetti(exclusive) and attaches it to master as their parent

Tags are one of the types of git database object along with commits,tress and blobs 

Annotated tags are discussed above, other kind of tags are light weight tags.
Tags are actually labels of the commits.

Creating a light weight tags.

git tag dinner

git tag > will show all the tags

Again there is a folder named as tags inside .git/ref that contains all the tags info.

cat .git/ref/tags/dinner > just gives the sha of the commit linked to it

One can say tag is like branch but it can't be moved just sticks to the same object ever

Run git clone <url>

and cat .git/config > it has the URL stored

Each git repository can remember the information about other copies of the same repository each other copies are called remote individually.

you can define as many remote as you want but at the time of cloning a repository git immediately defines a 
default remote and call it as origin > can be verified inside .git/config file

The default configuration says we have a master branch that maps over the master branch of remote.

To synchronize git also needs to know the current state of origin

Git tracks a remote branch by just exactly it tracks local branches > check .git/ref/remotes/origin, git will automatically update this information when we connect to a remote 

you may find that in this path(just mentioned above) some of the branches are missing or it may have only heads.
For the purpose of optimization these information are stored inside .git/packed-ref file
To know about these branches to which commit they are pointing at run

git show-ref master  > it will return all the branches that have master in their name which the local master branch and remote master branch

So the local branch in git is just a reference to a commit whereas remote branch is exactly the same thing. whenever you synchronize with a remote, git updates remote branches.

Now again if we change the in the local copy of the master branch
and run the command git show-ref master we will get local master and remote master pointing to the different commit..

To make change persistent at the remote run git push > it will push the changes to the remote server and will update remote master commit to the newer commit

Now suppose the scenario at the time you are going to push your changes into the remote and there is some changes pushed before your push, its kind of conflict
To deal with the conflict we should fetch the changes from the remote(results the same state of commits in local and remote), merge(may have to resolve conflicts) and then push

Git fetch followed by merge can be done by single command that is git pull

Don't use git push -f

Imagine a situation when you have to push your changes to the remote but you don't have the permission(basically at the time of contribution) than in that case first fork their repository means you will have the copy of their repository in your GitHub account(remote) then clone this forked repository into your local system.
you may have to link you git to the original repository from which you forked to keep track of changes in the original repo these known as upstream.
You can modify your local repository, pull changes from the upstream, resolve conflicts and push all these in the origin(forked repo).
You can now send pull request to the maintainers(to pull changes from your forked repo) of upstream.

========================================================================================================================================================================================================