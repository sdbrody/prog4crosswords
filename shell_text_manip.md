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

### Changing Text with `sed`

## Organizing Output
### The `sort` Command 
The `sort` command is used to sort lines in a file. By default, it sorts in case-sensitive alphabetically ascending order. When sorting numbers, use the `-n` argument (so that "10" with come after "2"). To sort in descending order, use the `-r` (for "reverse") argument. To ignore case, use the `-f` argument.

Combining the all the above, you can find all the 10-letter entries in the wordlist containing the sequence "GEM", sort them in descending order of score, and print the top 10 with the following command:
```
cat my_wordlist.dict | grep "^.\{10\};" | grep "GEM" |  cut -d ";" -f "2,1" --output-delimiter " " | sort -r -n | head
``` 

### The `uniq` Command



