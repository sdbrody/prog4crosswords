# The Basics of BASH (Bourne Again SHell)

The "shell" is a "command-line" environment, meaning you can type in a command, followed by enter, to make things happen. It is mainly intended for managing files and directories (copying, renaming, creating, etc.) and for running programs. Modern computers have a graphical file managing app that does all that, but the shell is much more powerfull and flexible.

There are several varieties of shells (just like there are different web browsers). This tutorial will be using BASH which is the default shell on most systems, and almost certainly on yours.

### Ctrl-c
If you run a command or program, and it misbehaves (e.g., is taking way too long, gets stuck in a loop, is dumping too much text to the screen), you can try to stop it by hitting the `ctrl-c` key combination. If this does not work, closing the shell window will usually kill any programs you ran from it.

### Handy Shell Features
You can use the arrow keys to scroll back to previous commands and edit them. This is useful when making similar commands with small changes, but be careful! Like copy/paste, it's easy to make unintentional errors when using this technique.

You can also search backward through previous commands by typing `ctrl-r`, and then typing in part of the previous command you are looking for. Repeatedly entering `ctrl-r` will cycle backwards through all the commands containing what you typed.

You can see a list of all your previous commands by typing `history`.

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

You can type `ls` again to list any files and subdirectories. To move one step back up the directory tree (i.e. to this directory's parent), use `cd ..`. To refer to the current directory, you can use a single period `.`. `cd .` will change directories to the current one, essentially doing nothing, but the `.` shortcut will be useful in the future. 

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

## Reading and Writing Text Files

##### `echo`: print a piece of text (string)
The `echo` command, followed by a list of strings will simply print those words to the screen. Since some characters (e.g., **;**, **(**, **)**, **-**) have special meaning, as we will see in the next section, it's good practice to put your desired output inside double quotes. For example `echo "What's your name?"` will print correctly, whereas `echo What's your name?` will not.

If you need to print a double quote, you can precede it by a backslash (**\**). This is called "escaping".

For example `echo "I like \"Alice in Wonderland\""`. 

Two useful characters you might want to print are tabs and new-line. These are represented by `\t` and `\n` respectively. To use them in this way (instead of just printing the backslash and letter), use the `-e` argument.

For example: `echo -e "name\tuser id\nSam\tsdbrody"`.

Echo has many options for formatting the text, printing variables, etc. For this purpose, it uses a wide range of special characters, most noteablly **$**, **\\**, and **"**. If you try to print a piece of text but don't get the result you want, it may be because it contains a special character. Try "escaping" any non-alphanumeric characters by putting a backslash before them.

Remember, if you don't get the behavior you expect and end up stuck, you can use `ctrl-c` to break out of the program/command you ran.  

> 📖 Further Reading: echo tutorials: [1](https://earthly.dev/blog/practical-guide-to-linux-echo-cmd/) [2](https://linuxhint.com/bash_echo/)

##### `cat`: print out text file(s)
To print out text files, use the `cat` command followed by a list of the file names (or just a single file). `cat` is short for "contcatinate", since it will print out the contents of the files, in order, joined together.

##### `head`/`tail`: print the first/last lines of a file
`head -123 filename` will print out the first 123 (or whatever number you specify) lines of the file `filename`. `tail -123 filename` will print the last 123 lines.  

> 📝 If you enter `cat` without a file, press `ctrl-d` to exit. The reason for this has to do with standard input, described below.

##### `less`: scrolling file view
Use `less file_name` to open a text file in a user-friendly viewer. This viewer allows you to scroll the text using the arrows and pgup/pgdn keys, as well as search for a pattern. To see the full list of options, type `h`. To exit, type `q`.

##### `nano`: basic text editor
Type `nano` to open the editor with a new, blank, file (you will be prompted for a name before saving), or `nano file_name` to edit an existing file. The editor is quite basic, but is good for making small changes or writing short scripts. Note that a list of the basic commands is at the bottom of the screen (with `^` indicating `ctrl` and `M` indicating `alt` or `option` on Macs).

## Standard Input and Output, Pipes and Redirection

When a program prints some text (for example, `echo` or `cat`), by default it goes to the shell's designated "standard output", which is the terminal display. However, BASH allows you to _redirect_ this output to a file, using the `>` sign. For example, entering `echo "hello world!" > test_file.txt` will create a file named "test_file.txt", and print "hello world!" into it. Nothing is printed to the screen .You can check out the file using `cat`, `less`, or `nano`, as described above.

> ⚠️ Make sure the destination file doesn't exist, or you will overwrite it! ⚠️

**Q.** What does `cat file1.txt > file2.txt` do?

<details>
  <summary>Click to reveal answer</summary>
  
  > **A.** The command copies file1.txt to file2.txt, similarly to using `cp`. Also similarly, if file2.txt already existed, it would be overwritten with the content of file1.txt.
</details>


To append to an existing file, used `>>`. For example, entering `echo "and this is the 2nd line" >> test_file.txt` will add the line to the file.

All the programs for displaying text files listed above are designed to read from the shell's "standard input" source if no file is given as an argument. By default the standard input source is your keyboard, which leads to the strange behavior you might have seen if you typed `cat`, `head`, or `tail` without a file.

This is not very useful in the default setting, but becomes very powerful with the use of **|**, known as the "pipe" symbol. Putting "|" after a program "pipes" its output to the next program, or to put it another way, redirects the first program's standard output to be the next one's standard input. You can chain multiple programs together like this for all kinds of handy functionality.

**Q.** What does `cat my_long_file.txt | head -100 | tail -10 > result.txt` do?

<details>
  <summary>Click to reveal answer</summary>
  
  > **A.** The command copies lines 91 through 100 of my_long_file.txt into result.txt: `cat` prints the whole file, which gets piped to `head`, which prints only the first 100 lines, which get piped to `tail`, which prints the last 10 of those 100 lines (i.e., lines 91-100 of the original file), which get redirected into result.txt. 
</details>

> 📝 There is also a "standard error" output source to which errors are printed. By default that is your display. When you redirect program output using **|** or **>**, error messages are not redirected, and you will see them on your screen. This is usually desirable, since it prevents you missing errors that are written to a file. However, if you _do_ need to redirect error messages, instructions can be found in the "further reading" recommended below. 

#### `tee`: print to display _and_ to file
In many cases, especially when you are tweaking a script or verifing behavior, you want to see the program output on the screen, but also save it to a file. To do this, use `tee` (so called because it acts as a T-junction in the pipe). For example:
`cat my_long_file.txt | head -200 | tee result.txt` will write the first 200 lines of my_long_file.txt to both the screen and result.txt.

> 📖 Further Reading: [BASH piping and redirecting:](https://www.redhat.com/sysadmin/redirect-operators-bash)

### Grouping Shell Commands
Sometimes you want to set off a sequence of multiple shell commands without having to wait for each one to finish. You can do this by separating the commands with a semicolon (**;**). One handy example is to measure the time a long program takes. You can run the command `date; my_long_program; date`, which will print the date and time, then run your program, and then print the date right after your program completes.

What if you wanted to capture the output of the previous example in a file? If you try to append `> filename.txt` to the previous command, it will only write the output of the last command in the sequence to your file, since each **;** is treated as strating a new command. To group together a bunch of commands for the purposes of capturing their combined output, place them in parantheses.
For example: `(echo "Dear Sam," ; cat form_letter.txt) > letter_to_sam.txt` will print the personalized greeting "Dear Sam," followed by the contents of form_letter.txt into a new file named letter_to_sam.txt.

### Writing Shell Scripts
If you find yourself reusing specific sets of commands frequently, you can bundle them into a _shell script_ for convenience. Shell scripts are simply text files that contain the commands you want to run. By convention, they usually end in `.sh` instead of `.txt`.

For example, you can run `nano lines91to100.sh` to create and edit a new file called `lines91to100.sh`. Then type in `head -100 | tail -10`, save, and close. You then need to run `chmod +x lines91to100.sh` to turn it into an **executable** file (meaning it can be run as a command). You now have your first shell script!

You can use it like this: `cat my_long_file.txt | ./lines91to100.sh`

> 📝 You must run the scripts using their full path. For scripts that are in your current directory, this means `./` followed by the file name. For scripts in a sub directory called `scripts`, it would be `./scripts/` followed by the file name.

The previous script is very specific, always printing out lines 91-100. You can add more flexibility by using command line arguments. Inside BASH scripts, the arguments given when running the program are referrenced by `$1` `$2` etc. So if you wanted your script to be more flexible, you could create a new script `some_lines.sh` (or edit your old one) as follows: `head -$1 | tail -$2`. Remember to `chmod +x some_lines.sh`!!

If you then run `cat my_long_file.txt | ./some_lines.sh 50 5` it will print out lines 46-50 of `my_long_file.txt`, if you run `cat my_long_file.txt | ./some_lines.sh 10 3` it will print out lines 8-10, and so on.

You can also use the variables inside `echo` strings, for example, you can create a script named `personalized_letter.sh` that contains `(echo "Dear $1,"; cat form_letter.txt) > $2`. When you run `./personalized_letter.sh Sam sams_letter.txt`, it will print the form letter with the header "Dear Sam," to the file sams_letter.txt. 

We've only scratched the surface of what you can do with BASH scripts. There are many tutorials available on the web, and I've listed a couple below. BASH is a full-powered programming language, and you can do almost anything with it, but you shouldn't! It is badly suited for complex logic or long programs. It should mostly be used only to automate short sets of repeated commands. If you find yourself writing a script that is more than 5 lines long, stop. You are almost certainly better off doing it in Python. 

> 📖 Further Reading: [Deeper Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/), [Beginner to Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)




