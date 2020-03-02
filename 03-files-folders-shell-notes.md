# 03-files-folders-shell-notes


## Working with files and folders
* we can interact with files on the command line: we can read them, open them, run them, and even edit them. 
* there’s really no limit to what we can do in the shell, but even experienced shell users still switch to graphical user interfaces (GUIs) for many tasks, such as editing formatted text documents (Word or OpenOffice), browsing the web, editing images, etc. 
* But if we wanted to make the same crop on hundreds of images, say, the pages of a scanned book, then we could automate that cropping work by using shell commands.

* We will try a few basic ways to interact with files. 
* Let’s first move into the `shell-lesson directory` on your desktop.
```
$ cd
$ cd Desktop/shell-lesson
$ pwd
```
* we will create a new directory and move into it:
```
$ mkdir firstdir
$ cd firstdir
```
* Here we used the `mkdir` command (meaning ‘make directories’) to create a directory named `‘firstdir’`. 
* Then we moved into that directory using the cd command.

* There’s a trick to make things a bit quicker. 
* Let’s go up one directory.
```
$ cd ..
```
* Instead of typing `cd firstdir`, let’s try to type `cd f` and then hit the Tab key. 
* We notice that the shell completes the line to `cd firstdir/`

#### talk about auto-complete
* Hitting `tab` at any time within the shell will prompt it to attempt to auto-complete the line based on the files or sub-directories in the current directory. 
* Where two or more files have the same characters, the auto-complete will only fill up to the first point of difference, after which we can add more characters, and try using `tab` again. 
* Try using this method throughout today to see how it behaves (as it saves loads of time and effort!).

## Reading files - HEAD, TAIL, LESS
If you are in `firstdir`, use `cd ..` to get back to the shell-lesson directory.

Here there are copies of two public domain books downloaded from Project Gutenberg along with other files.
```
$ ls -lh
```
* The files `829-0.txt` and `33504-0.txt` holds the content of book #829 and #33504 on Project Gutenberg. 
* But we’ve forgot which books, so we try the cat command to read the text of the first file:
```
$ cat 829-0.txt
```
**The terminal window erupts and the whole book cascades by (it is printed to your terminal). Great, but we can’t really make any sense of that amount of text.**

#### Cancelling commands
* Unix shell, hit `Ctrl+C`


* Often we just want a quick glimpse of the first or the last part of a file to get an idea about what the file is about. 
* To let us do that, the Unix shell provides us with the commands `head` and `tail`.
```
$ head 829-0.txt
```

* This provides a view of the first ten lines, whereas `tail` 829-0.txt provides a perspective on the last ten lines:
```
$ tail 829-0.txt
```
* If ten lines is not enough (or too much), we would check `man head` to see if there exists an option to specify the number of lines to get (there is: `head -n 20` will print 20 lines).

* Another way to navigate files is to view the contents one screen at a time. 
* Type `less 829-0.txt` to see the first screen, `spacebar` to see the next screen and so on, then `q` to quit (return to the command prompt).
```
$ less 829-0.txt
```

* Like many other shell commands, the commands `cat, head, tail and less` can take any number of arguments (they can work with any number of files). 
* We will see how we can get the first lines of several files at once. 
* To save some typing, we introduce a very useful trick first.

#### Tip - Resusing commands - up arrow

* On a blank command prompt, hit the `up arrow key` and notice that the previous command you typed appears before your cursor. 
* We can continue pressing the `up arrow` to cycle through your previous commands. 
* The `down arrow` cycles back toward your most recent command. 
* This is another important labour-saving function and something we’ll use a lot.

* Hit the up arrow until you get to the `head 829-0.txt` command. 
* Add a space and then `33504-0.txt` (Remember your friend Tab? Type 3 followed by Tab to get 33504-0.txt), to produce the following command:
```
$ head 829-0.txt 33504-0.txt
```
* All good so far, but if we had lots of books, it would be tedious to enter all the filenames. 
* Luckily the shell supports `wildcards!` The `?` (matches exactly one character) and `*` (matches zero or more characters) are probably familiar from library search systems. 
* We can use the `*` wildcard to write the above head command in a more compact way:
```
$ head *.txt
```

#### Tip More on Wildcards - ?,*

* Wildcards are a feature of the shell and will therefore work with any command. 
* The shell will expand wildcards to a list of files and/or directories before the command is executed, and the command will never see the wildcards. 
* As an exception, if a wildcard expression does not match any file, Bash will pass the expression as a parameter to the command as it is. 
* For example typing `ls *.pdf` results in an error message that there is no file called `*.pdf`.

## Moving, copying and deleting files - MV, CP, RM
* We may also want to change the file name to something more descriptive. 
* We can move it to a new name by using the `mv or move command`, giving it the old name as the first argument and the new name as the second argument:
```
$ mv 829-0.txt gulliver.txt
```
* This is equivalent to the `‘rename file’` function.

* Afterwards, when we perform a `ls` command, we will see that it is now called `gulliver.txt`:
```
$ ls
```
* Finally, onto deleting. We won’t use it now, but if you do want to delete a file, for whatever reason, the command is rm, or remove.

* Using wildcards, we can even delete lots of files. 
* adding the `-r` flag we can delete folders with all their content.

* Unlike deleting from within our graphical user interface, **there is no warning, no recycling bin from which you can get the files back and no other undo options!**
* **For that reason, please be very careful with `rm` and extremely careful with `rm -r`.**


---
## Exercises - 
#### 1 Copy a file
#### 2 renamining a directory
#### 3 moving a file into a directory

https://librarycarpentry.github.io/lc-shell/03-working-with-files-and-folders/index.html

























