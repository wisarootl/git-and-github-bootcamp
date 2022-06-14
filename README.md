# Brief Description

This is my note for [The Git & Github Bootcamp](https://www.udemy.com/course/git-and-github-bootcamp/) course

# Course Covers

**Git Core :** **`Intro to Git`**, [**`Installation`**](#installation--setup), [**`Command Line`**](#command-line), [**`Git Basics`**](#git-basics), [**`Committing in Detail`**](#committing-in-detail), [**`Branching`**](#branching), [**`Merging`**](#merging)

**Next Level Git :** [**`Diffing`**](#diffing), [**`Stashing`**](#stashing), [**`Undoing Changes`**](#undoing-changes--time-traveling)

**Github and Collaboration Core :** [**`Github Basics`**](#github-basics), [**`Fetching & Pulling`**](#fetching--pulling), [**`Github Odds & Ends`**](#github-odds--ends), **`Collaborative Workflows`**

**The Other Parts :** **`Rebasing`**, **`Interactive Rebasing`**, **`Git Tags`**, **`Git Behind The Scenes`**, **`Reflogs`**, **`Custom Aliases`**

# Installation & Setup

- Configuration

```python
# user's name
git config user.name # get
git config --global user.name "[name]" # set

# email
git config user.email # get
git config --global user.email "[email]" # set

# default branch-name
git config init.defaultBranch # get
git config --global init.defaultBranch main # set
```

# Command Line

- `ls` : list directory content

- `ls -a` : list all directory content including hidden one

- `pwd` : print working directory (return current working directory)

- `cd` : change directory (only `cd` is same as `cd ~`)

- `cd ..` : back to parent directory

- `cd /` : go to terminal directory

- `cd ~` : go to user home

- `cd c/folder` : go to folder in drive c

- `mkdir test` : create folder

- `start folder`(Windows) : open folder in file explorer (`open folder` for other OS)

- `start .` (Windows) : open current working directory in file explorer (`open .` for other OS)

- `echo "" > index.html`(Windows) : create index.html file in current working directory (`touch index.html` for other OS)

- `cat > b.txt` + `enter` + `hello` + `enter` + `crtl+v` : create file with `hello` in content

- `cat b.txt` : look at content

- `cat b.txt >> c.txt` : concatenate b.txt to c.txt

- `subl` : Open sublime text (Windows). follow config below first.

  - add code below in file `C:\Users\Titta\.bash_profile`

  - `alias subl="/c/Program\ Files/Sublime\ Text/sublime_text.exe"`

- `open -a “Sublime Text”` (Other OS) : open sublime text for other OS

- `mv index.html about.html` : change name `index.html` to `about.html`

- `mv style.css /css` : move `style.css` to `/css` subfolder

- `rm <file>` : remove file

- `rm -r <folder>` : remove folder (-r recursive inside folder as well)

- `clear` : clear output

- `cp (-r) <file/folder name> -r <folder>` : copy file/folder use -r for folder (recursive)

- `nano b.txt` : open text editor

# Git Basics

- Repo (Repository) : workspace / folder

- `git status`

- `git init`

- `git add file1 file2`

- `git add .`

- Working Directory

- Staging Area : Something intermediate between working directory abd repo

- Repo (Repository) : workspace / `.git` folder

```mermaid
flowchart LR
A(Working Directory) -->|git add| B(Staging Area)
B -->|git commit| C(Repository)
```

- `git commit -m "message"`

- `git commit -a -m "message"` or `git commit -am "message"` : `git add <tracked-file>` and `git commit -m "message"`. Note: `<tracked file>` is not include new file.

- `git log`

# Committing in Detail

- Atomic Commit : 1 commit, 1 thing

- Use present tense in Git Commit message (It is only convention in Git Docs)

- Change default text editor for `git commit` without message

```
git config --global core.editor "code --wait"
```

- `git log --oneline`

- `git commit --amend` : change last commit

# Branching

- `git branch` : list all branches

- `git branch <branch-name>` : create new branch

- `git switch <branch-name>` : switch branch

- `git checkout <branch-name>` : switch branch

- `git switch -c <branch-name>` : create and switch branch

- `git checkout -b <branch-name>` : create and switch branch

- **Commit before switch branch**

- `git branch -d <branch-name>` : delete fully merged branch

- `git branch -D <branch-name>` : force delete unmerged branch

- `git branch -m <branch-name>` : rename current branch to `<branch-name>`

# Merging

- Merge `<incoming-branch>` into `<receiving-branch>`. We have to be on the `<receiving-branch>`

```
git switch <receiving-branch>
git merge <incoming-branch>
```

- Fast-Forward Merge : `<receiving-branch>` and `<incoming-branch>` are in the same chain. `<receiving-branch>` is in the past and will be fast forward to `<incoming-branch>`

<p align="center"><img src="./asset/01-git-merge.png" alt="drawing" style="width:400px;"/> <img src="./asset/02-git-merge.png" alt="drawing" style="width:400px;"/></p>

- Non Fast-Forward Merge **without Conflict** : `<receiving-branch>` and `<incoming-branch>` are in the different chains. Git will generate new commit consisting both chains from `<receiving-branch>` and `<incoming-branch>`.

<p align="center"><img src="./asset/03-git-merge.png" alt="drawing" style="width:400px;"/> <img src="./asset/04-git-merge.png" alt="drawing" style="width:400px;"/></p>

- Non Fast-Forward Merge **with Conflict** :
  1. open files with merge conflicts
  2. remove the conflicts and remove conflict marker
  3. `git add .` and `git commit`

# Diffing

- `git diff` : working directory and staging area

- `git diff HEAD` : working directory and HEAD (last commit)

- `HEAD~1` : parent of head

- `git diff --staged` : last commit and staging area

- `git diff <filename1> <filename2>` : narrow down to specific `<filename1>` and `<filename2>`

- `git diff <branch-name1>..<branch-name2>` : `<branch-name1>` and `<branch-name2>` `<old>..<new>`

- `git diff <commit-hash1>..<commit-hash2>` : `<commit-hash1>` and `<commit-hash2>` (`<commit-hash>` is git hash, some pre-fix of git hash)

# Stashing

- save uncommitted changes without unnecessary commits.

- `git stash` : save all uncommitted change (staged and unstaged)

- `git stash pop` : pop oldest stash (FIFO) and re-apply to current working copy

- `git stash apply` : apply without remove

- `git stash list` : show stash queue (FIFO)

- `git stash apply stash@{<id>}`, `git stash apply stash@{2}` : apply specific stash in the queue

- `git stash drop stash@{<id>}`, `git stash drop stash@{2}` : remove specific stash in the queue

- `git stash clear` : clear all stash

# Undoing Changes & Time Traveling

- `git checkout` are old command that can do many thing but it is confusing. There are 2 new command for more specific thing: `git switch` and `git restore`

```mermaid
flowchart LR
A(git checkout) --> B(git switch)
A --> C(git restore)
```

- `git checkout <commit-hash1>` : go to specific commit (`<commit-hash>` is git hash, some pre-fix of git hash)

- Detached HEAD : Head point to specific commit instead of branch. (Normally HEAD point to branch)

- `git switch <branch-name>`, `git checkout <branch-name>` : re-attaching head

- `git checkout HEAD~1` : reference relative to head, go to parent of head

- `git checkout HEAD~2` : reference relative to head, go to grandparent of head

- `git switch -` : go back to current commit of the branch

- `git checkout HEAD <file>` or `git checkout -- <file>` or `git restore <file>` : discarding changes in that files, reverting back to the head.

- `git restore .` : discarding all changes, reverting back to the head.

- `git restore --source HEAD~1 <file>` : git restore to 2 commit ago

- `git restore --staged <file>` : unstage file (move from staging area t working directory)

- `git reset <commit-hash>` : remove commit (but not remove change in working directory)

- `git reset --hard <commit-hash>` or - `git reset --hard HEAD~1` : remove commit and remove change

<p align="center"><img src="./asset/05-git-reset-revert.png" alt="drawing" style="width:400px;"/> <img src="./asset/06-git-reset-revert.png" alt="drawing" style="width:400px;"/></p>

- `git revert <commit-hash>` : similar to `git reset` but not remove commit. it create new commit with undo change.

<p align="center"><img src="./asset/05-git-reset-revert.png" alt="drawing" style="width:400px;"/> <img src="./asset/07-git-reset-revert.png" alt="drawing" style="width:400px;"/></p>

# Github Basics

- Github : host for git repositories

- `git clone <url>` : download git repository to local machine

- SSH keys : can connect github without identifying username and password

- `git remote -v` : display list of remotes

- `git remote add <name> <url>` : add a new remote

- `git remote rename <old-name> <new-name>` : rename remote

- `git remote remove <name>` : remove remote

- `git push <remote> <branch-name>` : push `<branch-name>` on local to `<branch-name>` on remote

- `git push <remote> <local-branch>:<remote-branch>` : push `<local-branch>` on local to `<remote-branch>` on remote

- `git push -u <remote> <branch-name>` : push and make `git push` = `git push <remote> <branch-name>` for next time usage

# Fetching & Pulling

- `git branch -r` : list all remote branches

- `git branch -vv` : list all local branches and their remote tracking branches

- `git checkout <remote>/<remote-branch>` : go to `<remote-branch>` on remote

- `git switch <remote-branch>` or `git checkout --track <remote>/<remote-branch>` : make branch `<local-branch>` = `<remote>/<remote-branch>` in the same branch name

```mermaid
flowchart LR
A(Working Directory) -->|git add| B(Staging Area)
B -->|git commit| C(Local Repository)
C -->|git push| D(Remote Repository)
D -->|git fetch| C
D -->|git pull| A
```

- `git fetch <remote>` : fetch all changes from the remote repository without merging to local working directory. this will **not create conflict**

<p align="center"><img src="./asset/08-git-fetch-pull.png" alt="drawing" style="width:400px;"/> <img src="./asset/09-git-fetch-pull.png" alt="drawing" style="width:400px;"/></p>

- `git pull <remote> <branch>` : `git fetch <remote>` + `git merge <branch>`

  - Good practice : `git pull` and fix merge conflict before `git push`
  - can result in **merge conflict**
  - not recommend if you have uncommitted changes!

- `git pull` : this will use default value as `git pull origin <tracking-current-branch>`

<p align="center"><img src="./asset/08-git-fetch-pull.png" alt="drawing" style="width:400px;"/> <img src="./asset/10-git-fetch-pull.png" alt="drawing" style="width:400px;"/></p>

# Github Odds & Ends
