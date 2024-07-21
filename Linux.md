## Bash script template

```
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

```Note: ls is aware of whether the output is printed to the screen or piped. When piped, the output is formatted in a single column

$ ls | wc -l
4 
## ls prints
myf1
myf2
myf3

```

### head
useful to peak at the beginning of files without caring for the rest e.g 
```head -n3 my file
hi
hi
hi
```

### cut
prints one or more field columns in a file. the option `-f` defines a field as a sequence of words delimited by a tab character.

