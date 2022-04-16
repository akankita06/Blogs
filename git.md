## Git common comands & terms

- `clone` - bring repo hosted somewhere like github into a folder on local machine
- `add` - track your files and changes in git
- `commit` - save your files in git
- `push` - upload git commits to a remote repo like github
- `pull` - download changes from remote repo to local machine
- **Pull request -** when you want your code to be reviewed, you’ll pull your code changes from feature branch to master branch and then merge to master


## Starting a new repo

- `git —version` - to check if git is installed in your machine
- Starting a new repo - 2 ways:
    - `git clone <link for clone with ssh>` - clone a repo from an existing remote repo
    - creating a new local repo and connecting it to a remote repo
        - `git init` - to initialize git in your local repo if you are creating a new repo in the local machine without cloning it
        - create a remote repo on github
        - `git remote add origin <link to remote repo>` - link the remote repo with local repo
- `.git` directory gets created in the directory if that directory has git initialized in it. It is a hidden folder (accessible by running `ls -la`)


## Git workflows & commands
<img src="https://github.com/akankita06/notes/blob/8d8d7c1a573efe4039834d3e0c26d56d48987f36/images/git%20workflows.png" width=50% height=50%>
- `git status` - shows all files updated or modified but haven’t been committed
- `git add` - tell git to track a file, to save new snapshot of contents of modified file for the next commit
    - `git add -A` - stage all changes = `git add .` ; `git add -u`
    - `git add .` - stage new files & modifications, without deletions (on the current dir or sub-dir)
    - `git add -u` - stage modifications and deletions, without new files
- `git commit` - save changes to the files
    - `git commit -m “<commit message>”` - commit changes with title
    - `git commit -m “<commit message>” -m “<commit desc>”` - commit changes with title and desc
    - `git commit -am “<message>”` - adds and commits at the same time but it only works for modified files and not for newly created files
- `git push` - push the changes to remote repo and make it live on github
    - `git push origin master`
        - `origin` - word that stands for location of your repo in github (github server with remote repo)
        - `master` - main branch to which the changes are pushed
    - `git push -u origin master` - sets origin master as upstream, so next time you can just write `git push` and it will automatically push to origin master
        - `-u` - basically sets up a tracking connection between local and remote branch so a direct push and pull can be done without mentioning specific branch all the time. Tracking works both ways - bring local to remote or remote to local
        - `git push —-set-upstream origin <branch>` - push newly created local branch <branch> to the remote repo. `-u` is shorthand for —set-upstream.
  
  
## Setting up tracking connections

- `git push -u origin master` - sets origin master as upstream, so next time you can just write `git push` and it will automatically push to origin master
- `git branch -—track <local_branch> <remote_branch>` - here local and remote would know each other.
- `git checkout -—track <remote_branch>`  - if no local branch is mentioned, git will automatically create branch with same remote branch name
- **Advantages of setting up tracking connections:**
    - Can do a direct push and pull between local and remote branch without having to mention specific branch names all the time. Just a `git push` or `git pull` command would suffice.
    - Can tell which commits are missing from remote and local on GUI or through the CLI command - `git branch -v`
  
## Branching

- **terms**
    - master - main branch
    - feature branch - other branches you create
    - changes on feature branch cannot be seen on master and vice-versa (unless merged)

    <img src="https://github.com/akankita06/notes/blob/8d8d7c1a573efe4039834d3e0c26d56d48987f36/images/git%20branching.png" width=50% height=50%>
  
- **creating new branch & swithcing between branches (`git branch` and `git checkout`)**
    - `git branch` - list of branches in your local repo
    - creating a new branch
        - `git checkout -b “<branch_name>”` - create a new branch and switch to that branch
        - `git branch <branch> <commit_hash>` - start a branch at a particular commit
    - switching between branches**
        - `git checkout` - switch between branches
        - `git switch <branch>` - only for switching to another branch
    - renaming branches**
        - `git branch -m <new_name>` - rename the HEAD (currently checked out) branch
        - `git branch -m <old_branch>  <new_name>` - rename a non-head branch (not currently checked out)
        - git does not allow to rename a remote branch. For that, you’ll need to delete the branch in remote, and push those changes in another branch to the remote
    - `git checkout -b <branch_name>` vs `git branch <branch_name>`
        - `git branch <branch>` - creates a new branch but leaves you on the current branch
        - `git checkout -b <branch>` - creates a new branch and checks out that new branch. So it does following steps:
            - `git branch <branch>`
            - `git switch <branch>`
  
  - **deleting a branch**
    - `git branch -d <branch_name>` - delete a branch once merged (on local)
    - `git push origin -—delete <branch>` - remove remote branch. Always delete its local tracking branch if any
    
- **push & pull branches**
    - `git push -—set-upstream origin <branch_name>` - push newly created local branch <branch_name> to the remote repo.
    - `git pull origin master` - get changes after a merge to local master
        - if upstream is set as origin master, then - `git pull`
- **differences between branches**
    - `git diff` - difference between master and current branch (from the last commit)
    - `git diff <branch_name>` - diff between current branch and <branch_name>
    - `git diff <filename>` - local changes (uncommitted and unstaged) made to a file in the current branch
    
- **compare branches**
    - `git log main..<branch>` - which commits are in <branch> but not in main
- `git log` - log of all commits on the branch
  
- **merge & rebase**
    - `git merge master` - merge master into current branch in local repo (not a common pattern)
    - `git pull origin master —-rebase` - rebase all commits from remote master on local branch
    
    - rebase
        - re-commiting all commits of the current branch onto a diff base commit
        - looks like dev history has been in a straight line i.e. i want the point at which i branched to move to a new starting point
    - merge
        - takes all changes in one branch and merges them into another branch in one commit
        - like a knot between 2 branches which creates additional merge commit
        
    - when to use which:
        - merge
            - when you’ve created a branch just to develop a single feature and want to bring it to master. You don’t care about maintaining interim commits
            - when you want to add changes of a branched branch back to base branch. Eg: changes from local branch to master
        - rebase
            - when you are doing a dev and another dev is making unrelated code change. You want to pull those changes and rebase your local branch to mitigate any merge conflicts, etc.
            - when you want to add changes of a base branch to a branch out branch.Eg: pull changes of master to local branch
  
  ## Undo mistakes with git

- `git restore` - to undo local changes that have not been staged or committed yet
    - `git restore <filename>` - remove all local changes (uncommitted and unstaged) in a file. Discarding uncommitted local changes cannot be undone. This also works if a file was deleted and you want to undelete it. Command - `git restore <deleted_filename>`
    - `git restore -p <filename>` - discard indvidial patches / chunks / lines of changes in a file
    - `git restore .` - discard all local changes (basically a do-over of your work)
    - `git restore -—source <commit_hash> <filename>` - for restoring a only the given file to an old commit hash. (Note - in this case, restore command works even though here the file has been committed)
  
  - `git commit --amend` - for making changes to the latest commit (HEAD commit).
    - For any additional changes that need to go in the last commit -
        - make the change
        - stage the change
        - use this command to add that change to the last commit
    - `git commit —-amend -m “<new_commit_message>”` - change the title of the last commit
    - `—-amend` rewrites history (recreated commit with a new hash). Never change history for commits that have already been pushed to a remote repo.
    
- **to undo local changes that have been committed but from a commit in the middle (not the one HEAD is pointing)**
    - `git revert <hash_of_commit_to_undo>`  - revers a commit in the middle by creating opposite changes to the commit you want to revert. It creates a new commit that includes theseopposite changes.
    - `git reset -—hard <old_commit_hash>` - clear all changes and commits after a certain commit and reset the HEAD to the given commit hash. In a way, go back in time to that earlier commit.
    - `git reset —-mixed <old_commit_hash>` - unlike previous command, this won’t clear the changes, it will keep the changes and commits that came after the given commit hash as local changes. The HEAD now points to the given commit hash which becomes our latest commit.
  
- **Reflog** - it is like git’s activity log (every movement of the HEAD pointer). It stores info about when you checkout, commit, restore, etc. Command - `git reflog`. Use cases:
    - recover deleted commits after we reset to an earlier commit - `git reset <reflog_hash_of_state_just_before_deleting_commits>` or if you want to create a new branch with that - `git branch <branch_name> <reflog_hash>`
    - similarly for recovering deleted branch - find reflog hash just for jsut before deleting that branch and create a new branch with it - `git branch <branch_name> <reflog_hash>`
    
- **commits to wrong branch**
    - moving a commit to a new branch -  like when you committed changes to the wrong branch, and now want to move and commit those changes to a new branch. Done in 2 steps:
        - create a new branch with the commit - `git branch <branch_name>`
        - and remove that commit from old branch - `git reset HEAD~1 —-hard`
    - moving a commit to a different branch (existing) - steps
        - copy hash of the commit to move from current branch
        - switch to the different branch - `git checkout <diff_branch>`
        - cherry pick the commit in that branch - `git cherry-pick <commit_hash>`. Cherry pick is used to move a commit to a different branch.
        - checkout old branch - `git checkout <old_branch>`
        - remove that commit from old branch - `git reset —hard HEAD~1`
  
- **Interactive rebase** - a lot can be done through this like following. 3 steps for every interactive rebase session:
    - determine how far back do you want to go - **parent commit** of the commit where the changes are to be made
    - start rebase session - `git rebase -i HEAD~3`
    - in the editor, determine only which actions you want to perform (no commit data changes here). Note - commits are listed in rev. order. Save the action changes.
    - make changes in the new screen you get
    - eg use cases
        - edit commit message of an old commit - action - `reword`
        - delete old commits - action - `drop`
        - squash multiple commits into one - action - `squash`. The commit you mark as squash is combined with the commit on prev line (commit right after squash actioned commit). Squashing creates a new commit.
        - adding a change to an old commit or fix an old commit
            - `git add <changed_file>`
            - `git commit —fixup <commit_hash_where_change_goes>`
            - `git rebase -i HEAD~4 —-autosquash`
        - split / edit an old commit
  

## Search & find

Filtering your commit history 

- by date - `--before / --after`
- by message - `--grep`
- by author - `--author`
- by file - `-- <filename>` (a gap in between dash and file name)
- by branch - `<branch-A>`

Eg:  

- `git log --author="ABC"`
- `git log --grep="refactor" --after="2022-03-04"`
- `git log <branch>`

  
## Resources:

1. [git and github for beginners crash course](https://www.youtube.com/watch?v=RGOj5yH7evk&ab_channel=freeCodeCamp.org)
2. [git branches tutorial](https://www.youtube.com/watch?v=e2IbNHi4uCI&list=PLK9vszOhGRSZnsLf6EAAkA7HeEux0LYNI&index=3&ab_channel=freeCodeCamp.org)
3. [how to undo mistakes with git using CLI](https://www.youtube.com/watch?v=lX9hsdsAeTk&list=PLK9vszOhGRSZnsLf6EAAkA7HeEux0LYNI&index=2&ab_channel=freeCodeCamp.org)
4. [advaced git tutorial](https://www.youtube.com/watch?v=qsTthZi23VE&list=PLK9vszOhGRSZnsLf6EAAkA7HeEux0LYNI&index=5&ab_channel=freeCodeCamp.org)
  
