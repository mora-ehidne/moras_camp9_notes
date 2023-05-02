For documentation, see [Linux terminal documentation](https://linuxcommand.org/lc3_man_page_index.php#text).

### general 

* `whoami` - prints the id of the current user (the id is also visible as the first part of the prompt)
* `ctrl + c` - terminates the running process
* `ctrl + r` - start reverse command history, hitting it again will go one step back in history
* `clear` - clears the current screen
* `du` - **disk usage** - print disk usage of a directory, if no directory path is given, shows disk usage of the working directory
* * `-h`, `---human-readable`- flag to print sizes in human readable format (e.g., 1K 234M 2G)
* `nano` - enters the *nano* text editor
* * `nano myfile.txt` - enters the *nano* text editor with *myfile.txt* open
* `echo` - prints the specified string on screen
* * `echo "hello!"` - prints *hello!* on the screen
* `history` - shows all the used commands in this session
* * `history 10` - shows the 10 last used commands in this session
* `>` - __redirect output, overwrite__ - instead of printing the output of a command on screen, writes it in a text file. If the output text file is nonexistent, creates the file. If the output text file exists and already has some content, that old content is overwritten.
* * `echo "hello!" > myfile.txt` - writes *hello!* into *myfile.txt* (prints nothing on screen)
* * `ls > myfile.txt` - writes the list command output into *myfile.txt* (prints nothing on 
*  `>>` - **redirect output, append** - same as the `>` command, but does not overwrite file content, instead appending the text output to the end of the text file
* * `echo "hello!" >> myfile.txt` - appends *hello!* into *myfile.txt*, creating *myfile.txt* if nonexistent screen)
* `&&` - the chaining operator can be used to execute multiple commands


#### commands used before other commands

* `sudo` - **super user do** - used before a command to grant administrator privileges to the command 
* `man` - **manual** - used before a command to open the manual entry for that command
* * `man ls` - opens the manual entry for the command `ls`


### navigation

* `pwd` - **print working directory** - displays the full path of the working directory
* `ls` - **list** - prints all files and directories in the working directory
*  *  `-a`, `--all` - flag to include all hidden files and directories
*  * `-A`, `--almost-all` - flag to to include all hidden files and directories except `.` and `..`
* * `-l` - flag to use long listing format, lists in columns with additional information
* * `-o` - similiar to `-l`, but ommits group info
* `cd` - **change directory** - changes the working directory to the one specified
* * `cd ..` - moves one directory up
* * `cd ../..` - moves two directories up
* * `cd ~` or `cd`- changes to the base directory 
* * `cd /` - changes to the root directory
* * `cd directoryname` - changes to the directory name specified

>[!TIP] File paths starting with `/` are **absolute**, meaning they start from the root directory. All other file paths are **relative**, meaning they start from the working directory.
>

### file/directory creation & manipulation

>[!INFO] All navigation/manipulation/package manager commands are called **within the working directory**

* `mkdir` - **make directory** - creates a new directory with the specified name
* * `mkdir my-new-dir` - creates a new directory called *my-new-dir*
* * `-p` - creates all parent directories specified in the path
* `touch` - create a new file with the specified name
* * `touch new-file.txt` - creates a new file called *new-file.txt*
* `cp` - **copy** - creates a copy of a directory or file to the destination
* * `cp my-file.txt copy-my-file.txt` - creates a copy of *my-file.txt* named *copy-my-file.txt* (the destination is a file, thus it becomes the name of the new file)
* * `cp my-file.txt mydir` - creates a copy of *my-file.txt* in the directory *mydir* (the destination is a directory, thus the name of the copy stays the same)
* * `-r`, `R`, `--recursive` - flag to copy directories
* `mv` - **move** - moves the directory or file into a subdirectory
* * `mv mydir myotherdir` - moves the directory *mydir* into the directory *myotherdir*
* * `mv my-file.txt mydir` - moves the file *my-file.txt* into the directory *mydir*
* * `mv my-file.txt new-name-file.txt` - uses the **move** command to rename a file or a directory
* `rm` - **remove** - removes a file or directory
* * `rm myfile.text` - removes *myfile.txt*
* * `-d`, `--dir` - flag to remove an empty directory, same functionality as the `rmdir` command
* * `-r`, `R`, `--recursive` - flag to remove a non-empty directory
* * `-f`,  `--force` - forces the removal, skipping any prompts
* `cat` - **concatenate** - prints contents of a file to the screen
* * `cat myfile.txt` - prints all the contents of *myfile.txt* on the screen

### package managers
* `npm` - node package manager
* - `npm install` - downloads and installs packages with the specified name
* - `npm info` - prints the information on the specified package, regardless if it's installed or not
* - `npm run` - runs a command, eg. `npm run dev` runs the live server for Vite (running process)
* - `npm watch` - builds the Vite/Node.js project on each new file save (running process)
* - `npm build` - builds the Vite/Node.js project

* `npx` - command that sets up packages only in the temporary memory

* `pnpm` - package manager that sets up the node packages globally, with only references in the local project directory

### vim

docs: https://vim.rtorr.com/
- `vimtutor` - tutorial for vim
- `:w` - write (save) the file
- `:q` - quit the file (fails if any unsaved changes exist)
- `:q!`, `ZQ` - force quit with unsaved changes 
-  `:wq`, `:x`, `ZZ` - write (save) and quit
- `Esc` - exit insert mode



### Git commands
![[Git]]