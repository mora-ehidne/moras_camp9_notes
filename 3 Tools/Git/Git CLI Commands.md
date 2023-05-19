
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
* `-help` - shows help for the command

## Git areas commands
- `git status` - shows the active branch, its difference to its remote-tracking branch, its index and working tree

* `git add 'filename'` - tracks and stages the specified directories or files
* -  `git add .`  - tracks and stages all directories and files

- `git commit` - creates a new local commit. Opens the default text editor (eg. Vim) to write the commit message (note: commit messages have a header of max 50 symbols followed by a body, separated by an empty line)
* -  `-a`,`--all` - stages all currently tracked files before commiting
* - `--ammend` - edit the last commit by including the current Index and editing the commit message
- `git restore <location> <filename>` - restores a tracked file to its version in the HEAD
- - `location` can be:
- - - `-S`, `--staged` - unstages the file: removes it from the index, but leaves it in the worktree
- - - `-W`, `--worktree` - default location - restore a file in the working tree, but leaves its version in the Index
- - Note that the location can be also be both, so the file is removed from the Index and restored in the working tree!
* `git rm <filename>`  - removes a tracked, unmodified file from the working tree and index
	- `-f`, `--force`- removes a tracked file from index and working tree, regardless if it's modified or not
	- `--cached` - removes a file from Index, the file stays untracked in the working tree
- `git reset <mode> <commit>` - sets HEAD and the current branch to the given commit. `<commit>` can be any ref, including relative refs, such as `git reset --hard HEAD~2`
	- `<mode>` can be:
	- - `--mixed` - default mode - clears the index, leaves the working tree untouched 
	- - `--soft` - leaves both index and the working tree untouched
	- - `--hard` - clears both the index and the working tree, all changes are discarded

## Branch commands

* `git branch` - shows all the local branches and highlights the current one (the one that HEAD points to)
 * * `-r` - shows all the remote-tracking branches 
 * * `-a`, `--all` - shows all local and remote-tracking branches
 * * `-v`,  `--verbose` - shows the SHA1s, header of the the last commit messages and difference to the remote-tracking branch
 * * `-vv`,  `--verbose --verbose` - same as `-v` but includes tracking reference for the local tracking branches
 * * `--merged` - shows only the branches merged into the current branch or the branch specified by name
 * * `--no-merged` - shows only the branches not merged into the current branch or the branch specified by name
 * * `git branch <branchName>` - creates a new local branch from the current branch
 * * * `-d`, `--delete` - deletes the specified branch 
* * * `-D`, `--delete --force`- deletes the specified branch, regardless of its merge status
 * * * `-m` - rename the branch
- `git switch 'branch name'` - switches to the specified local branch
- - `-c`, `--create` - creates the new branch before switching to it
*  `git checkout 'branch name'` - switches to the specified local branch. If no local branch with such a name exist, but a remote branch with the same name exists, creates a new tracking branch and switches to it
* - `-b` - creates the new branch before switching to it
* - `-f`, `--force` - switches even if there are uncommited changes in the index or the working tree. The uncommited changes get discarded.
* - `-t`, `--track` - sets the remote tracking reference
- `git prune` - deletes all unreachable local references
-  - `-n`, `--dry-run` - only displays which refs would be deleted, without actually deleting anything

* `git log` - shows the commit history for the active branch, starting with the latest one (reverse chronological order). Navigate with `arrow up` and `arrow down`. `q` to quit.
* - `-p, --patch` - shows the differences introduced by each commit
* - `--stat` - shows an abbreviated stat of the differences introduced by each commit
* - `--no-merges` - excludes all merge commits

## Remote communication commands

- `git push <remote> <branchname>` - pushes the local branch into the remote branch (eg. `git push origin main`) 
* - `git push` - pushes the tracking branch into its tracked remote branch
* - `-u`, `--set-upstream` -  also adds the tracking reference to the local branch 
* - `-d`,`--delete` - deletes the remote branch from the remote repository

- `git remote update` - downloads all data and refs from the remote, creating remote-tracking branches if necessary. Same as `git fetch`.

- `git fetch 'remote' 'branchname'` - updates the specified remote-tracking branch to the state of the remote branch
- `--set-upstream` - also adds the tracking reference to the branch
- - `git fetch` - updates all remote-tracking branches from the remote 
* `git pull 'remote' 'branchname'` - does both `fetch` and `merge`: updates the remote-tracking branch, then merges it into the current local branch
* - `git pull` - pulls from the remote branch that tracking reference is set to
* - - `-r`, `--rebase` - perform a rebase instead of a merge

>[!TIP] Colon refspecs
> `push`, `fetch` and `pull` commands can also receive arguments in the form of colon refspecs - source and destination branch separated by a colon. 
> 
> The syntax looks like this: `git push <remote> <source>:<destination>` - pushes the source branch into the destination branch on the given remote (eg. `git push origin main:main`).
> 
> If the source for a `push` command is empty, the destination branch will be deleted.
> If the source for a `fetch` or `pull` command is empty, a new local branch will be created as the destination branch.


## Remote commands

* `git clone 'SSH depository code'` - creates a local clone of the online repo
- `git remote` - shows a list of all the remotes (usually just one, _origin_)
	- `-v, --verbose` - includes the full URL of the remotes

* `git remote show <remote>` - shows details for the specified remote repository, including:
	1. the URLs for fetching/pushing
	2. the name of it's HEAD branch (`main` by default)
	3. all its remote branches and if a corresponding remote-tracking branch exist
	4. the tracking references for local tracking branches
- `git remote add 'remote' 'remote-url'` - adds a remote repository reference from a remote server, eg `git remote add origin git@github.com:devhausleipzigacademy/camp9-midterm.git`
* `git remote remove <remote>` - removes the specified remote repository reference
-  `git remote prune origin` - deletes all remote-tracking branches whose remote branches  no longer exist
- - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything



