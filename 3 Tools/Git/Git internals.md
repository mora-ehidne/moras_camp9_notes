# Git objects

Git objects are Git files that contain some actual data and are not just pointers to data.

There are three types of Git objects:
1. Blobs
2. Trees
3. Commits

All Git objects are stored in the `.git/objects` directory. 
The file names of Git objects are their SHA-1 hash values.

>[!TIP] SHA-1 (Secure Hashing Algorithm 1) hashes
>
>All Git files (blobs, commits, branches etc.) are referred to by their SHA-1 checksums. 
>
>The SHA-1 hash value is generated from the data and metadata of a file. The SHA-1 is 160 bits (20 bytes) long and is typically rendered as a 40 digits long hexadecimal number, such as: `4878d2e218393781121da3d1b5a6fef2d98f0d40`.

## Blob

A blob holds data from a specific versions of a file. A file that got included in a commit and then modifed and included in a different commit will exist in Git as two unique blobs - the first version of the file and the second version of the file. Blobs contain no file names - only the actual content of a file.

## Tree

A tree is a list of objects that are referenced to with their SHA-1 hashes, types and file names. It acts as a directory containing references to other objects. (resembling a UNIX directory entry)
A tree can contain references to blobs and other trees.
A tree is essentially a snapshot of data at a certain point of time.

## Commit

A commit is a file containing a snapshot of the files in their specific versions (a tree object) and some additional data.

A commit object contains:
- references to parent commits
- a reference to a single tree object
- information about the author (commiter) - name and e-mail address
- date and time of commiting
- the commit message
. It is referred to by its SHA-1 hash.

All commits have parents (except the initial commit in a repository).
A commit that is simply created from another commit (via the `commit` command) has a single parent.
A commit that is the result of a merge has two parents.

### Commit methods

#### Merging

Merging is the act of creating a new commit as a combination of two already existing commits. The new commit can have data from both of its parent commits. If the parent commits contain one or more files that share the same name but have different contents, that creates a _merge conflict_. The conflicting files must be manually changed to specify which data should be kept and which discarded.

#### Fast forwarding

Merging a commit that is a direct descendent of the commit that is being merged into never creates a _merge conflict_ and does not create a new commit - the pointer (HEAD and the branch HEAD points to) simply moves to point to the descendent commit. Such an action is called a `fast forward`.

#### Rebasing

Rebasing is similiar to merging, as it creates a combination of two already existing commits. The difference is that rebasing does not create a new commit, it simply places the commit being rebased as the parent of the commit the rebasing is performed in. In other words, it simply places one commit in the history of the other, creating a clean, linear history.

Rebasing can be done using the `rebase` command or by specifying that the pull request should rebase instead of merging with the `-r` / `--rebase` flag.

#### Cherry-picking

In a way similiar to rebasing, cherry-picking simply places the selected commit into the history (ancestor tree) of the currently active branch.

# Git references (refs)

A git ref is simply a named pointer to a single commit.
A commit can have an unlimited number of refs pointing to it.

Git references files contain only two pieces of information:
1. a pointer to a commit 
2. name of the reference

All git reference files are stored within the directory `.git/refs`.

Types of refs:
1. heads (branches and the HEAD) - stored within `.git/refs/heads`
2. tags - stored within `.git/refs/tags`
3. remotes - stored within `.git/refs/remotes`

All Git commands that target a specific commit can also be used by specifying a ref, as a ref can always be resolved into a commit (eg. branch `main` pointing to the commit `a2af` resolves in commit `a2af`, HEAD pointing to `main` pointing to to the commit `55ha` resolves in commit `55ha` etc.)

>[!INFO] Unreachable objects / orphaned objects / loose objects / dangling objects
> All these terms refer to the same thing: objects (blobs, tree, commits) that no refs are pointing to and which are not ancestors of an object a ref is pointing to. Unreachable objects cannot be found through a ref or by following a commit inheritance tree upward from a ref.
> 
> Unreachable objects get deleted on _garbage collection_. Garbage collection can be invoked manually through the command `gc` and its child command `prune`, but is also run automatically after a `fetch`, `merge`, `rebase` and `commit` commands.
> 
> Note that the `gc` command runs the `prune` command, but also `repack`, `pack` and `rerere` commands, which also compress Git data in order to optimize storage usage.

## heads

### Branches

A branch is a movable reference to a single commit. Each time a new commit is created while HEAD is on a specific branch, the branch moves to point to the newly created commit.

>[!INFO] The default branch is named _main_.

There are three types of branches:
1. **local branch** - branch in the local repository that can be moved (by creating a new commit, resetting, force moving it etc.). It is created by the user.
   All local branches are in the directory `.git/refs/heads`.
	-  **tracking branch** - a local branch that is set up to track an upstream branch
>
2. **remote-tracking/upstream branch** - branch in the local repository that cannot be moved. If HEAD is pointed at it, the the detached HEAD state is entered. 
   It acts as a copy of the remote branch it is tracking that gets updated via `fetch`/`remote update` commands. Its name takes the form of `<remote>/<branch>` (eg. `origin/main`). It is created by a `fetch` or a `remote update` command.
	All remote-tracking branches are in the directory `.git/refs/remotes/<remote>`.   
>
3. __remote branch__ - branch in the remote repository. Cannot be moved but can be updated via the `push` command from the local tracking branch. It is created remotely or by being pushed from a local branch. Only exists in the remote repository - its local mirror image is the remote-tracking branch.

>[!TIP] To see all the branches in the local repo, including the connections between the local tracking and remote-tracking branches, use the command `git branch -avv`.

>[!WARNING] The naming used for remote-tracking and remote branches can vary:
> - **remote-tracking branches** are sometimes referred to as _remote branches_
> - **remote branches** are sometimes referred to as:
>   -  _remote repository branches_
>	- _branches in the remote repository_ 
>	- _branches on the remote_
>
> This makes the whole thing very confusing.
> In these notes, I will only use the namings _remote-tracking branches_ and _remote branches_.

#### Tracking branches

A local branch can be set up as a tracking branch via different commands, such as:
- by checking out a branch whose name matches one of the remote-tracking branches, eg. `git checkout myBranch` if there is a remote-tracking branch called `origin/myBranch`
- by checking out and creating a new branch explicitly set to track a specific remote-tracking branch, eg. `git checkout -b myBranch origin/someOtherBranch`
- by using the `-u`/`--upstream` flag on a `push`, `fetch`, `pull` or `branch` command

A tracking branch can perform:
- a `push` to update the remote-tracking and the remote branch (note that in some versions of GIt `push` does not automatically update the remote-tracking branch!). 
	- `git push origin main`
- a `fetch`  to download all the data related to the remote branch from the remote repository and to update the remote-tracking branch to the state of its remote branch
	- `git fetch origin main`
- a `merge` to update itself to the state of the remote-tracking branch (also doable with similiar commands such as cherry-pick or rebase)
	- `git merge origin main`

>[!WARNING] The `pull` command first performs a `fetch` and then a `merge` command.

>[!NOTE]  The `git remote update`, `git fetch` and `git pull` commands:
> download ALL the relevant data from the remote repo and update ALL the remote-tracking branches. They also create remote-tracking branches for ALL remote branches whose remote-tracking counterparts still do not exist.


### HEAD

HEAD is a symbolic reference (a reference to a reference) that usually points to a branch. 
There is only a single HEAD in a repository.

The branch being pointed to by HEAD is the currently active (checked out) branch. When HEAD changes which branch it points to (switching between branches), the commit the newly active branch is pointing to gets checked out (the working tree is set to its contents).

When a new branch is created, it points to the same commit as the branch that HEAD was pointing to.

When a new commit is created, the current branch moves to point to the new commit. The HEAD follows, still pointing at the current branch.

>[!WARNING] The HEAD can also point to a tag or a commit, not only a branch. This is called the  _detached HEAD state_.

#### Moving HEAD

HEAD can be moved to point to a branch, a tag or a commit. This can be achieved by either a `switch` or a `checkout` command, followed by the name of the branch or the hash of the commit (note that the first 4 characters of the hash are enough!).

The standard usage is having HEAD point to a branch.
When HEAD point to a tag or a commit, it is in the _detached head state_.

## Relative refs

Instead of using the name of a branch or the hash of a commit to specify where HEAD is moving to, a _relative ref_ can be used.
A relative ref specifies a commit in the history of a commit (an ancestor commit).

###### The caret symbol `^`

The caret symbol `^` means _one step back in history_ or _the first ancestor commit_.
For example, using `git checkout HEAD^` means _checkout the first ancestor (parent) commit of the commit that HEAD is pointing to_. `git checkout main^` means _checkout the first ancestor commit of the commit that main was pointing to_.
The caret symbol can be stacked, so `^^` would move to the second ancestor, `^^^` to the third ancestor etc.

>[!TIP] Relative refs for commits with two parents
> Some commits have two parents, as they got created by a merge.
> 
> By default, relative refs always move through the inheritance tree through the first parent. To specify the relative ref to a second parent of a commit, the caret symbol followed by the number of the parent is used, eg. `main^2` would mean _the second parent of the commit that main is pointing to_.

###### The tilde symbol `~`

The tilde `~` on its own is the same as a single caret `^` - _the first ancestor commit_.

A tilde can be followed by a number, denoting the number of ancestors to move upward. Eg. `git checkout main~3` would mean _move to the third ancestor of the commit that main is pointing to_.

>[!NOTE] The relative refs can be chained! Eg. `git checkout HEAD^2~3^` would mean _checkout the parent of the third ancestor of the second parent of HEAD _.

## Tags

A tag is similiar to a branch, except that it is not movable.
It serves to mark an important object or an important point in the code of the project, a milestone or a code version (eg. v0.1).

A tag can point to any Git object, not only a commit.

All tags stored within `.git/refs/tags`

>[!WARNING] Tags are actually considered Git objects instead of refs, even though they get saved within the `.git/refs` directory. Git is pretty horrible.

## remotes

Remotes are references to remote repositories. They represent the last known state of a remote repo.

A local repository can connect to the remote repository through a remote.
The default remote name is `origin`.

Remotes are read-only, and HEAD can never point to a remote.