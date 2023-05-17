# Git basics

A git repository is any directory with a `.git` directory within it.
The `.git` directory contains all the data used by Git, including commits, branch references, snapshots of the working tree etc.

Git saves the data as a series of snapshots. Every time a commit is created, all the data at the form of the commit is saved.

All Git files (including commits) are referred to by their SHA-1 checksums.

## Git Areas

There are three Git areas:

1. The working tree / the working directory
2. The Index / the staging area
3. The local repository

>[!TIP] Files ignored by Git by their inclusion in the `.gitignore` file exist outside of these areas. They cannot be accessed by Git in any way, except of forcibly adding them to the index with the `-f, --force` flag on the `add` command.

### The working tree (working directory)

The working tree contains all the actual non-Git files that can be accessed/modified. It is a checkout of a specific git commit, and it includes all the non-staged changes to the files.
If the working tree is exactly the same as the commit it checked out, it is considered _clean_.

Files in the working tree can be:
- untracked (no file with that name exists in the checked out commit)
- tracked (a file with that name exists in the checked out commit)
	- modified (and it's contents are different)
	- not modified (and it's contents are exactly the same)

All newly created files in the working tree are untracked.
Untracked and modified tracked files can be staged (added to the index - the staging area).

After a successful commit, that new commit is _checked out_, meaning that the files in the working tree are set to exactly match the files in that commit. This makes all the files in the working tree tracked and not modified. Such a state of the working tree is considered _clean_. 

>[!TIP] When using the `git status` command:
> all files that are in the index will be shown as <span style="color:green">green</span> and files that are in the working tree but not in the index as <span style="color:red">red</span>.

### Index (Staging area)

The Index is the area containing all the files in their specific version that will be included in the next commit. 

After a successful commit, the Index is emptied.
When a file gets added to the Index, only that specific version of the file is added to the index. If a file from the index get changed before the commit, the new version is considered _modified_ and has to be added to the index again. Otherwise, the previously indexed version will be included in the next commit. 

Files that can be added to the index from the working tree can be:
- modified (a file with that name exists either in the index or the checked out commit, but it's contents are different)
- untracked (no file with that name exists in the checked out commit)
- deleted (a file with that name exists either in the index or the checked out commit, but does not exist in the working tree)

>[!NOTE] The index 
> A file containing all the informations about the files, in their specific versions, that will be included in the next commit.

### The local repository (the .git repository)

The local repository is contained within the `.git` folder. It contains all the data and metadata that exists in our repository, that is, all the pointers (local branches, remote branches and HEAD), all commits those pointers point to and its ancestors, and all the data of those commits.

>[!TIP]  Backwards movement between the areas:
> To move a file from the Index to the working tree (unstage it), use the command:
> `git restore --staged <filename>`. 

## Git pointers

### Branches

A branch is a pointer to a single commit. 
A commit can have multiple branches pointing to it.

>[!INFO] The default branch is named _main_.

There are three types of branches:
1. **local branch** - branch in the local repository that the local HEAD can point to and that can be moved (by creating a new commit, resetting etc.). It is created by the user.
	-  **tracking branch** - a local branch that is set up to track an upstream branch
>
2. **remote-tracking/upstream branch** - branch in the local repository that the HEAD cannot point to and that cannot be moved. It acts as a copy of the remote branch it is tracking that gets updated via `fetch` and `remote update` commands. Its name takes the form of `<remote>/<branch>` (eg. `origin/main`). It is created by a `fetch` or a `remote update` command.
>
3. __remote branch__ - branch in the remote repository. Cannot be moved but can be updated via the `push` command. It is created remotely or by being pushed from a local branch.

##### Tracking branch

A local branch can be set up as a tracking branch in different ways:
- via 

A tracking branch can perform:
- a `push` to directly update the remote branch (note that this command does not automatically update the remote-tracking branch too!). 
	- `git push origin main`
- a `fetch` to update the remote-tracking branch to the state of its remote branch
	- `git fetch origin main`
- a `merge` to update itself to the state of the remote-tracking branch
	- `git merge origin main`

>[!WARNING] The `pull` command does first a `fetch` to update the remote-tracking branch and then a `merge` to update the local branch.

>[!NOTE]  Both the `git remote update` and `git fetch origin` commands update ALL the remote-tracking branches and download all the remote commits, files and refs.


### HEAD

HEAD is a pointer that points to a branch. 

The branch being pointed to by HEAD is the currently active branch. When HEAD changes which branch it points to (switching between branches), the commit the new active branch is pointing to gets checked out (the working tree is set to its contents).

When a new branch is created, it points to the same commit as the branch that HEAD was pointing to.

When a new commit is created, the current branch moves to point to the new commit. The HEAD follows, still pointing at the current branch.

>[!WARNING] The HEAD can also point to a commit, not a branch. This is called the  _detached HEAD state_.


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
eval ssh-agent
```

```bash
ssh-add 
```

also tried:
``` bash
ssh-add --apple-use-keychain ~/.ssh/[your-private-key]
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
* `git init` - sets the working directory up as a Git repo. Creates a `.git` directory within the working directory.
* `git status` - shows the active branch, its difference to the remote tracked one, its index, and the tracked files in the working tree
* `-help` - shows help for the command
* `git log` - shows the history of all commits for the active branch, starting with the latest ones. Navigate with `arrow up` and `arrow down`. `q` to quit.

## Updating commands

* `git add 'filename'` - tracks and adds the specified directories or files into the staging area
* -  `git add .`  - tracks and stages all non-ignored directories and files in the current directory

- `git commit` - creates a new local commit. Opens the default text editor (eg. Vim) to write the commit message (note: commit messages have a header of max 50 symbols followed by a body, separated by an empty line)
* -  `-a`,`--all` - stages all currently tracked files before commiting
* - `-m`, `--message=` - adds the commit message specified. If used, the default text editor will not be opened.

- `git push 'remote' 'branchname'` - pushes the current local branch into the specified branch (eg. *main*) in the remote repo (eg *origin*)
* - `git push` - pushes the current local branch into the remote branch the current branch is tracking
* - `-u`, `--set-upstream` -  also adds the tracking reference to the branch 
* - `-d`,`--delete` - deletes the specified branch from the remote server

- `git fetch 'remote' 'branchname'` - downloads the specified remote branch and all of its commits and data
- `--set-upstream` - also adds the tracking reference to the branch
- - `git fetch` - fetches the remote branch the current branch is tracking 
* `git pull 'remote' 'branchname'` - does both `fetch` and `merge`: downloads the specified remote branch and all of its commits and data, then merges it into the current local branch
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
*  `git checkout 'branch name'` - switches to the specified local branch. If no local branch with such a name exist, but a remote branch with the same name exists, creates a new tracking branch and switches to it
* - `-b` - creates the new branch before switching to it
* - `-f`, `--force` - switches even if there are uncommited changes in the index or the working tree. The uncommited changes get discarded.
* - `-t`, `--track` - sets the remote tracking reference

## Remote commands

* `git clone 'SSH depository code'` - creates a local clone of the online repo
- `git remote add 'remote' 'remote-url'` - adds a remote repository reference from a remote server, eg `git remote add origin git@github.com:devhausleipzigacademy/camp9-midterm.git`

* `git remote update` - downloads all remote branches and all of their commits and data
-  `git remote prune origin` - deletes all remote branches which no longer exist on the remote server
- - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

## Pruning (removing *stale* references)

* `git prune` - deletes all unreachable local references
* * - `-n`, `--dry-run` - only displays which branches would be deleted, without actually deleting anything

