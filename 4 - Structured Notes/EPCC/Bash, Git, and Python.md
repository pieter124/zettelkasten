2025-06-16 

Tags:  [[programming]]

# **Bash, Git, and Python** 

A shell is a REPL, Read Evaluate Print Loop.
Computer file system hierarchically organised.

**Bash Commands**
cd : Navigate through directory(es).
pwd : Gives current directory.
mkdir : Makes an empty directory.
ls : Lists all files/directories inside current working directory.
wget : Use to download files from a URL.
CTRL + R (Reverse Search) : Gets the first matched previously inputted command.
history : Displays history of commands in shell lifetime.
head -n : Displays first n lines of the file.
less : Can display lines through a file which you can navigate via arrow keys.
export PS1= "$ " : Modify the shell environment variable to display differently at the start of a new line.
echo $HOME : Prints to the shell the value of the environment variable HOME.
man ls : Shows the manual of the ls command.
tldr ls : Explains what the ls command does.
touch x.txt : Creates an empty file named x.txt. Can also be used to update the timestamp of a file.
rm : Remove. Dangerous. Stay Cautious.
ls p* : The asterisk is the wildcard symbol (means all) which matches any file starting with the previous string before the asterisk.
| : The pipe symbol. Can be used to chain commands. The output of the previous command is the input of the next, separated by the pipe symbol.
grep : Helps you search specific text within files.
echo $? : Prints the special value to see if the previous command executed correctly.
wc -l *.pdb > numLines.txt : Adds the line count of all files ending .pdb to numLines.txt.
wc -l .pdb >> numLines.txt : Appends the line count of all files ending .pdb to numLines.txt.
cut -d , -f 2 : Cutting out sections using the delimiter (-d) ',' and uses the 2nd field.
"#!/bin/bash" indicates the file can be read by bash.
diff : Check the difference between text files.


**Git**
```
// This sets your username for git.
git config --global user.name "Username" 

// This sets your user email for git
git config --global user.email "youremail@provider.ending"

// Changes default repo name from master to main
git config --global init.defaultBranch main

// 


```


**Key Ideas:**
Bash is a powerful shell scripting language that allows the users to perform a number of operations.
Git is a stupid content tracker. Used to manage the history/changes to a directory/repository.

**References**
*EPCC HPC Summer School*
**Lecturers: Chris Wood, Evgenij Belikov**