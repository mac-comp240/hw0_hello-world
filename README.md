# A test of the course setup

This repository is designed to help you work through the mode of working that you will do for this course. Please follow the steps below after you have your account set up on our department server using the install instructions for VS Code.

You should have already followed some instructions for cloning this repository in the VS Code editor (which might mean cloning directly to the server, **or** cloning to your computer and then syncing a copy of it to the server).

**You should have the terminal open on the server and should have used the 'cd' command in the command line to be in the directory where this code is.**

______________________

# Saving your work as you go!

It is **very important** that you get into the habit of not only saving your files
on the server or your own computer, but that you also frequently *stage*, *commit*, and *push*
your code to github. We recommend that you do this in between steps of an assignment,
any time your code is working. When you do this:

- You will then have a version that you can always get back to when something goes wrong as you continue editing.

- If you need help from an instructor over email, they can see your code on github and help.

- If your laptop dies or the server goes down, there is a version on github that you can recover.


## Using git from the terminal

### 1. Stage the Changes

Stage the changes by running the following on the command line (in the terminal) for each
file you have created and/or modified:
```
    git add <filename>
```

(Avoid using shortcuts that add all files: executables and other such files should **not**
be part of your github repo.)

### 2. Commit the changes

Commit the changes by running:
```
    git commit -m "Enter a meaningful commit message between these quotes"
```

### 3. Push the changes to github

Now, you can push this to GitHub by running:
```
    git push
```

### First time?

If this is your first time running these commands from the server, you may get some warning messages, questions, etc. Read them! They will tell you what you are expected to do. You can always ask for help, but first, read the message and see if it answers your question.

Further, you can run
```
    git status
``` 

To inform you what stage in the add/commit/push process you're at, if you've forgotten, or you want a reminder of which files you've made changes to.


## Go to github.com to check for your changes

 Now in a web browser, log into your github.com account and find this repository and look for the changes that you made.



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

## 1. Library "includes" are placed at the top

Include statements are always placed at the top of the code file. These are used to indicate that we will use code from other libraries of C code. This signals to the compiler to find that library and load it during the *linking* stage of compilation.

Line 2 includes the library containing code for input/output functions:

```
#include <stdio.h>
```

### More information about the libraries and compilation
The API or interface of a library is specified in a header file, given the 
extension `.h`. The actual implementation of the library is stored in a compiled
"object code" format, which is combined with the user's program after it has been
converted to object code. For more details, see 
[Section 2.9.5 of _Dive into Systems_](https://diveintosystems.org/book/C2-C_depth/advanced_libraries.html#_compilation_steps_).


## 2. Function declarations

Programs in C are decomposed into functions. Each function takes inputs of specified types,
and either returns a value of some type or returns nothing, which is indicated by a return value of `void`.

**Function declarations** do not fully define a function. They declare its interface: the
function's name, its inputs, and its return type. Instead of having curly braces
with the actual body of the function, though, they simply end with a semicolon at
the end of the function definition line.

Function declarations are placed at the top of the code
file after the include statements. For the compiler to work, a function must be 
declared or defined before it is used. Placing a declaration at the top of the file
allows us to order function definitions in any way that makes logical sense, as the compiler knows enough to
process calls to the function, trusting that the actual definition will come later.

Line 5 declares the existence of a function called `aFunction` in this file. The function
takes in a parameter, `aNumber` of type `int, and it returns `void` (does not return anything):
```
void aFunction(int aNumber);
```


## 3. The main program

There must be one function called `main` that returns an `int` in all C programs. 
This is the main program that will be run automatically in the executable. Typically,
this function will be the first function **definition** in the file, and it does
not need to be declared separately because of this.

In this example, the main function has no input parameters. We will see later that 
`main` can take in specific parameters that feed command-line (terminal) arguments
to the program.

```
int main() {
    printf("hello world\n");
	// 42: the answer to life, the universe, and everything
    aFunction(42);
	
    return 0;
}
```

## 4. Function definitions

After the main function, C programs list the other functions in the program,
in some logical ordering.

In this program, that means the full **definition** of the function `aFunction`.

```
void aFunction(int aNumber) {
    printf("Your number is: %d\n", aNumber);
}
```

### Declarations and definitions
Note that the **definition** of a function has to match its **declaration** exactly, except
that it does contain the complete code for the function, wrapped in curly braces.

Every declared function must have a definition later on.

____________________

# Building code with make

The example program in this assignment is extremely simple. However, as our programs get more complicated, compiling the C code gets much more complicated as well, especially when you have multiple code files that make up a project. It can be a struggle to remember which files need to be compiled with which compiler options, and how to combine together the files into one executable!

To help manage this, Unix systems provide a command-line program called `make` which reads a special file named `Makefile` to determine how to compile a C program. You create the Makefile and write in it how compilation needs to work. Then you don't have to remember it: you just call `make`!

Open the file called Makefile. It looks like this:

```
CC = gcc                          # line 1
                                  # line 2
hello: hello.c                    # line 3
	$(CC) -o hello hello.c        # line 4
                               # line 5
clean:                            # line 6
	rm hello                      # line 7
```


There are some important things to know about makefiles. ...


- lines 4 and 7 are indented with a tab (it MUST be a tab)

- line 1 defines a variable `CC` to be the string gcc. This is defining which compiler
on the computer we want to use. On line 4, `$(CC)` tells `make` to substitute the
value of `CC` with what it is defined to be on line 1

- comments begin with `#`

- the words that come before colon on unindented lines (such as line 3 and line 6) are
called "targets". They are often the name of the executable to be created, as in line 3,
or describe whatever else we want to do (as in line 6).

- the file names after the colon on line 3 indicate which files this executable depends on 
(in this case one `hello.c` file).

- the tabbed-in line 4 indicates how to compile and create the executable named `hello`.

- the second target on line 6 is conventional for Makefiles: the `clean` target is
followed by commands that clean up the files created by the main target(s).


See [Section 17.5 in _Dive into Systems_](https://diveintosystems.org/book/Appendix2/makefiles.html#_make_and_makefiles) 
for a detailed tutorial on `make` and Makefiles.


### A warning about tabs

One problem that often occurs when editing makefiles is to forget those pesky tab characters. If you get an error like this:

```
Makefile:4: *** missing separator.  Stop.
```

It means that you used spaces instead of tabs.

## Try using make

1. Type these two alternatives at the command line:

```
make

make hello
```

When you run `make` with no target specified, it runs the first target in the file (in this case,
`hello`). You can also specify the target as the second example above does.

2. To see the result, run the compiled program:

```
./hello
```


3. Edit the `hello.c` file in VS Code by changing this line in main (line 14) to print some  number other than 42:

    aFunction(42);

Make sure the changes to `hello.c` are saved. 

Then, in the terminal, use either command above again to re-compile the program with make,
and re-run it to be sure that your changes worked.

4. Finally, clean up your folder by doing this:
```
    make clean
    ls
```

What changed? 

Then try making the code again.

Now you have the basics of the gcc compiler for C code and using make to handle the 'build' of your code.

# Turning in the homework

Double check that you have done everything required by this assignment, then make 
one final round of staging, committing, and pushing your code. That's all you need to hand in your
homework.

