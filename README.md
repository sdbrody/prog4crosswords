# Programming basics for crossword constructors
## Intro
This tutorial is intended to give very basic programming skills that will be handy for crossword constructors working on specific themes.
I try to assume very little programming experience, but there will probably be some instances where I do so anyway. Please reach out at sdbrody@gmail.com and
let me know, and I will attempt to fix the issues.

In many cases I'll only briefly touch on a subject or functionality, to give the minimum needed for the example. You'll need to do some searching on your own if you want to know more. There are many tutorials on the web for Python and Bash. This one is just aimed at getting you started.

## Prerequisites
The tutorial assumes you have access to a linux-like shell and have Python installed. 

On a Windows machine, you can get the prerequisites by installing WSL (Windows Subsystem for Linux). To do so, open the Powershell program, and type `wsl --install`. Once installed, you can run the WSL program or open Powershell and type `wsl` to get you to the linux shell. On a Mac or Linux computer, open the Terminal program.  

Whatever system you use, you should see something like this:
![Shell prompt](imgs/shell_prompt.png)


To check for Python, enter `python3 --version`. If it prints out a version number, you are good to go.

## Shell Basics
The "shell" is a "command-line" environment, meaning you can type in a command, followed by enter, to make things happen. It is mainly intended for managing files and directories (copying, renaming, creating, etc.) and for running programs. Modern computers have a graphical file managing app that does all that, but the shell is much more powerfull and flexible.

There are several varieties of shells (just like there are different web browsers). This tutorial will be using BASH which is the default shell on most systems, and almost certainly on yours.

