## File System Navigation
As mentioned, one of the primary purposes of the shell is dealing with files, so our first step is to learn the commands that will help navigate the file system.

### Orientation - the home directory
As mentioned earlier, the directory you are currently in is shown in the command prompt, between the **:** and the **$** signs.
When you open the terminal program, you will start off in your "home" directory, which is represented by the shorthand **~** character.
You can display the contents of your current directory using the `ls` command. This will show you all the files and subdirectories
in your current directory. On most systems, directories and different file types each have distinct colors.

Typing `ls` followed by a subdirectory will list the contents of that subdirectory.
For a detailed list, with one entry per line use `ls -l`. The list of words appearing after the name of the program are called _arguments_. The `-l` argument is only one of many options available for `ls`. We will not go into the others in this tutorial, but ...

>  📝 You can get a description and list of options for *any shell command* by typing that command followed by `--help` or preceded by `man` (both with a space between).
> For example: `ls --help` or `man ls`. However, these manual-style pages (`man` is short for "manual") can be a little tricky for beginners.
> Googling something like "tutorial for ls command" is often helpful.

The home directory is usually also the one shown when you open your computer's file manager program.
You might find it useful to open it and compare what you see there with what you see with the `ls -l` command.  

### Moving Around
You can move between directories by using the `cd` (change directory) command. For instance, if you have see a **Downloads** subdirectory when running `ls`, you can try `cd Downloads`. Notice how the last part of your prompt changes from `:~$` to `:~/Downloads$` to reflect your current location. 

You can type `ls` again to list any files and subdirectories. To move one step back up the directory tree (i.e. to this directory's parent), use `cd ..`.

You can also specify a full path as an argument to `cd`. For example, if you entered the command `cd Downloads`, and then wanted to go to a different (sibling) subdirectory in your home directory named `Docs`, you could enter `cd ..` and then `cd Docs`, or `cd ../Docs` or `cd ~/Docs`.


cd, mkdir, rm (use manager)

###
cat, echo, head, tail, less, nano
; and ()

###
standard in/out, pipe and redirect

### tr, grep and sed
 
