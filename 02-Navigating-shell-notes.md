# 02-Navigating-shell-notes

## Navigating the shell

* We will begin with the basics of navigating the Unix shell.

* Let’s start by opening the shell. - start Gitbash on Win.

* This likely results in seeing a black window with a cursor flashing next to a dollar sign. 

* This is our command line, and the `$` is the command prompt to show that the system is ready for our input.
*  The appearance of the prompt will vary from system to system, depending on how the set up has been configured, but it usually ends with a `$`.

* When working in the shell, you are always somewhere in the computer’s file system, in some folder (directory).

**show/epxplain folder hierarchy use image http://swcarpentry.github.io/shell-novice/fig/filesystem-challenge.svg**

*  We will therefore start by finding out where we are by using the `pwd` command, which you can use whenever you are unsure about where you are. 
*  It stands for **“print working directory”** and the result of the command is printed to your standard output, which is the screen.

* Let’s type `pwd` and hit enter to execute the command: (The `$` sign is used to indicate a command to be typed on the command prompt, but we never type the `$` sign itself, just what follows after it.)

```
$ pwd
```

* The output will be a path to your home directory. 
* Let’s check if we recognise it by listing the contents of the directory. To do that, we use the ls command:
```
$ ls
```
* We may want more information than just a list of files and directories. We can get this by specifying various **flags** (also known as options, parameters, or, most frequently, arguments) to go with our basic commands. 
* Arguments modify the workings of the command by telling the computer what sort of output or manipulation we want.

* If we type `ls -l` and hit enter, the computer returns a list of files that contains information similar to what we would find in our **Finder (Mac) or Explorer (Windows): the size of the files in bytes, the date it was created or last modified, and the file name.**
```
$ ls -l
```
* In everyday usage we are more used to units of measurement like kilobytes, megabytes, and gigabytes. 
* there’s another flag `-h` that when used with the `-l` option, use **unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte** in order to reduce the number of digits to three or less using base 2 for sizes.

* Now `ls -h` won’t work on its own. When we want to combine two flags, we can just run them together.
* typing `ls -lh` and hitting enter we receive an output in a human-readable format (note: the order here doesn’t matter).
```
$ ls -lh
```
* We’ve now spent a great deal of time in our home directory. 
* Let’s go somewhere else. 
* We can do that through the `cd` or **Change Directory** command: (Note: On Windows and Mac, by default, the case of the file/directory doesn’t matter On Linux it does.)
```
$ cd Desktop
```
* Notice that the command didn’t output anything. This means that it was carried out successfully. 
* Let’s check by using `pwd`:
```
$ pwd
```
* If something had gone wrong, however, the command would have told you. 
* Let’s test that by trying to move into a non-existentdirectory:
```
$ cd "Evil plan to destroy the world"
```

* Notice that we surrounded the name by quotation marks. 
* The arguments given to any shell command are separated by spaces, so a way to let them know that we mean ‘one single thing called “Evil plan to destroy the world”’, not ‘six different things’, is to use (single or double) quotation marks.

* We’ve now seen how we can go ‘down’ through our directory structure (as in into more nested directories).
* If we want to go back, we can type `cd ..`. 
* This moves us ‘up’ one directory, putting us back where we started. 
* If we ever get completely lost, the command `cd` without any arguments will bring us right back to the home directory.

### Tip
* switching back to a previous directory
* To switch back and forth between two directories use 
```
cd -
```
* Being able to navigate the file system is very important for using the Unix shell effectively. As we become more comfortable, we can get very quickly to the directory that we want.

* Show `man` command and explain help


## Exercise 1:
* Do Try exploring:
    * Move around the computer, get used to moving in and out of directories, see how different file types appear in the Unix shell. Be sure to use the `pwd` and `cd` commands, and the different flags for the `ls` command you learned so far.

If you run Windows, also try typing `explorer .` to open Explorer for the current directory (the single dot means “current directory”). If you’re on a Mac, try `open .` and for Linux try `xdg-open` . to open their graphical file manager.

* Do Find out about advanced ls commands
https://librarycarpentry.github.io/lc-shell/02-navigating-the-filesystem/index.html










































