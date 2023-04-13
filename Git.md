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
* `git clone 'SSH depository code'` - creates a local clone of the online repo

## Updating commands

* `git add 'filename'` - adds the specified directories or files into the staging area
* `git add .`  - adds all non-ignored directories and files from the current directory into the staging area

* `git commit -m 'commit message'` - commits to the local directory with the message as identifier
* `git commit -am 'commit message'` - adds and commits to the local directory with the message as identifier, note that it doesn't work on newly created files!

* `git push -u origin 'branchname'` - pushes the commited local repository upstream into the specified repository (in this case *origin*) into the specified branch (eg. *main*)
* `git pull` - updates the local branch to the status of the remote branch

## Branching commands

* `git branch` - shows all the local branches and highlights the one we are on
 * * `-r` - shows all the remote branches 
 * * `-a` - shows all local and remote branches

* `git branch 'branchname'` - creates a new branch with the name specified
* `git checkout 'branch name'` or `git switch 'branch name'` - switches to the specified branch
* `git checkout --track origin/my-branch-name` - adds the remote branch to the list of local branches
* `git remote update` + `git status` - shows if the local branch is up to date with the remote branch

### Deleting branches

* `git branch -d 'branchname'` - locally deletes the branch with the specified name
* `git branch -D 'branchname'` - locally deletes the branch with the specified name (regardless of content)
* `git push origin --delete 'branchname'` - deletes the branch with the specified name from the online repository
* `git prune -p` - removes deleted remote files from showing up in the remote branch display