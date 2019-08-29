---
layout: article
titles:
  en      : &EN       UNIX tutorial
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-UNIX
---

This page outlines some more advanced uses of UNIX that are very useful for research.<br>

**NOTE:** this is not required for the course but are useful tools for general working within the unix environment.<br>

## Redirect output to file

If a command prints information to the screen (standard out) such as `cat`, `echo`, `ls`, `grep` etc. this output can instead be redirected to a file.<br>
The `>` symbol is used to overwrite the contents of the file with whatever output you specify to redirect to it.<br>
The `>>` is used to append instead of overwrite.<br>
Thus, to place the sentence “this is redirected output” into a file ‘redir.txt’ we type<br>
```console
echo “this is redirected output” >redir.txt
```
If we then want to add the contents of a file called ‘file1.txt’ to that file we type<br>
```console
cat file1.txt >>redir.txt
```
This is very useful for concatenating multiple files (e.g. sequence files) into one large file by using:<br>
```console
cat sequenceFile1.txt >>largeFile.txt
cat sequenceFile2.txt >>largeFile.txt
```
etc.<br>

## Tab completion

The tab button can be used to complete file/directory names and do quick lookup of commands.<br>
If, for example, a file or directory has a long name, you can save time by using tab completion.<br>
Lets say we wanted to copy a file named ‘reallyLongFilename.txt’ to the parent directory. We would use the command<br>
```console
cp reallyLongFilename.txt ..
```
Instead of having to type out the the whole filename, you can type the first few letters and hit the tab button. This will fill in the rest of the name for you, providing that the file is in the current directory and there is no other file/directory that starts with that name.<br>

To test this, create a file called reallyLongFilename.txt and use tab completion to fill out the name within a cat command.<br>
If there are two or more files that start the same way (for instance if you have a file reallyLongFilename.txt and a file realDataTest.txt) then tab completion after typing ‘rea’ will not fill in the whole name as there is ambiguity to which file you mean. In this instance pressing tab will fill in as much as it can (in this case ‘real’) and stop. Pressing the tab button twice will now display all the options of files that start with those letters, allowing you to see what extra letters you must type to complete the file.<br>
In this case you can type an extra l (giving you ‘reall’) and then hit tab and it will complete it for you.<br>

Create a file named ‘realDataTest.txt’ in the same folder as the ‘reallyLongFilename.txt’ file and try this double tap hinting completion method.<br>

Tab completion can be used on directories to show their contents as well. Say, for instance, you wish to copy a file to your Desktop folder but don’t know what else is in the folder. You start the command by typing<br>
```console
cp file1.txt ~/Desktop/
```
and then hit tab twice. This will then list the folder contents as per the `ls` command, and allow you to see what options are available to you for subdirectories etc.<br>
The same will work for commands such as `cd`, `less`, etc. and programs that are installed such as `raxml` and `migrate-n`.<br>

## Repeating commands using loops

The real power of the shell is the ability to repeat commands on multiple targets. This is useful for example for creating multiple folders, moving files into each folder, running pipeline on multiple samples etc.<br>
This is accomplished by using a tool called the for loop. In order to use these properly, two features of the shell need to be understood: variables and wildcards.

### Variable

A variable is a placeholder for some text such as a directory name, filename, number, sentence etc. These allow for the contents of the variable to be changed within a loop without manually having to do so yourself.<br>
A variable is always initialised using the name you designate for the variable (e.g. file, direc, superman, x, etc.) It can be whatever you want once it is a single word without spaces or special characters.<br>
The variable is then called using a ${} around the name. Thus is the variable is named direc it is referenced using ${direc}.

### Wildcards

The asterisk (\*) is referred to as a wildcard symbol in unix. This allows for matching of filenames, directories etc that all have a certain sections of their name in common.<br>
For example, if all your files start with ‘result’ (e.g. result.txt, result.tree, result.nexus, resultFile, result) these will all be recognised using result*.<br>
Alternatively if they all end with .txt you can loop over them all using the *.txt

Both variables and wildcards are used in for loops to maximise their power. A for loop has the syntax:
```console
for <variable> in <list>
do
<tasks to repeat for each item in list>
done
```
Each section is written on a separate line (e.g. after `do` hit enter’) and instead of a prompt the terminal will display a > to designate you are in a multi-line command.<br>
Alternatively you can place a loop all on one line using `;` to separate the commands (except for the line break after the `do` where there is no `;` included).

For example, we can use the command `echo` to print something to the screen. This is used like<br>
```console
echo hello
```
which will print hello to the terminal.<br>
We can use a for loop to print the number 1 to 10 to screen by typing
```console
for num in {1..10}
do
echo ${num}
done
```
This loop starts at 1, places the number in the variable num which can then be accessed inside the loop through `${num}`.<br>
(this can be done on one line by writing `for num in {1..10};do echo $num;done;` Note the lack of semi-colon after `do`)

This becomes more useful when we want to create, move, modify etc. files and directories.<br>
Lets use a for loop to create 3 directories which will be named run1, run2 and run3
```console
for num in {1..3}
do
mkdir 'run'${num}
done
```
We place `run` before the variable to tell the system we want this string to be placed before the variable as part of the directory name. If we wanted it placed after (e.g. create 1run etc.) we could use `${num}run`.

Loops can also be used to affect a set of folders or files that have some portion of their name in common.<br>
We can then use a loop to go into each run folder (created above) and create a blank file called ‘result.txt’ within the folder. This is done using `cd` commands to go in and out of directories in a list and the `touch` command to create blank files.<br>
This is done by the following loop:
```console
for direc in run*
do
cd ${direc}
touch result.txt
cd ..
done
```
This loop goes into each directory that starts with ‘run’, creates a file called ‘results.txt’, goes back out of the directory and then to the next in the list etc. Thus, the loop is stepping in (using `cd ${direc}`) and out (using `cd ..`) of each folder and issuing commands within the folders without you having to do so manually.<br>
**NOTE:** this loop will operate on every folder or file that starts with ‘run’. Thus if you happen to have a file that starts with ‘run’ in the same directory, the loop will attempt to step into this file, print an error saying it can’t but then continue the loop and create a file called ‘results.txt’ and `cd ..` meaning it goes into the directory above. Therefore you must be careful that if you are stepping in and out of folders with these loops there are no files that would be put into your list due to matching the text with the wildcard. The best way to test this is to create your loops that step in and out of folders and use pwd commands to check it is the right path at each step.

Loops are then most useful when running a pipeline on multiple samples. For example if you wish to run mafft and raxml on files contained in folders that start with ‘sample’ you could use a command such as
```console
for x in sample*
do
cd $x
mafft <put mafft command options here>
raxml <put raxml command options here>
cd ..
done
```
This will then run the programs on each sample in sequence, saving you from having to manually start these programs on every sample yourself.<br>
Anther use is to take all the .txt files in a directory and concatenate their contents into one large file using a for loop. Try this as an exercise.

## Grep

Grep is a tool for searching files for a specific content. It has many powerful applications, the basics of which will be explained here.
The basic syntax of grep is
```console
grep <search pattern> <filename>
```
For example if we want to find every line that contains the word ‘result’ in the file output.txt we should type
```console
grep “result” output.txt
```
This will print the lines to the screen (or you can redirect these to a file using the `>` or `>>` methods).

Flags can be used to modify these results in many useful ways. For example:
* `grep -n <search pattern> <filename>` will print the line number of the result beside each matching line
* `grep -v <search pattern> <filename>` will find the lines which don’t contain the search pattern
* `grep -c <search pattern> <filename>` does not return the lines that match but instead returns a count of the number of lines that contained a hit
* `grep -i <search pattern> <filename>` use a case insensitive match (meaning B and b are the same thing)
* `grep -A 5 <search pattern> <filename>` will print the 5 lines that come after a line that matches the pattern
* `grep -B 5 <search pattern> <filename>` will print the 5 lines that come before a line that matches the pattern
These can then be combined so that, for example, `grep -vc <search pattern> <filename>` will return a count of the lines that don’t contain the provided search pattern

Grep can also be used to search multiple files using wildcards as seen in the for loop.<br>
For example, to search for the pattern “result” (without worrying about case) in all files that end in .txt we could use
```console
grep -i “result” *.txt
```
You can display the filenames that match instead of the matching lines by using `-l`.<br>
Thus, to create a file that lists all the text files which contain the word “result” (case insensitive) you could use
```console
grep -il “result” *.txt >>found.txt
```
Grep can also be used with regular expression patterns, which allow for wildcards and other special characters to be used to match a variety of pattern combinations.<br>
For example, to find lines which have a b followed by any letter followed by a g (e.g. matching big, bog, etc.) we would write
```console
grep “b.g” file.txt
```
Here the `.` is used as a special character designating ‘any character’. If we want to look for the . specifically (e.g. b.g only) we have to ‘escape’ the . to tell grep we want to find the period, not the special function the period has. This is done with a `\.`<br>
Thus, to look for b.g only (and not big etc.) we type
```console
grep “b\.g” file.txt
```
If we want to find b followed by any number of characters and then a g we use the * symbol after the .. e.g.
```console
grep “b.*g” file.txt
```
which will find big, brig, berg, bloomberg etc.<br>
If we wanted to have only a selection of characters matched we can use the [] (square brackets).<br>
For instance, if we wanted to search for only big or bog we could use
```console
grep “b[io]g” file.txt
```
or if we wanted specific ranges, like only 1,2,3 after the word ‘result’ we could use
```console
grep “result[1-3]” file.txt
```
We can also specify if we want matches only at the start of the line using ^ or the end of the line using $.<br>
For example if we wanted a line that started with ‘Salmonella’ and ended with any number between 400 and 600 but we didn’t care about the character inbetween we could use
```console
grep “^Salmonella.*[400-600]$” file.txt
```
Thus you can see how grep and regular expressions are useful for searching large files for certain information like specific blast results in a tabular file, likelihood scores in phylogenetic analysis outputs etc.

## Sed

Another useful tool for file manipulation is sed. This tool has many powerful applications including the replacement of one block of text with another.<br>
The syntax for this is
```console
sed ‘s/<pattern to find>/<text to replace it with>/g’ <filename>
```
This will output the changed file contents to the screen, which can then be redirected to a new file using the `>` or `>>` as above. For example, if we wanted to replace every instance of the word ‘species’ with the abbreviation ‘sp’ in the file tax.txt and place it in a new file called newTax.txt we could use
```console
sed ‘s/species/sp/g’ tax.txt >newTax.txt
```
Remember: if a file is overwritten by a bad sed command there is no ‘undo’: the file is now permanently changed. Thus, use sed with caution and practise.<br>
Sed has many other powerful applications such as deletion of text and lines and regular expression pattern matching. These are very useful to learn but are to be used with caution.

## Pipe

The output from one unix command can be sent as input to another using a pipe. The symbol for this pipe is the vertical bar `|`.<br>
For example, lets say you have a directory that has lots of files and folders, making the `ls` command very full. If you want to search for a specific file prefix (lets say ‘result’) within the `ls` command we can pipe the output of `ls` to `grep` like so:
```console
ls| grep ‘result’
```
Note we do not specify anything as the input to `grep` since the pipe takes the output of `ls` and automatically puts it as the input to `grep`.<br>
Piping commands together as input to grep, sed, less, etc can become very useful for sorting, modifying and searching files and folders, especially within loops.

## .bash_profile, alias and PATH

### .bash_profile
The behaviour of the terminal shell can be modified by adding commands to one of two hidden files: .bashrc and .bash_profile, which are found in the home directory (/home/ubuntu on the Amazon instance). In the Mac OSX terminal these files do the same thing. In the Linux version the .bashrc runs each time a terminal window is opened whereas .bash_profile only runs the first time a terminal is opened.<br>
Here we will learn how to modify and use the .bash_profile file as the .bashrc is already populated with many commands we do not wish to interfere with.<br>
The two main things we will use the .bash_profile file for is creating aliases and modifying the PATH.

### Alias

An alias allows you to create shortcut commands that point to longer commands, thus saving on time.<br>
For example, if we used `ls -al` often and wanted a shortcut for this we could create an alias `lal` that would run this command for us.<br>
Create a .bash_profile file in the /home/ubuntu directory by typing
```console
nano .bash_profile
````
Within this file we will create a new alias for `ls -al` by typing
```console
alias lal=’ls -al’
````
Save and close the file as per the nano instructions above.<br>
Now, each time you use the terminal in the Amazon instance, you can type lal and it will run the command ls -al. However, because .bash_profile is only called the first time we use the terminal, we would have to shut down the instance and start again to enact this change.<br>
To save on having to do this each time we modify and test the .bash_profile, we can manually load the .bash_profile file by typing
```console
source .bash_profile
````
Now if you type `lal` the command should run as specified.
Aliases can be used to create command shortcuts for any task. This is useful particularly for repeated tasks such as ssh and scp to locations with long addresses. For instance, lets say in order to shh to my computer in work I had to type
```console
ssh conor@work.address.com
````
This would become tedious and hard to remember if addresses are long and complicated. Instead I can create an alias ‘work’ to enact this command for me. E.g.
```console
alias work=’ssh conor@work.address.com’
````
Thus I just type ‘work’ on the terminal and the ssh command is run for me.

### PATH

The commands that are run within the terminal such as cd, less, ls etc. are executable files that have been created and stored in specific folders in the system. The system then knows where to look for these programs by searching in directories specified in the environment variable PATH.<br>
You can view your current PATH by typing
```console
echo $PATH
````
which will likely output something like<br>
/usr/local/bin:/usr/bin:/bin<br>
This means that the system can run executable programs that are stored in these three folders (separated by the : ) without the user having to specify the absolute path to the folder.<br>
A user may wish to modify this path to add other folders where such programs can be stored. This is useful for downloaded programs which you want to be able to run.<br>
For instance, if you download the BLAST+ package from NCBI and store it in your home directory, each time you wish to run blastn in the terminal you would have to type
```console
/home/ubuntu/blast+/bin/blastn <options etc>
````
This is because the system does not have that folder in the PATH and thus you must specify the path to the program manually each time.<br>
Alternatively, a good practise is to create a bin folder in your home folder (i.e. /home/ubuntu/bin/) and store all downloaded programs (like BLAST) in this folder. You then add this folder to the path in the .bash_profile<br>
Thus, if a folder /home/ubuntu/bin/ exists and blastn is inside this we can add the folder to the path by editing the .bash_profile file and writing
```console
export PATH=$PATH:/home/ubuntu/bin
````
This command says to set the PATH to whatever is currently in the PATH ($PATH:) followed by the new addition (/home/ubuntu/bin)<br>
Save the .bash_profile file and exit. You can reload the .bash_profile file manually again by typing
```console
source .bash_profile
````
Now if you use `echo $PATH` you will see the /home/ubuntu/bin added to the end of the PATH. Therefore, any executable program placed in this folder (eg. blastn, raxml, mafft etc) can be called directly from the command line, similar to cd etc.

## Other useful commands

Below is a brief overview of some other useful commands. I suggest looking at these in more detail yourself.<br>
wc counts words or lines in a file or output.<br>
e.g.<br>
* `wc -m file.txt` will output the number of characters in the file<br>
* `wc -l file.txt` will output the number of lines in the file<br>
* `ls|wc -l` will take the output from ls and then pipe to wc, resulting in a count of items in the directory

cut undertakes basic text processing by cutting a text file in specific ways.<br>
e.g.
* cut -c2 file.txt will return the second character of each line in the file
* cut -c3-5 file.txt will return the 3rd, 4th and 5th character of each line in the file
* cut -c2- file.txt will return from the 2nd character to the end of the line for each line in the file
* cut -d’:’ -f1 file.txt will take a file, cut each line by the : character and return the first field resulting from this split on each line

rm is the remove command. It will completely remove the file from the system and does not ask for confirmation before doing so.<br>
**NOTE:** rm removes the file and does not send it to the trash. Thus, once you use rm on a file it is gone and irretrievable.<br>
**NOTE2:** be VERY careful using rm inside loops. If you make a mistake it may end up removing multiple files you did not want removed without asking for confirmation. This is very dangerous when using in loops that use cd to step in and out of directories.<br>
Always test loops you wish to use for rm with echo commands instead first.<br>
The rm format is
```console
rm <filename>
```
Remember: rm is like alcohol: use responsibly.

## UNIX shortcuts

The UNIX terminal has many shortcuts using the keyboard to make it easier to edit commands. For example:
* ctrl-a will bring you to the start of a line on the prompt
* ctrl-e will bring you to the end of the line
Also, if you are unsure what flags etc. can be passed to a command there are manual pages built in to UNIX.
For example, to find all the options that can be passed to ls you can type
```console
man ls
````
The manuals can then be progressed and quit as per the less command.
