# Command Line Basics

The following information is related to the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation also found in this GitHub repository. 

## Overview

Using the command line interface (CLI), you can issue commands to a computer via lines of text. The CLI passes commands to the computer's operating system, which runs the requested tasks. There are many CLI tutorials freely available (some recommended ones are listed at the bottom of this page), so a great way to get started is to dive in with some sample files on your Desktop or in a virtual machine. As mentioned in the _NDSR 2016 Immersion Week_ slides, you want to have some freedom to play around with the CLI without harming your machine or machines on attached networks.  

### Quick Reference: Commands and tips

You will likely use the following commands frequently as you get more comfortable on the CLI. These, and more, are part of the exercises below. 

`pwd` - prints working directory (a.k.a. shows current directory)

`cd [directory]` - changes working directory to a new directory you enter

`ls` - lists visible files in your working directory

`cp` - copies file(s)

`mv` - moves file(s)

`mkdir` - creates directory

`rm` - !!! removes/deletes files or directories. *Proceed with caution!* 

- You can use your `tab` button to auto-complete filenames, directory names, and paths in the Terminal. Start typing and click `tab` and the CLI will suggest possible matches - can help save time and increase accuracy of your commands. 
- Want to know more about command syntax, options, or usage? Read the manual page (aka "man page"). You can find this online or usually by typing _man_ followed by the command (`man cd`) into the Terminal. Read the docs!

## Getting started

1. Open Terminal (Applications > Utilities > Terminal). 

2. Download the sample materials for this exercise ([cli-basics-samples.zip](./workshop-samples/cli-basics-samples.zip). Do not move the ZIP file - leave it in your DOWNLOADS folder. 


### Navigating a file system

A hierarchical directory and file tree follows this kind of structure: 

/- root

/-- directory1

/-- directory2

/--/-- fileA

/--/-- fileB

/--/-- directory3

You can move through your own file system via the CLI with a few simple commands. 

1. Best start is to figure out where you are. You can quickly identify your current working directory in two ways:
    
 1a. Type `pwd` into the Terminal and hit enter. This command prints the path to your current or "working" directory to the Terminal

 _OR_

 1b. Look at the command prompt in the Terminal. When you open a new Terminal window the tilde (~) represents the home folder which is your current working directory. When you are in a different folder, it will display the name of the directory (e.g. _Desktop_ if you are in _/Users/username/Desktop_).

2. Let's change your working directory to your Desktop. Chances are you have a few files or directories sitting in that folder, right? Type the following into the Terminal.

        cd Desktop

 Then confirm you're in the right place. Type `pwd` - what appears after you submit this command?

3. Great. Now we are going to use the `ls` or list command to see what is in your working directory (the Desktop). Type:

        ls

 - What gets printed to the Terminal? Now try adding the `-a` option, which lists ALL files (including hidden ones like .DS_Store) in your working directory. 
    
        `ls -a`
    
 - What is the difference between the list of files and directories that printed with `ls` versus `ls -a`?

4. Before we move forward, try jumping around to different directories and getting comfortable with navigating the file hierarchies on the CLI. Use these commands (and try `ls` and some of its options!).


        cd ..

 - move to the parent of the current directory

        `cd ../..`

 - move up two levels to the grandparent directory
    
       `cd /Applications/Utilities`

 - move to the Applications directory then the Utilities subdirectory
  
        `cd -`

 - move to the previous working directory (also prints the path to the previous working directory)


### Opening, reading, writing, and moving files and directories

1. Let's dig into the sample files. Change the working directory to where ever the ZIP file was auto-downloaded to. You can type `cd` then drag and drop the folder containing _cli-basics-samples.zip_. This might look like:

        cd Downloads/

2. List all the files in your new working directory - is _cli-basics-samples.zip_ there? You can check quickly by listing only files that have the extension "zip" with this command:

        ls *.zip

 This command lists filenames ending with the four characters following the asterisk (dot, z, i, p in that order). Try this command with another common file extension (like .pdf or .jpg).

3. Now we want to make a copy of _cli-basics-samples.zip_ on your Desktop - we'll use the move or `mv` command. For example, `mv file1.txt otherDirectory/file2.txt` - "moves" and/or renames file1 from source location to a destination location (`otherdirectory` and names it `file2.txt`). In the Terminal, type:

        mv cli-basics-samples.zip ~/Desktop/cli-basics-samples-moved.zip

 - Using Finder (or just looking at your Desktop) - can you visually confirm the file has been moved? 

4. Let's use the CLI to verify the file was moved correctly and unzip it. Do the following:

        cd ~/Desktop/

        ls *.zip

 - has the file _cli-basics-samples-moved.zip_ been moved to the Desktop?

        `unzip cli-basics-samples-moved.zip -d cli-basics-samples`

 - unzips file to a directory on the Desktop we are naming _cli-basics-samples_

5. Look in the provided samples directory.

        cd cli-basics-samples

        ls 

 - What files and folders are provided? Now change your working directory into the subdirectory and use the list command to explore this sub-hierarchy.

 - Change your working directory back to _cli-basics-samples_ (you can use the path or `cd ..`)

6. Let's move some files around. First, find the JPEG in the folder (HINT: use an `ls` option)

7. I want to make a copy of _Shar-pei_casa.JPG_ in the subdirectory of this samples folder. This is done using `cp` command. For example, `cp file1.txt file2.txt` makes a copy of file1 and names/locates it as file2. To make a copy of this JPEG with a new name in the subdir, type:

        cp Shar_pei_casa.JPG this-is-a-subdir/dog.jpg

8. List the files in the subdir. Instead of changing the directory and using `ls` (multi-step), you can invoke `ls` from your current directory if you name the location you want to list files in. Type:

        ls this-is-a-subdir/ 

 - Do you see the newly copied JPEG image? 

9. You should still be in _cli-basics-samples_ (check with `pwd`). Let's look at one of the text files provided. You can read the file in two ways:

 9a. Using `cat` to print the text in the Terminal. `cat` can be used to display, combine/append, or create new text. Let's start by just reading the existing text.
    
        cat hello.txt
 _OR_
     
 9b. You can open a file in the default application by using the `open` command:
    
        open hello.txt

10. You've used a text editor (TextEdit, Xcode, SublimeText, etc.) - and the CLI has a built in text editor. It can be a bit tricky to learn, but can be easily used for simple editing or just viewing existing text. Use the man page for vim or check it out online. Here's how to find it:

        vim file1.txt

 FYI: to escape vim, click the `esc` key. Then `control` + `z`. 

11. Let's create a new subdirectory. Use the `mkdir` command (aka make directory). Try this:

        mkdir other-subdir

12. Use `echo` command to create a new file in the _other-subdir_, which appends or replaces text via the CLI.

        echo "This is brand new text for your brand new file" > other-subdir/hola.txt

13. Use `cat` or `vim` to confirm that text appears in the _hola.txt_ file. 

14. Let's clean up these samples. There may be cases where you need to delete files or folders, so let's learn the basics to avoid any accidental deletions. Let's get rid of the _other-subdir_ folder. Try to delete the directory:

        rmdir other-subdir

 - What happened? 

15. There are few instances where the CLI will try to stop you from deleting something - this is one of them. Change the working directory to _other-subdir_. Then delete the _hola.txt_ file.

        rm hola.txt

 - Notice how this is `rm`, and to delete a directory is `rmdir`. 
    
        `ls` 

 - The directory should be empty - yes?

16. `cd` back up to _cli-basics-samples_. Now try #14 again. Check with `ls` that it's successfully deleted.

17. Ok, last deletion. Let's get rid of that _dog.jpg_. You can remove files from non-parent directories For example, if you're in _cli-basics-samples_ you can use the following command to delete a grandchild file:

        rm this-is-a-subdir/dog.jpg 


## Recommended resources

1. [Command Line Crash Course](http://cli.learncodethehardway.org/book/) is a great introduction to the CLI and shell, good as a refresher too :)
2. [Introduction to the command line interface](http://tutorial.djangogirls.org/en/intro_to_command_line/) by Django Girls (available in 14 languages, additional video instruction in English)
3. [Unix Commands and Batch Processing for the Reluctant Librarian or Archivist](http://journal.code4lib.org/articles/9158) by Anthony Cocciolo, (2014)
4. [An Introduction to Using the Command Line
Interface (CLI) to Work with Files and Directories (MAC OS)](https://www.avpreserve.com/wp-content/uploads/2015/09/CLI_MacOS_Tutorial.pdf) by Bertram Lyons, AVPreserve (2015)
5. [the sourcecaster](https://datapraxis.github.io/sourcecaster/) - CLI command generating resource that "helps you use the command line to work through common challenges that come up when working with digital primary sources", created by [Thomas Padilla](https://github.com/thomasgpadilla) and [James Baker](https://github.com/drjwbaker)
6. [Script Ahoy: Community Resource for Archivists and Librarians Scripting](http://dd388.github.io/crals/) created by Jarrett Drake and Dianne Dietrich.



