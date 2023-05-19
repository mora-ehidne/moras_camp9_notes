# Git basics

A git repository is any directory with a `.git` directory within it.
The `.git` directory contains all the data used by Git, including blobs, commits, branch references, snapshots of the working tree etc.

Git saves the data as a series of snapshots. Every time a commit is created, all the data at the form of the commit is saved.

# [[Git internals]]
## [[Git internals#Git objects|Git objects]]
![[Git internals#Git objects]]

## [[Git internals#Git references (refs)|Git refs]]
![[Git internals#Git references (refs)]]
# Git Areas

There are three Git areas:

1. The working tree / the worktree / the working directory
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
> `git restore --staged <filename>`
> to also untrack it, use:
> `git rm <filename> --cached`.
> To remove all files from the Index and reset the working tree to the HEAD, use the command:
> `git reset --hard`

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