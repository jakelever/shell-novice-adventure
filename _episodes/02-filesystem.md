---
title: "Background (Moving Around)"
teaching: 15
exercises: 0
questions:
- "How can I move around on my computer?"
- "How can I see what files and directories I have?"
- "How can I specify the location of a file or directory on my computer?"
objectives:
- "Explain the similarities and differences between a file and a directory."
- "Translate an absolute path into a relative path and vice versa."
- "Demonstrate the use of tab completion, and explain its advantages."
keypoints:
- "The file system is responsible for managing information on the disk."
- "Information is stored in files, which are stored in directories (folders)."
- "Directories can also store other directories, which forms a directory tree."
- "`cd path` changes the current working directory."
- "`ls path` prints a listing of a specific file or directory; `ls` on its own lists the current working directory."
- "`pwd` prints the user's current working directory."
- "`/` on its own is the root directory of the whole file system."
- "A relative path specifies a location starting from the current location."
- "An absolute path specifies a location from the root of the file system."
- "Directory names in a path are separated with '/' on Unix, but '\\\\' on Windows."
- "'..' means 'the directory above the current one'; '.' on its own means 'the current directory'."
- "Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file."
- "Most commands take options (flags) which begin with a '-'."
- "`cat` displays the contents of its inputs."
---

The part of the operating system responsible for managing files and directories
is called the **file system**.
It organizes our data into files,
which hold information,
and directories (also called "folders"),
which hold files or other directories.

The image below gives an initial summary of the files that we're going to be looking at. You can see that the emails folder is inside the adventure-data folder. And that the README.md file is also inside the adventure-data folder.

![The File System](../fig/file_hierarchy.png)

## Starting Off

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, let's open a shell window:

~~~
$
~~~
{: .bash}

The dollar sign is a **prompt**, which shows us that the shell is waiting for input;
your shell may use a different character as a prompt and may add information before
the prompt. When typing commands, either from these lessons or from other sources,
do not type the prompt, only the commands that follow it.

## Where am I?

Windows and MacOS uses a graphical user interface (GUI) to let you interact with files. You can click on folders to move around the file system and see everything presented as icons. With the shell, everything is presented as text and the way to interact is by typing commands.

First we want to know where in the filesystem we are. For that we use the `pwd` command. It stands for "print working directory". The working directory is the name used for the directory that we are currently in. All commands that we run will be based in this directory (unless we specify otherwise).

~~~
$ pwd
~~~
{: .bash}

~~~
/home/exampleuser/
~~~
{: .output}

The output will look different for you and depend on what type of system you are using and your own username. The first forward slash designates the root of the whole file system. We are then inside the home directory, and then inside the exampleuser directory.

> ## Home directory
>
> You normally start in your home directory. On Linux, this is normally /home/USERNAME, for windows it is /C/Users/USERNAME and for MacOsX it is /Users/USERNAME (where USERNAME is your username).
{: .callout}

## What is here?

With a GUI, the files appear as little icons. But with the shell, we need to use a command to get a list of files in the current working directory. For that we use `ls` which stands for "list".

~~~
$ ls
~~~
{: .bash}

~~~
documents Desktop downloads thesis.pdf
~~~
{: .output}

This gives the contents of current directory. Notice that it shows both files and directories.

> ## Arguments
>
> When you call a command, you can give it extra information on what it should do. These are often called arguments or parameters. This might be a signal to give the output in a different format, or to process a different file. It depends on the program.
{: .callout}

A useful argument for `ls` is to get more details using `-l`. Try it out. Now each file/directory is on each line with extra information.

~~~
$ ls -l
~~~
{: .bash}

~~~
drwxr-sr-x  2 exampleuser users 4096 Apr 23 15:39 documents
drwxr-sr-x  2 exampleuser users 4096 Apr 23 15:39 Desktop
drwxr-sr-x  2 exampleuser users 4096 Apr 23 15:39 downloads
-rw-r--r--  1 exampleuser users  210 Apr 23 15:39 thesis.pdf
~~~
{: .output}

The `ls` command has a lot of possible arguments. Many commands will give you more information using the `--help` argument. Give it a try with ls.

~~~
$ ls --help
~~~
{: .bash}

## I want to go somewhere

It's not much fun staying in the same place, so to get moving we use `cd`. It stands for "change directory". But it normally takes one argument. In this case, the extra piece is where we should move to. The easiest is the name of a directory in our current working directory. Let's try moving to the Desktop (which is normally a directory called Desktop in your home directory.

~~~
$ cd Desktop
~~~
{: .bash}

And a quick check with `pwd` shows that we've moved.

~~~
$ pwd
~~~
{: .bash}

~~~
/home/exampleuser/Desktop/
~~~
{: .output}


> ## Up and Down arrows
>
> You don't have to retype every command every time. Try using the up and down arrows on the keyboard to cycle through previous commands.
{: .callout}


~~~
$ ls
~~~
{: .bash}

~~~
adventure-data
~~~
{: .output}

Let's keep going to the downloaded files. You should have already downloaded them to the Desktop. If you haven't already, go to the [setup page](../setup/)

~~~
$ cd adventure-data
~~~
{: .bash}

Let's check what we've got.

~~~
$ ls
~~~
{: .bash}

~~~
bank_statements  contacts.txt  emails  email_summaries  README.md  research_files  tools
~~~
{: .output}

## Let's check out the research files

~~~
$ cd research_files
$ ls
~~~
{: .bash}

~~~
project_arcturus  project_columbia  project_smith
project_asimov    project_gibson    project_titan
~~~
{: .output}

## Going back

If you go into the `research_files` directory but want to go back out, you can use the `cd ..` command. `.` and `..` are special cases in the shell. `.` means here and `..` means up one.

~~~
$ pwd
$ cd ..
$ pwd
~~~
{: .bash}
~~~
/home/exampleuser/Desktop/adventure-data/research_files
/home/exampleuser/Desktop/adventure-data
~~~
{: .output}

> ## ls can take a directory as an argument
>
> Instead of using a combination of `cd` and `ls` to see the contents of a directory, you can give the name of the directory to `ls` and it will list the contents. But remember, `ls` won't change the current working directory. If you want to move into that directory, you'll still need to use `cd`.
> ~~~
> $ ls research_files
> ~~~
> {: .bash}
{: .callout}

## Getting straight to the point

You don't always need to do a set of `cd` commands to get to a directory, when one will do it. 

~~~
$ cd research_files
$ cd project_arcturus
~~~
{: .bash}

Instead of two `cd` commands, you could just use one.

~~~
$ cd research_files/project_arcturus/
~~~
{: .bash}


> ## Tab-complete
>
> Shell users are lazy and typing out long filenames is tedious. If you've started typing a filename, you can press Tab and the shell will try to complete the rest (if there is only one possibility).
{: .callout}

## Absolute Paths

We've been navigating using **relations** paths. So far, any directory name we give to `cd` depends on where we currently are in the file system. We can also give an `absolute` path that will get you to that location wherever you start in the file system. Let's get our current working directory using `pwd`

~~~
$ pwd
~~~
{: .bash}
~~~
$ /home/exampleuser/Desktop/adventure-data/research_files
~~~
{: .bash}

We could move back to the adventure-data directory using an absolute path (where we list all the parent directories above it). An absolute path is easy to spot as it will start with a forward slash.

~~~
$ cd /home/exampleuser/Desktop/adventure-data
~~~
{: .bash}

## Reading Tiny Files

The `cat` command is a very basic command that displays the contents of a file. It actually stands for concatenate as you can use it to concatenate multiple files. You should only use it to display very small files which will contain unformatted text. It can't deal with things like PDFs or Word documents. Its most basic usage involves one argument: the name of the file you want to display.

~~~
$ cat README.md
~~~
{: .bash}

## Exercise

Dr Gill was apparently working on the Gibson project at Sandford Biotechnologies. Using `cd`, `pwd`, `ls` and `cat`, can you read the summary for the gibson project? It will be in the research_files directory.

> ## Solution
>
> ~~~
> $ cd research_files
> $ ls
> $ cd project_gibson
> $ ls
> $ cat summary.txt
> ~~~
> {: .bash}
>
{: .solution}

## Bonus Points
- Can you reduce the number of commands needed to read the file? Can you use just one `cat` command?
- Can you read the README file about the tools that are supplied?

