# Git configuration

Git configuration defines such settings such as the user name and email, name of the main branch, remote repo for the current repository, etc.

Git settings are saved in three different configuration files:
- __local __(for the repository)
- __global__ (for the user, applies to all repositories)
- __system__ (for the device, applies to all users and repositories)

If the same setting (*key*) is defined in more than one configuration file, the most specific configuration file will overwrite other configurations (__local__ overwrites __global__ overwrites __system__).

On my MacBook, the paths for the configuration files are:
 - __local__: .git/config
 - __global__: /Users/mora/.gitconfig (~/.gitconfig)
 - __system__: /Library/Developer/CommandLineTools/usr/share/git-core/gitconfig

# SSH key caching

I cached the SSH key for GitHub on Mac by using the following commands:

```bash
eval $(ssh-agent)
```

```bash
ssh-add --apple-use-keychain 
```

I am no longer prompted to enter the SSH key.

# Git commands

>[!INFO] All Git commands are called **within the working directory**
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
* `git status` - shows the current branch, its status and the status of the items in it
* `-help` - shows help for the command
* `git log` - shows the history of all commits

## Updating commands

* `git add 'filename'` - adds the specified directories or files into the staging area, tracking the files if they are untracked
* -  `git add .`  - stages all non-ignored directories and files in the current directory

* `git commit -m 'commit message'` - commits to the local directory with the message as identifier
* -  `-a`,`--all` - stages all currently tracked files before commiting

* `git push 'remote' 'branchname'` - pushes the current local branch into the specified branch (eg. *main*) in the remote repo (eg *origin*)
* - `git push` - pushes the current local branch into the default remote repo
* - `-u`, `--set-upstream` - saves the specified remote repo as the default remote repo
* - `-d`,`--delete` - deletes the specified branch from the remote server

- `git fetch 'remote' 'branchname'` - downloads the specified remote branch and all of its commits and data
- - `git fetch` - fetches the remote branch the current branch is tracking 
* `git pull 'remote' 'branchname'` - downloads the specified remote branch and all of its commits and data, then merges it into the current local branch
* - `git pull` - pulls from the remote branch the current branch is tracking
- `git rm <filename>`  - removes the file from the working tree and the index
	- `--cache` - unstages and untracks the file without removing the file from the working tree

## Branching commands

* `git branch` - shows all the local branches and highlights the current one (the one that HEAD points to)
 * * `-r` - shows all the remote branches 
 * * `-a`, `--all` - shows all local and remote branches
 * * `-v`,  `--verbose` - shows the SHA1 and message for the last commit on each branch
 * * `-vv`,  `--verbose --verbose` - same as `-v` but includes the remote branches for the local tracking branches
 * * `--merged` - shows only the branches merged into the current branch or the branch specified by name
 * * `--no-merged` - shows only the branches not merged into the current branch or the branch specified by name
* * `-d`, `--delete` - deletes the specified branch
* * `-D`, `--delete --force`- deletes the specified branch, regardless of its merge status
 * * `-m` - rename the branch
 * * `git branch 'branchname'` - creates a new local branch from the current branch
- `git switch 'branch name'` - switches to the specified local branch
- - `-c`, `--create` - creates the new branch before switching to it
*  `git checkout 'branch name'` - switches to the specified local branch, if the branch does not exist but a remote branch with the same name exists, creates a new tracking branch before switching to it
* - `-b` - creates the new branch before switching to it
* - `git checkout --track origin/my-branch-name` - adds the remote branch to the list of local branches

## Remote commands

* `git clone 'SSH depository code'` - creates a local clone of the online repo
- `git remote add 'remote' 'remote-url'` - adds a remote repository reference from a remote server, eg `git remote add origin git@github.com:devhausleipzigacademy/camp9-midterm.git`
- `git remote update` - downloads all remote branches and all of their commits and data
-  `git remote prune origin` - deletes all remote branches which no longer exist on the remote server
- - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

## Pruning (removing *stale* references)

* `git prune` - deletes all unreachable local references
* * - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

