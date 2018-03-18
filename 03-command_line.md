# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

1. pwd-shows current working directory path
2. mkdir-creates a new directory
3. rm -r-deletes a directory and all it's child directories
4. touch-creates a new file
5. cp(1starg, 2ndarg)-copies files and directories from one directory to another
6. cd-changes working directory
7. ls -a-lists hidden files
8. * -selects all files in current directory
9. mv-move a file into a directory or renames a file
10. rm-deletes a file


---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

1. ls-lists all the files in the current directory
2. ls -a-lists hidden files
3. ls -l-lists all files in long format
4. ls -lh-lists files in long format with byte sizes
5. ls -lah-lists all files(including hidden files) in long format with byte sizes
6. ls -t-lists files in order of when they were last modified
7. ls -Glp-lists files with group ID number in long format and puts "/" after directory name

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

1. ls -a
2. ls -m
3. ls -C
4. ls -q
5. ls -R

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

xargs runs a command by taking the text you type afterwards as an arguement. For example, running xargs touch and then typing bob new cat will create three files called bob, new, and cat.

 

