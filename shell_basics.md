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

> 📖 Further Reading: [relative vs. absolute paths](https://linuxhandbook.com/absolute-vs-relative-path/)

### Copying, Creating and Deleting Files and Directories
To copy a file, use `cp source_file_name destination_name`.

> ⚠️ Make sure the destination file doesn't exist, or you will overwrite it! ⚠️

If the destination you specified is a directory, the file will be copied (with the same name) into that directory. If you want to copy a directory and all its contents, use the `-r` (recursive) option. For example: `cp -r my_docs_dir my_docs_backup_dir`.

To move or rename a file or directory, use `mv source_name destination_name`. The same logic as above applies: if the destination is an existing directory, the source will be moved _into_ it. If it is an existing file, it will be _overwritten_!

To make a new directory under the current one, enter `mkdir` followed by the desired name. You can also specify a relative or absolute path as the argument, however, the parent directory for the new one you are creating has to already exist. 

Since this is a tutorial for beginners, I will skip the topic of deleting files and directories from the shell. This can be done easily and more safely from the graphical file manager, which has safeguards and recovery features.

> ⚠️ 📖 Further Reading: [rm and rmdir](https://www.hostinger.com/tutorials/how-to-remove-files-and-folders-using-linux-command-line) ⚠️

### Reading and Writing Text Files

### Ctrl-c
If you run a command or program, and it misbehaves (e.g., is taking way too long, gets stuck in a loop, is dumping too much text to the screen), you can try to stop it by hitting the `ctrl-c` key combination. If this does not work, closing the shell window will usually kill any programs you ran from it.

##### `cat`: print out text file(s)
To print out text files, use the `cat` command followed by a list of the file names (or just a single file). `cat` is short for "contcatinate", since it will print out the contents of the files, in order, joined together.

##### `echo`: print a piece of text (string)
The `echo` command, followed by a list of strings will simply print those words to the screen. Since some characters (e.g., **;**, **(**, **)**, **-**) have special meaning, as we will see in the next section, it's good practice to put your desired output inside double quotes. For example `echo "What's your name?"` will print correctly, whereas `echo What's your name?` will not.

If you need to print a double quote, you can precede it by a backslash (**\**). This is called "escaping".

For example `echo "I like \"Alice in Wonderland\""`. 

Two useful characters you might want to print are tabs and new-line. These are represented by `\t` and `\n` respectively. To use them in this way (instead of just printing the backslash and letter), use the `-e` argument.

For example: `echo -e "name\tuser id\nSam\tsdbrody"`.

Echo has many options for formatting the text, printing variables, etc. For this purpose, it uses a wide range of special characters, most noteablly **$**, **\\**, and **"**. If you try to print a piece of text but don't get the result you want, it may be because it contains a special character. Try "escaping" any non-alphanumeric characters by putting a backslash before them.

Remember, if you don't get the behavior you expect and end up stuck, you can use `ctrl-c` to break out of the program/command you ran.  

> 📖 Further Reading: echo tutorials: [1](https://earthly.dev/blog/practical-guide-to-linux-echo-cmd/) [2](https://linuxhint.com/bash_echo/)

##### `head`/`tail`: print the first/last lines of a file
`head -123 filename` will print out the first 123 (or whatever number you specify) lines of the file `filename`. `tail -123 filename` will print the last 123 lines.  

##### `less`: scrolling file view
Use `less file_name` to open a text file in a user-friendly viewer. This viewer allows you to scroll the text using the arrows and pgup/pgdn keys, as well as search for a pattern. To see the full list of options, type `h`. To exit, type `q`.

##### `nano`: basic text editor
Type `nano` to open the editor with a new, blank, file (you will be prompted for a name before saving), or `nano file_name` to edit an existing file. The editor is quite basic, but is good for making small changes or writing short scripts. Note that a list of the basic commands is at the bottom of the screen (with `^` indicating `ctrl` and `M` indicating `alt` or `option` on Macs).

### Standard Input and Output, Pipes and Redirection

### ; and ()

### Searching for and Editing Patterns
tr, sort, cut, grep, sed, 
