## Bash script template

```bash
#! /usr/bin/env bash # could also be zsh

set -o errexit # stop script if error is raised.
set -o nounset # raise an error if a variable is unset.
set -o pipetail # raise an error on a pipe failure.
```

## Basics

- Process := user facing unit, based on an executing of a program.
	- It is an abstraction used by the kernel of a group of hardware resources.
- Thread := unit of execution in the context of a process.
- Multithreading :=  `parallel` (NOT concurrent) execution of units, perhaps in multiple cpus.

### File Descriptors
In Linux, there are three file descriptors by default.
- 0 -> stdin
- 1 -> stdout
- 2 -> stderr 
- use `& >` to redirect both stdin and stderr to a file.
	- e.g `grep "example" & > output.log`
	- Similarly, you can redirect the stdout and stderr accordingly.
## Some useful shell commands
- To run a process in the bg -> append & 
	- e.g `grep "example" &`
- To run a process even if the shell is closed -> use `nohup`
	- e.g `nohup grep "example"` 
	- You can also achieve the same thing with `disown`.
		- TODO: write an example using disown
# Some useful tools 
- `kill` - make a process exit.
	- Challenge- could you write a small script that takes a process's name and kill it?
- `exa` - replacement for `ls` , it is written in rust.
	- Does this replacement enhance your workflow? Why?
- `bat` - replacement for cat.
- `rg` - replacement for `find , grep` (but I use ripgrep and fzf)
- Check out the modern-unix repo for more cool tools.
-  `date` - generate UNIX timestamps
- `less` - displays one page at a time for long text files
	- Too many files to display the permissions? you can use the pipe command to see a page at a time `ls -l | less`

## Some commands in depth
#### wc
Short for word count, displays the following information in the following order `lines, words, characters` . Note that wc counts newlines as a character.

You can tell wc to list the number of lines, words and characters only by passing the following flags `-l -w -c`

```bash
Note: ls is aware of whether the output is printed to the screen or piped. When piped, the output is formatted in a single column

$ ls | wc -l
4 
## ls prints
myf1
myf2
myf3

```

### head
useful to peak at the beginning of files without caring for the rest e.g 
``` bash
head -n3 my file
hi
hi
hi
```

### cut
prints one or more field columns in a file. the option `-f` defines a field as a sequence of words delimited by a tab character.
	- Use the option `-c` to isolate columns. e.g isolate the first column with `cut -c1`
	- You can specify a delimiter with the `-d` flag `cut -d: # specify : as delimeter`

### grep
Useful for findin text in a file, usage `grep <WORD_TO_SEARCH? <file>`
- use `-v` to do a reverse search (find ocurrences where the word is not present).
### sort 
Used to sort text alphabetically (by default) or numerically with the `-n` flag. Sorting is in ascending order (lower to greater) by default.
- reverse the order with `-r`.
- to tell grep to match **exactly** a word, use the `-w` flag. `grep -w skipper # matches words if and only if it is exactly skipper. Won't match words like firstskipper`  
### uniq
Detects repeated adjacent lines in a file, by default it removes dupes.
- For uniq to reduce fields to a single line, ocurrences must be next to each other
- To get the count of each occurence, use `-c` count `uniq -c `
- Useful for grouping (can be useful for grouping serial numbers or uuids)

# Pattern Matching and Shells in Linux
To preface this section, we define a _shell_ as an interface between the linux operation system and the user.
With this in mind, it is important to know what functionality is handled by the shell and which ones are by the command (e.g ls).

Take for example the following `grep Linux chapter*` . 

The `*` means to match any zero or more characters. This is however, not handled by `grep`, it is handled by the shell.  (it does not matches leading dots or directory slash)

To only match a single character use `?` e.g `grep chapter?`

You can also specify to match for specific characters in a set `grep chapter[12345]`
or even in a range of characters `grep chapter[1-5]` or characters `ls [A-Z]*.png`

IMPORTANT: Pattern Matching only applies to files and directory paths.

To evaluate env variables use $ . `$HOME`, this is evaluated by the shell and not the program.

In shell land, single quotes tell the shell to not evaluate special characters 
```bash
echo '$HOME'
$HOME

echo "My home is $HOME" # double quotes allow expansion
my home is /etc/home

```
### tr 
The tr command translates (or transforms) a sequence of characters to another `ls : "\n" #transform : to \n`

# Command History retrieval
There are three techniques
1. History cursor
- Common, use the arrow keys to navigate through the command history
- Gets tedious if the command you're looking for is far away

2. History expansion
- Shell feature
	- use `!!` to execute the last command executed
	- To execute the latest command that begins with a string use `!<string>` e.g `!grep # executes the latest grep command
	- To  search for the latest command (and execute) that contains a string anywhere, surround the string with question marks `!?grep?`
	- You can also execute a command based on its command id, to get the ids, use history `history | grep cat # list commands executing cat`. `use !<command_id>` to execute the command with the corresponding command_id. You can also execute commands using negative indexes `!-3` executes the command executed 3 commands ago.
	- To prevent running command blindly, use `:p` . e.g `:-3:p` this will print the command but not run it and also append the command to the history. If it looks good you can run `!! to run it.
- `!$` means, final word you typed in the previous command 
- You can also use `!*` to expand (and match) the arguments listed in the previous command.
- Use ctl-r to actiivate reverse history search
- To correct the latest command use carer notation `^jg^jpg` this corrects the first ocurrence of jg with jpg.