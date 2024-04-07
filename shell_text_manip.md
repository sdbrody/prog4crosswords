# Manipulating Text with BASH (Bourne Again SHell)

This chapter will discuss how to use the the features of BASH and its built-in tools to search through and modify text files. The focus will be on the use cases that come up when constructing crosswords. As in the previous chapter, I will not describe all of the options and possibilities of each tool, but will try to give useful pointers for further reading.


## Swapping and Deleting Characters with `tr`

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

> ⚠️ `tr` works on individual characters. `tr "hi" "yo"` will not replace "hi" with "yo", but instead will replace **all** h's with y's and all i's with o's! The same applies to deletion. ⚠️  

> 📖 Further Reading

## sort
## uniq
## cut
## grep
## sed






tr, sort, cut, grep, sed
