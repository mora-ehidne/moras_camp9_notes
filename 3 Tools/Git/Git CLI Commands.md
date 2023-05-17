
>[!INFO] All Git CLI commands are called **within the working directory**
^4995f4

## General commands

* `git config` - shows the configuration options, used with flags to set up local, global (user) and system configuration
* * `--list` - lists all the active config settings (including the local, global and system configs, use additional flags to only list specific settings)
* * `--local` - use the local config file
* * `--global` - use the global config file
* * `--system` - use the system config file
* * `--show-origin` - used with `--list` to include the paths of the config files
* * `git config user.name` - shows the value of the key *user.name*
* * `git config --global user.name "New Name"` - changes the global username to *New Name*
* * `git config --global user.email me@mysite.com` - changes the global email to `me@mysite.com`
* `git init` - sets the working directory up as a Git repo. Creates a `.git` directory within the working directory.
* `git status` - shows the active branch, its difference to the remote tracked one, its index, and the tracked files in the working tree
* `-help` - shows help for the command
* `git log` - shows the history of all commits for the active branch, starting with the latest ones. Navigate with `arrow up` and `arrow down`. `q` to quit.

## Updating commands

* `git add 'filename'` - tracks and stages the specified directories or files
* -  `git add .`  - tracks and stages all directories and files

- `git commit` - creates a new local commit. Opens the default text editor (eg. Vim) to write the commit message (note: commit messages have a header of max 50 symbols followed by a body, separated by an empty line)
* -  `-a`,`--all` - stages all currently tracked files before commiting
* - `-m`, `--message=` - adds the commit message specified. If used, the default text editor will not be opened.

- `git push 'remote' 'branchname'` - pushes the local branch into the remote branch by specifying its remote-tracking branch (eg. `git push origin main`) (does not update the remote-tracking branch)
* - `git push` - pushes the tracking branch into its tracked remote branch (does not update the remote-tracking branch)
* - `-u`, `--set-upstream` -  also adds the tracking reference to the local branch 
* - `-d`,`--delete` - deletes the remote branch from the remote repository

- `git fetch 'remote' 'branchname'` - updates the specified remote-tracking branch to the state of the remote branch
- `--set-upstream` - also adds the tracking reference to the branch
- - `git fetch` - updates the remote-tracking branch the current branch is tracking 
* `git pull 'remote' 'branchname'` - does both `fetch` and `merge`: updates the remote-tracking branch, then merges it into the current local branch
* - `git pull` - pulls from the remote branch that tracking reference is set to
- `git rm <filename>`  - removes the file from the working tree and the index
	- `--cache` - unstages and untracks the file without removing the file from the working tree

## Branching commands

* `git branch` - shows all the local branches and highlights the current one (the one that HEAD points to)
 * * `-r` - shows all the remote branches 
 * * `-a`, `--all` - shows all local and remote branches
 * * `-v`,  `--verbose` - shows the SHA1 and message for the last commit on each branch
 * * `-vv`,  `--verbose --verbose` - same as `-v` but includes the remote-tracking branches for the local tracking branches
 * * `--merged` - shows only the branches merged into the current branch or the branch specified by name
 * * `--no-merged` - shows only the branches not merged into the current branch or the branch specified by name
* * `-d`, `--delete` - deletes the specified branch
* * `-D`, `--delete --force`- deletes the specified branch, regardless of its merge status
 * * `-m` - rename the branch
 * * `git branch 'branchname'` - creates a new local branch from the current branch
- `git switch 'branch name'` - switches to the specified local branch
- - `-c`, `--create` - creates the new branch before switching to it
*  `git checkout 'branch name'` - switches to the specified local branch. If no local branch with such a name exist, but a remote branch with the same name exists, creates a new tracking branch and switches to it
* - `-b` - creates the new branch before switching to it
* - `-f`, `--force` - switches even if there are uncommited changes in the index or the working tree. The uncommited changes get discarded.
* - `-t`, `--track` - sets the remote tracking reference

## Remote commands

* `git clone 'SSH depository code'` - creates a local clone of the online repo
- `git remote` - shows a list of all the remotes (usually just one, _origin_)
	- `-v, --verbose` - includes the full URL of the remotes
- `git remote add 'remote' 'remote-url'` - adds a remote repository reference from a remote server, eg `git remote add origin git@github.com:devhausleipzigacademy/camp9-midterm.git`

* `git remote update` - downloads all remote branches and all of their commits and data
-  `git remote prune origin` - deletes all remote branches which no longer exist on the remote server
- - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

## Pruning (removing *stale* references)

* `git prune` - deletes all unreachable local references
* * - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

