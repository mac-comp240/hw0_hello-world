# A test of the course setup

This repository is designed to help you work through the mode of working that you will do for this course. Please follow the steps below after you have both a terminal program (such as Termius) and the Atom editor installed on your machine with the remote-sync package also installed.

You should have already followed some instructions for cloning this repository in the Atom editor and syncing a copy of it to the server.

**You should have the terminal open on the server and should have used the 'cd' command in the command line to be in the directory where this code is.**

# Hello, World

The file hello.c contains the classic basic C program. Let's start by compiling it and running it **on the server.**

## Compile it

In the terminal, type:

    gcc -o hello hello.c


## Run it

The following part of the compiler command above

    -o hello

indicates that an executable program file called hello will be created from your hello.c file.

To execute this executable file on the command line, type the following:

    ./hello

___________________

# Basic features of hello.c

The example program in the file `hello.c` has the basic components that all C programs have. Your programs should contain these parts at a minimum. We will add more complexity to our programs a bit later.

Let's look at the sections of this program, from top to bottom.

## 1. the includes at the top

Line 2 contains an include statement. These are used to indicate that we will use code from other libraries of C code. This signals to the compiler to find that library and load it during the *linking* stage of compilation.

### Info
Please see:
In chapter 1 of your course textbook, Figure 1.3 depicts the compilation process for a C program.


## 2. function declarations

Programs in C are decomposed into functions. Each function returns a value of some type, or returns nothing, in which case, as is shown on line 5, it returns void, as indicated before the function name itself.

Line 5, a **declaration**, is provided at the top of the file to indicate that there is a function called `aFunction` later in this file, and it returns void and takes one parameter of type int.

## 3. the main program

There must be one function called main that returns an int in all C programs. In this example, the main function has no parameters. We will see later that main can take specific parameter as command-line arguments.

## 4. function definitions

Beginning on line 17 is where we see the full **definition** of the function called `aFunction`.

### Info
Note that a **definition** is separate from a **declaration** and contains the complete function.

____________________

# Building code with make

C code compiling can be fairly complicated, especially when you have multiple code files that make up a project.

Unix systems provide a command-line program called `make`, when used in conjunction with a file that you write, usually named `Makefile`, will let you more easily build your C code into an executable.

Open the file called Makefile. It looks like this:

    CC = gcc                     #line 1
                                 #line 2
    hello: hello.c               #line 3
    	$(CC) -o hello hello.c   #line 4
	                             #line 5
    clean:                       #line 6
    	rm hello                 #line 7



There are some important things to know about makefiles. ...


- lines 4 and 7 are indented with a tab (for make, it MUST be a tab)

- $(CC) is replaced with what is to the right of the = in line 1
- comments begin with #

- the first line that has a word followed by a colon (in this case line 3) indicates the name of the executable that will get made from this makefile (in this case the program named `hello`).

- the file names after the colon on line 3 indicate what this executable depends on (in this case one hello.c file).

- the tabbed-in line 4 indicates how to compile and create the executable named `hello`.

### warning

One problem that often occurs when editing makefiles is to forget those pesky tab characters. If you get an error like this:

    Makefile:4: *** missing separator.  Stop.

It means that you used spaces instead of tabs.

## Try using make

Type these two alternatives at the command line:

    make

    make hello

Edit the hello.c file in Atom on your laptop by changing this line in main (line 14) to print some  number other than 42:

    aFunction(42);

Next, **save the changes to hello.c**. To make sure the changes were synced on the server, go back to the terminal and try either command above again to re-compile it with make.

Do this:

    make clean
    ls

What did the make clean command do?

Then try making the code again.

Now you have the basics of the gcc compiler for C code and using make to handle the 'build' of your code. Next step:'turn it in'.

______________________

# Keep versions and Turn in assignments by saving changes to github

**IMPORTANT:** You should periodically do what we are going to describe here as you work on your homework. When you are at a point where code is working, it is always a good idea to *commit* and *push* it up to github, because:

- You will then have a version that you can always get back to when something goes wrong as you continue editing.

- If you need help from an instructor over email, they can see your code on github and help.

- If your laptop dies, there is a version on github that you can recover.

## From Atom editor (VS Code below)

There are two steps to getting your code up to your github repository:

1. Stage and commit
2. Push committed changes to github

### 1. Stage and Commit

Open the Git panel, which should appear on the right, showing changed files in yellow and new files in green in the top section.

Choose 'Stage All' in the upper right by clicking on it. The files will move to the center section, labeled 'Staged Changes'.

In the area that says "Commit message", type some words to help you remember the changes you made, such as 'updated value printed.'

**Important:** A meaningful text is really helpful here, so that you can get back to this change if you need to later.

Now click the "Commit to Master" button.

### 2. Push committed Changes to github

In the bottom panel towards the right corner, just to the left of the GitHub button, choose the button labeled 'Push 1'. It is finished when the arrow goes away and the button changes to 'Fetch'.

You should be able to go back to GitHub and check whether your changes are now there for this repository.

## From Visual Studio Code editor

From the far left, choose the tab along the left side that looks like 3 circles connect with lines.

Look for files under the section labeled CHANGES.

 You can stage each change individually by hovering over a file name and clicking the + icon.

 You can stage all the changes to several files by choosing the menu with three dots, ..., and then 'Stage All Changes'.

 Write in a commit message for these changes. It helps to recover this commit if you give it a reasonable message.

 Choose the check mark icon to commit the changes.

 Then from the three dots menu, choose to 'Push'.
