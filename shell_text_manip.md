# Manipulating Text with BASH (Bourne Again SHell)

This chapter will discuss how to use the the features of BASH and its built-in tools to search through and modify text files. The focus will be on the use cases that come up when constructing crosswords. As in the previous chapter, I will not describe all of the options and possibilities of each tool, but will try to give useful pointers for further reading.

## Basic Text Manipulation

### Swapping and Deleting Characters with `tr`

The `tr` command (short for "translate") allows you to replace one character with another throughout a file.

For example `cat myfile.txt | tr "L" "R"` will print out the contents of `myfile.txt` with all the L's changed to R's.

> ⚠️ If you skipped the chapter on [The Basics of BASH](shell_basics.md) and you're confused by the use of `cat` or `|`, go back and review it.  ⚠️

There are a few things to note in this example:

- `tr` is case-sensitive, so only upper-case L's will be converted (to upper-case R's). Lower-case ones will stay the same.
- L's will be converted to R's, but not vice-versa. This means it may be impossible to know if an R in the output was there before or came from the translation.

Luckily, `tr` also allows you to specify multiple replacements at once. This is done by providing two strings of letters (instead of single characters). The first letter of the string 1 is replaced by the first letter of the string 2, the second letter of string 1 by the second letter of string 2, etc.

So, to address the to issues mentioned above (only replacing upper case letters, and only translating L-->R but not vice versa), we can use the command `tr "LlRr" "RrLl"`, which will convert L to R, l to r, R to L, and r to l.

You can also use the dash (`-`) to specify a range of letters. For example, `tr "a-z" "A-Z"` converts lower-case letters to upper case (but not vice versa). This can be very useful, for instance, when creating a word list from a file with both upper- and lower-case letter (a list of book titles, say).

In addition, `tr` can delete characters, using the `-d` argument. For example, `tr -d " "` will remove all spaces from the output, and `tr -d "aeiou"` will remove all (lower-case) vowels.

> ⚠️ `tr` works on individual characters. `tr "hi" "yo"` will not replace "hi" with "yo", but instead will replace _all_ h's with y's and _all_ i's with o's! The same applies to deletion. ⚠️  

> 📖 Further Reading: you can find more examples and additional options you can use with `tr` [here](https://phoenixnap.com/kb/linux-tr).

### Handling Columns of Data with `cut`

The `cut` command has several functionalities, but the one I've found most useful is to rearrange data that comes in columns (sometimes refered to as "fields"). The most common such formats are CSV (comma-separated-values) and TSV (tab-separated-values), supported by almost all spreadsheet software. For crossword constructors, the common wordlist format is also of interest. It is comprised of two or three columns, separated by a semi-colon. The first column is the word or phrase (without spaces), the second is the score, and sometimes a third column is added, containing a sample clue.

`cut` allows you to specify the column separator (a.k.a. the "delimiter") via the `-d` argument, and to choose which column(s) you want to print out, and in what order, via the `-f` (for "fields") argument. You can also specify what to print between the columns in the output, using `--output-delimiter`.

The fields argument are specified using a list of comma-separated column indexes. For example, `-f "2,1"` tells `cut` to print the 2nd column, then the 1st. You can also specify ranges with a dash, and combine them with indexes. For example, `-f "4,1-2,7"` will print the 4th, 1st, 2nd, and 7th columns, in that order. 

To put it all together, if you had a wordlist and wanted to print the scores first, followed by a space, and then the word, you would use the command `cat my_wordlist.dict | cut -d ";" -f "2,1" --output-delimiter " "`.

A few things to note:
- by default, the input delimiter is assumed to be a tab, and the output delimiter is whatever the input one is.
- it's good practice to surround the argument values with quotes, to avoid potential issues. For example, without the quotes, the semi-colon would be interpreted by BASH as starting a new command (see [Chapter 1](shell_basics.md)).

## Advanced Text Manipulation
This section contains probably the two most powerful BASH tools in your arsenal, and the ones you will use most frequently.
While the __further reading__ links in other sections were just recommendations, for this section you will want to read and experiment as much as possible. This tutorial will only be able to provide a few basic examples, and putting in the effort to master `grep` and `sed` is very much worthwhile.
 
### Selecting Lines with `grep`

The `grep` command is used to search lines of text for a pattern of letters. The most simple patterns are exact matches. For example, running the command `cat my_wordlist.dict | grep "CAT"` will find all the entries in the wordlist (lines of text) that contain the sequence "CAT" in them, including "CATBURGLAR", "DOJACAT", "STAYCATION", and "CAT" itself.

Some useful arguments for `grep`:

- `-i` tells `grep` to ignore case, so `grep -i "CAT"`, `grep -i "cat"`, and `grep -i "cAt"` are equivalent, and will find any lines containing a "cat" regardless of whether the individual letters are upper or lower case (or a mixture).

- `-v` inverts the logic, printing only the lines that _don't_ match the pattern. So if you wanted to create a custom wordlist to use in a puzzle that has no I's in it, you could issue the command `cat my_wordlist.dict | grep -v "I" > no_i_wordlist.dict`.

- `-o` tells grep to only print the part of the line that matches the pattern, so `cat my_wordlist.dict | grep -o "CAT"` will print only the word "CAT" for every line containing that sequence (this option becomes more useful for complex patterns, as described below).

#### Regular Expressions

The main power of `grep` (and `sed`, below) is the ability to understand regular expressions (a.k.a. REs, regexs, or regexps). Regular expressions are a standard format for specifying letter patterns, and are supported by many applications, web sites, programming languages, and some search engines.

There isn't room in this tutorial to go into all the details of regular expressions or the complex things that can be done with them. I will give some of the basics below, and I've included a bunch of useful scripts [here](shell_example_scripts.md). I strongly encourage you to take a look and try to understand how they work, and also to explore and practice as much as possbile on your own.

##### Wild Card: `.`
In REs, the period is a wild card that stands in for any single character (letter, number, symbol, space, etc). For example, to find all lines containing the sequence "ALT" in alternating letters, use `cat my_wordlist.dict | grep "A.L.T"`, which will give you "T**A**B**L**E**T**", "B**A**L**L**E**T**" and many more.

##### Start and End Markers: `^`, `$`
The caret symbol (`^`) is used to mark the beginning of a line, and the dollar sign (`$`) to mark its end. So, for example, to find 6-letter words that start with B and are scored as 5, use `cat my_wordlist.dict |  grep "^B.....;5$"`. Note that if you didn't include the final "$", your command would also return lines that are scored 50 (or any score that starts with 5). If you didn't include the starting `^`, your command would return all entries that have B as the 6th-to-last character of the word, even if it isn't the first letter of the word. 

> ⚠️ Remember that in standard wordlists, each line ends with a `;` and the score, so when using grep on a wordlist, you'll want to use `;` rather than `$` to indicate the end of the word. ⚠️  

##### "One-Of" Group: `[]`
Use square brackets (`[]`) to specify a group of characters, any of which can appear (once) in that location in the pattern. For example, `cat my_wordlist.dict | grep "^B[AEIOU]P;"` will find all 3-letter entries in the wordlist that start with B, end in P, and contain a middle vowel (BIP, BOP, and BAP, in my wordlist).

You can also specify character ranges in the brackets, using the dash (`-`). For example, `cat my_wordlist.dict | grep "^[S-V]...;[5-7].$"` will find all 4-letter entries in the wordlist that start with S, T, U, or V, and have two-digit scores where the first digit is 5, 6 or 7 (i.e., scores between 50 and 79).

You can specify a group of characters to *exclude* by putting a caret (`^`) after the opening bracket. For example, `cat my_wordlist.dict | grep "^B[^AEIOU]G;[^1-4].$"` will find all 3-letter entries in the wordlist that start with B, end in P, **do not** have a middle vowel, and have 2-character scores that **do not** start with 1, 2, 3, or 4 (i.e., scores of 50 or more). In my wordlist, this produces only the entry BMP. 

> ⚠️ Do not confuse this caret with the one outside the bracket, which indicates the start of a line (see above). ⚠️

##### Count Specifiers: `*`, `+`, `?`, `{}`
You can specify the desired number of repetitions of a character (or "one of" group) by following it with one of the following:
 - `*` means zero or more repititions, for example `grep "C[AEIOU]*T"` will find entries containing the letters C and T separated only by zero or more vowels, so it will find SCOOTER, INTERSECT, CAT, COAUTHOR etc. 
 - `\+` means one or more repititions, for example `grep "C[AEIOU]\+T"` will find SCOOTER, CAT, and COAUTHOR, but not INTERSECT.
 - `\?` means zero or one repititions, for example `grep "C[AEIOU]\?T"` will find CAT and INTERSECT, but not SCOOTER or COAUTHOR.
 - `\{N\}` (where N is a number) means exactly N repititions, for example `grep "C[AEIOU]\{3\}T"` will find COAUTHOR, but not the rest. You can also specify a range using `\{N,M\}` (where N and M are both numbers). For example `grep "C[AEIOU]\{2,3\}T"` will find SCOOTER and COAUTHOR, but not CAT or INTERSECT.

> ⚠️ Note the backslashes in the last 3 entries, but not for `*` or other symbols above. Although the format of regular expressions is pretty standard, there are some small variations between different applications, sites, and programming languages. In particular, they may differ in whether special characters are treated literally by default and symbolicly when prefixed with a `\`, or vise versa. For examples, in some implementations, `+` will mean the plus character, and `\+` will mean "one or more repetitions of the previous character" (as above), and in some it will be the other way around. This can be frustrating when you first encounter it, and it may take some trial and error to figure out. ⚠️  

> 📖 Further Reading: (This site)[https://regex101.com/] lets you test your regular expressions as you create them, explaining what's going on as you type.

### Changing Text with `sed`

## Organizing Output
### The `sort` Command 
The `sort` command is used to sort lines in a file. By default, it sorts in case-sensitive alphabetically ascending order. When sorting numbers, use the `-n` argument (so that "10" with come after "2"). To sort in descending order, use the `-r` (for "reverse") argument. To ignore case, use the `-f` argument.

Combining the all the above, you can find all the 10-letter entries in the wordlist containing the sequence "GEM", sort them in descending order of score, and print the top 10 with the following command:
```
cat my_wordlist.dict | grep "^.\{10\};" | grep "GEM" |  cut -d ";" -f "2,1" --output-delimiter " " | sort -r -n | head
``` 

### The `uniq` Command



