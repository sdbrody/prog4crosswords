# Programming basics for crossword constructors
## Intro
This tutorial is intended to give very basic programming skills that will be handy for crossword constructors working on specific themes.
I try to assume very little programming experience, but there will probably be some instances where I do so anyway. Please reach out at sdbrody@gmail.com and
let me know, and I will attempt to fix the issues.

In many cases I'll only briefly touch on a subject or functionality, to give the minimum needed for the example. You'll need to do some searching on your own if you want to know more. There are many tutorials on the web for Python and Bash. This one is just aimed at getting you started.

## Setup
The tutorial assumes you have access to a linux-like shell and have Python installed. 

On a Windows machine, you can get the prerequisites by installing WSL (Windows Subsystem for Linux). To do so, open the Powershell program, and type `wsl --install`. Once installed, you can run the WSL program or open Powershell and type `wsl` to get you to the linux shell. On a Mac or Linux computer, open the Terminal program.  

Whatever system you use, you should see something like this:

![Shell prompt](imgs/shell_prompt.png)

This is called the command-line prompt (because it prompts you to type in a command). The default prompt consists of your username, followed by the **@** sign, then the name of your computer, then a colon, then your current directory path (which is **~** when you first open the shell), and finally a **$** sign.  

> 📖 Further Reading: [customizing the command prompt](https://ioflood.com/blog/bash-prompt/)

To check for Python, type `python3 --version` and press enter. If it prints out a version number, you are good to go.

## Overview
This tutorial is composed of three chapters:
1. [The Basics of BASH](shell_basics.md): covers navigating the file system (`cd, ls`), creating, copying, and displaying files (`cp, mv, mkdir, echo, cat, head, tail, less, nano`), standard input/output, piping, and redirection (`>, >>, |`), and writing shell scripts. This chapter can be skipped by those familiar with BASH.
2. [Text Search and Manipulation Tools](shell_text_manip.md): covers `tr, sort, cut, grep, sed`.
3. [Python Basics for Crossword Construction](python_basics.md): covers basic concepts and gives examples for common tasks of interest to crossword constructors for theme development and wordlist management.
