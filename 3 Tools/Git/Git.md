# Git basics

A git repository is any directory with a `.git` directory within it.
The `.git` directory contains all the data used by Git, including commits, branch references, snapshots of the working tree etc.

Git saves the data as a series of snapshots. Every time a commit is created, all the data at the form of the commit is saved.

# SHA-1

All Git files (including commits) are referred to by their SHA-1 checksums. The SHA-1 hash value is generated from the data and metadata of a file. The SHA-1 is 160 bits (20 bytes) long and is typically rendered as a 40 digits long hexadecimal number, such as: `4878d2e218393781121da3d1b5a6fef2d98f0d40`.

# Git Areas

There are three Git areas:

1. The working tree / the working directory
2. The Index / the staging area
3. The local repository

>[!TIP] Files ignored by Git by their inclusion in the `.gitignore` file exist outside of these areas. They cannot be accessed by Git in any way, except of forcibly adding them to the index with the `-f, --force` flag on the `add` command.

## 1. The working tree (working directory)

The working tree contains all the actual non-Git files that can be accessed/modified. It is a checkout of a specific git commit, and it includes all the non-staged changes to the files.
If the working tree is exactly the same as the commit it checked out, it is considered _clean_.

Files in the working tree can be:
- untracked - no version of the file does exists in the HEAD (the checked out commit)
- tracked - a version of the file exists in the HEAD...
	- modified (...and it's data is different)
	- not modified (...and it's data is exactly the same)

All newly created files in the working tree are untracked.
Untracked and modified tracked files can be staged (added to the index - the staging area).

After a successful commit, that new commit is _checked out_, meaning that the files in the working tree are set to exactly match the files in that commit. This makes all the files in the working tree tracked and not modified. Such a state of the working tree is considered _clean_. 

>[!TIP] When using the `git status` command:
> all files that are in the index will be shown as <span style="color:green">green</span> and files that are in the working tree but not in the index as <span style="color:red">red</span>.

## 2. Index (Staging area)

The Index is the area containing all the files in their specific version that will be included in the next commit. 

After a successful commit, the Index is emptied.
When a file gets added to the Index, only that specific version of the file is added to the index. If a file from the index gets changed before the commit, the new version is considered _modified_ and has to be added to the index again. Otherwise, the previously indexed version will be included in the next commit. 

Files that can be added to the index from the working tree can be:
- modified (a version of the file exists either in the index or the HEAD, but it's data is different)
- untracked (no version of the file exists in the HEAD)
- deleted (a version of the file exists either in the index or the HEAD, but does not exist in the working tree)

>[!NOTE] The index 
> A file containing all the informations about the files, in their specific versions, that will be included in the next commit.

## 3. The local repository (the .git repository)

The local repository is contained within the `.git` folder. It contains all the data and metadata that exists in our repository, that is, all the pointers (local branches, remote-tracking branches and HEAD), all commits those pointers point to and their ancestors, and all the data those commits refer to.

>[!TIP]  Backwards movement between the areas:
> To move a file from the Index to the working tree (unstage it), use the command:
> `git restore --staged <filename>`. 
> To remove all files from the Index and reset the working tree to the HEAD, use the command:
> `git reset --hard`

# Git pointers

## Branches

A branch is a pointer to a single commit. 
A commit can have multiple branches pointing to it.

>[!INFO] The default branch is named _main_.

There are three types of branches:
1. **local branch** - branch in the local repository that can be moved (by creating a new commit, resetting, force moving it etc.). It is created by the user.
   All local branches are in the directory `.git/refs/heads`.
	-  **tracking branch** - a local branch that is set up to track an upstream branch
>
2. **remote-tracking/upstream branch** - branch in the local repository that cannot be moved. If HEAD is pointed at it, the the detached HEAD state is entered. 
   It acts as a copy of the remote branch it is tracking that gets updated via `fetch` and `remote update` commands. Its name takes the form of `<remote>/<branch>` (eg. `origin/main`). It is created by a `fetch` or a `remote update` command.
	All remote-tracking branches are in the directory `.git/refs/remotes/origin`.   
>
3. __remote branch__ - branch in the remote repository. Cannot be moved but can be updated via the `push` command from the local tracking branch. It is created remotely or by being pushed from a local branch. Only exists in the remote repository - its local mirror image is the remote-tracking branch.

>[!TIP] To see all the branches in the local repo, including the connections between the local tracking and remote-tracking branches, use the command `git branch -avv`.

>[!WARNING] The naming used for remote-tracking and remote branches can vary:
> - **remote-tracking branches** are sometimes referred to as _remote branches_
> - **remote branches** are sometimes referred to as _remote repository branches_ or _branches in the remote repository_

### Tracking branches

A local branch can be set up as a tracking branch via different commands, such as:
- by checking out a branch whose name matches one of the remote-tracking branches, eg. `git checkout mybranch` if there is a remote-tracking branch called `origin/mybranch`
- by using the `-u`/`--upstream` flag on a `push`, `fetch` or `pull` command

A tracking branch can perform:
- a `push` to directly update the remote branch (note that this command does not automatically update the remote-tracking branch!). 
	- `git push origin main`
- a `fetch`  to download all the data related to the remote branch from the remote repository and to update the remote-tracking branch to the state of its remote branch
	- `git fetch origin main`
- a `merge` to update itself to the state of the remote-tracking branch (also doable with similiar commands such as cherry-pick or rebase)
	- `git merge origin main`

>[!WARNING] The `pull` command first performs a `fetch` and then a `merge` command.

>[!NOTE]  The `git remote update` and `git fetch origin` commands:
> both download ALL the relevant data from the remote repo and update ALL the remote-tracking branches. They also create remote-tracking branches for ALL remote branches whose remote-tracking counterparts still do not exist.


## HEAD

HEAD is a pointer that points to a branch. 

The branch being pointed to by HEAD is the currently active branch. When HEAD changes which branch it points to (switching between branches), the commit the new active branch is pointing to gets checked out (the working tree is set to its contents).

When a new branch is created, it points to the same commit as the branch that HEAD was pointing to.

When a new commit is created, the current branch moves to point to the new commit. The HEAD follows, still pointing at the current branch.

>[!WARNING] The HEAD can also point to a commit, not a branch. This is called the  _detached HEAD state_.

### Moving HEAD

HEAD can be moved to point to a branch or a commit. This can be achieved by either a `switch` or a `checkout` command, followed by the name of the branch or the hash of the commit (note that the first 4 characters of the hash are enough!).

The standard usage is having HEAD point to a branch.
When HEAD point to a commit, it is in the _detached head state_.

#### Relative refs

Instead of using the name of a branch or the hash of a commit to specify where HEAD is moving to, a _relative ref_ can be used.
A relative ref specifies a commit in the history of a commit (an ancestor commit).

##### The caret symbol `^`

The caret symbol `^` means _one step back in history_ or _the first ancestor commit_.
For example, using `git checkout HEAD^` means _checkout the first ancestor (parent) commit of the commit that HEAD is pointing to_. `git checkout main^` means _checkout the first ancestor commit of the commit that main was pointing to_.
The caret symbol can be stacked, so `^^` would move to the second ancestor, `^^^` to the third ancestor etc.

>[!TIP] Relative refs for commits with two parents
> Some commits have two parents, as they got created by a merge.
> 
> By default, relative refs always move through the inheritance tree through the first parent. To specify the relative ref to a second parent of a commit, the caret symbol followed by the number of the parent is used, eg. `main^2` would mean _the second parent of the commit that main is pointing to_.


##### The tilde symbol `~`

The tilde `~` on its own is the same as a single caret `^` - _the first ancestor commit_.

A tilde can be followed by a number, denoting the number of ancestors to move upward. Eg. `git checkout main~3` would mean _move to the third ancestor of the commit that main is pointing to_.

>[!NOTE] The relative refs can be chained! Eg. `git checkout HEAD^2~3^` would mean _checkout the parent of the third ancestor of the second parent of HEAD _.


# Commits

A commit is a file containing a snapshot of the files in their specific versions. It is referred to by its SHA-1 hash.

All commits have parents (except the initial commit in a repository).
A commit that is simply created from another commit (via the `commit` command) has a single parent.
A commit that is the result of a merge has two parents.

## Merging

Merging is the act of creating a new commit as a combination of two already existing commits. The new commit can have data from both of its parent commits. If the parent commits contain one or more files that share the same name but have different contents, that creates a _merge conflict_. The conflicting files must be manually changed to specify which data should be kept and which discarded.

### Fast forwarding

Merging a commit that is a direct descendent of the commit that is being merged into never creates a _merge conflict_ and does not create a new commit - the pointer (HEAD and the branch HEAD points to) simply moves to point to the descendent commit. Such an action is called a `fast forward`.


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

# [[Git CLI Commands]]
![[Git CLI Commands]]