# 04-counting-mining-shell-notes

## Counting and mining data
* Now that you know how to navigate the shell, we will move onto learning how to count and mine data using a few of the standard shell commands. 

* While these commands are unlikely to revolutionise your work by themselves, they’re very versatile and will add to your foundation for working in the shell and for learning to code. 
* The commands also replicate the sorts of uses library users might make of library data.

## Counting and sorting
* We will begin by counting the contents of files using the Unix shell. 
* We can use the Unix shell to quickly generate counts from across files, something that is tricky to achieve using the graphical user interfaces of standard office suites.

* Let’s start by navigating to the directory that contains our data using the `cd` command:
```
$ cd shell-lesson
```
* Remember, if at any time you are not sure where you are in your directory structure, use the `pwd` command to find out:
```
$ pwd
```
**make sure you are still in the shell-lesson directory**

* And let’s just check what files are in the directory and how large they are with `ls -lh`:
```
$ ls -lh
```
* lets focus on the dataset `2014-01_JA.tsv`, that contains journal article metadata, and the three `.tsv` files derived from the original dataset. 
* Each of these three `.tsv` files includes all data where a keyword such as africa or america appears in the **‘Title’ field** of `2014-01_JA.tsv`.

#### What are CSV and TSV files?
* `CSV (Comma-separated values)` is a common plain text format for storing tabular data, where each record occupies one line and the values are **separated by commas**. `TSV (Tab-separated values)` is just the same except that values are **separated by tabs** rather than commas. 
* Confusingly, CSV is sometimes used to refer to both CSV, TSV and variations of them. 
* The simplicity of the formats make them great for exchange and archival. 
* They are not bound to a specific program (unlike Excel files, say, there is no CSV program, just lots and lots of programs that support the format, including Excel by the way.), and you wouldn’t have any problems opening a 40 year old file today if you came across one.

#### Word count - WC

* `wc` is the “word count” command: it counts the number of lines, words, bytes and characters in files. 
* Since we love the wildcard operator, let’s run the command `wc *.tsv` to get counts for all the .tsv files in the current directory (it takes a little time to complete):
```
$ wc *.tsv
```
* The first three columns contains the **number of lines, words and bytes (to show number characters you have to use a flag)**.

* If we only have a handful of files to compare, it might be faster or more convenient to just check with Microsoft Excel, OpenRefine or your favourite text editor, but when we have tens, hundreds or thousands of documents, **the Unix shell has a clear speed advantage.** 
* **The real power of the shell comes from being able to combine commands and automate tasks, though. We will touch upon this slightly.**

* For now, we’ll see how we can build a simple pipeline to find the shortest file in terms of number of lines. 
* We start by adding the `-l` flag to get only the number of lines, not the number of words and bytes:
```
$ wc -l *.tsv
```

* The `wc` command itself doesn’t have a flag to sort the output, but as we’ll see, we can combine three different shell commands to get what we want.

* we have the `wc -l *.tsv` command. 
* We will save the output from this command in a new file. 
* To do that, we redirect the output from the command to a file using the `‘greater than’ sign (>)`, like so:
```
$ wc -l *.tsv > lengths.txt
```

* There’s no output now since the output went into the file `lengths.txt`, but we can check that the output indeed ended up in the file using `cat` or `less` (or Notepad or any text editor).
```
$ cat lengths.txt
```
* Next, there is the `sort` command. 
* We’ll use the `-n` flag to specify that we want **numerical sorting**, not lexical sorting, we output the results into yet another file, and we use cat to check the results:
```
$ sort -n lengths.txt > sorted-lengths.txt
```
```
$ cat sorted-lengths.txt
```
* Finally we have our old friend `head`, that we can use to get the first line of the `sorted-lengths.txt`:
```
$ head -n 1 sorted-lengths.txt
```
* But we’re really just interested in the end result, not the intermediate results now stored in `lengths.txt` and `sorted-lengths.txt`. 
* What if we could send the results from the first command (`wc -l *.tsv`) directly to the next command (`sort -n`) and then the output from that command to `head -n 1`? 
* we can, using a concept called `pipes`. 
* On the command line, you make a `pipe` with the vertical bar character `|`. 
* Let’s try with one pipe first:
```
$ wc -l *.tsv | sort -n
```
* Notice that this is exactly the same output that ended up in our `sorted-lengths.txt` earlier. 
* Let’s add another pipe:
```
$ wc -l *.tsv | sort -n | head -n 1
```

* It can take some time to fully grasp pipes and use them efficiently, but it’s a very powerful concept that you will find not only in the shell, but also in most programming languages.

### Show pipes graphic
https://librarycarpentry.github.io/lc-shell/fig/redirects-and-pipes.png



### Exercises
https://librarycarpentry.github.io/lc-shell/05-counting-mining/index.html

#### 1 adding another pipe
#### 2 Count, sort and print (faded example)
#### 3 Counting number of files, part I
#### 4 Writing to files - use `date` command
---

## Mining and Searching

* Searching for something in one or more files is something we’ll often need to do, so let’s introduce a command for doing that: `grep` **(short for global regular expression print)**. 
* As the name suggests, it supports `regular expressions` and is therefore only limited by your imagination, the shape of your data, and - when working with thousands or millions of files - the processing power at your disposal.

* To begin using `grep`, first navigate to the shell-lesson directory if not already there. 
* Then create a new directory `“results”`:
```
$ mkdir results
```

* Now let’s try our first search:
```
$ grep 1999 *.tsv
``` 

* Remember that the shell will expand `*.tsv` to a list of all the .tsv files in the directory. 
* `grep` will then search these for instances of the string `“1999”` and print the matching lines.

#### Define - Strings
* A string is a sequence of characters, or **“a piece of text”**.

* Press the up arrow once in order to cycle back to your most recent action. 
* Amend/retype `grep 1999 *.tsv` to `grep -c 1999 *.tsv` and hit enter.
```
$ grep -c 1999 *.tsv
```

* The shell now prints the number of times the string 1999 appeared in each file. 
* If you look at the output from the previous command, this tends to refer to the **date field for each journal article**.

* We will try another search:
```
$ grep -c revolution *.tsv
```
* We got back the counts of the instances of the string revolution within the files. 
* Now, amend the above command to the below and observe how the output of each is different:
```
$ grep -ci revolution *.tsv
```

* This repeats the query, but prints a case insensitive count (including instances of both revolution and Revolution and other variants). 
* Note how the count has increased nearly 30 fold for those journal article titles that contain the keyword ‘america’. 
* As before, cycling back and adding `> results/`, followed by a filename (ideally in .txt format), will save the results to a data file.

* So far we have counted strings in file and printed to the shell or to file those counts. 
* But the real power of `grep` comes in that you can also use it to **create subsets of tabulated data (or indeed any data) from one or multiple files**.
```
$ grep -i revolution *.tsv
```

* This script looks in the defined files and prints any lines containing revolution (without regard to case) to the shell.
* We add today’s date to the filename using `ISO format of YYYY-MM-DD`.
```
$ grep -i revolution *.tsv > results/2016-07-19_JAi-revolution.tsv
```

* This saves the subsetted data to file.

* However, if we look at this file, it contains every instance of the string ‘revolution’ including as a single word and as part of other words such as ‘revolutionary’. 
* This perhaps isn’t as useful as we thought… Thankfully, the `-w` flag instructs `grep` to look for whole words only, giving us greater precision in our search.
```
$ grep -iw revolution *.tsv > results/2016-07-19_JAiw-revolution.tsv
```
* This script looks in both of the defined files and exports any lines containing the whole word revolution (without regard to case) to the specified `.tsv` file.

* We can show the difference between the files we created.
```
$ wc -l results/*.tsv
```
#### next section covers regEx not taught #### 

Finally, we’ll use the regular expression syntax covered earlier to search for similar words.

Basic and extended regular expressions
There is unfortunately both “basic” and “extended” regular expressions. This is a common cause of confusion, since most tutorials, including ours, teach extended regular expression, but grep uses basic by default. Unles you want to remember the details, make your life easy by always using extended regular expressions (-E flag) when doing something more complex than searching for a plain string.

The regular expression ‘fr[ae]nc[eh]’ will match “france”, “french”, but also “frence” and “franch”. It’s generally a good idea to enclose the expression in single quotation marks, since that ensures the shell sends it directly to grep without any processing (such as trying to expand the wildcard operator *).
```
$ grep -iwE 'fr[ae]nc[eh]' *.tsv
```
The shell will print out each matching line.

We include the -o flag to print only the matching part of the lines e.g. (handy for isolating/checking results):
```
$ grep -iwEo 'fr[ae]nc[eh]' *.tsv
```
#### Tip: Invalid option – o?
If you get an error message “invalid option – o” when running the above command, it means you use a version of grep that doesn’t support the -o flag. This is for instance the case with the version of grep that comes with Git Bash on Windows. Since the flag is not crucial to this lesson, please just relax and ignore the problem. If you really needed the flag, however, you could have installed another version of grep. The situation for Windows users also improves on Windows 10 with the new Bash on Windows.

## Exercises - grep
https://librarycarpentry.github.io/lc-shell/05-counting-mining/index.html

#### 1 Case sensitive search in select files
#### 2 Count words (case sensitive)
#### 3 Count words (case insensitive)
#### 4 Case insensitive search in select files and save to new file
#### 5 Case insensitive search in select files (whole word)









