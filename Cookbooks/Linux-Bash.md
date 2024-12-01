
```bash
# Printing the maximum element in a text with numbers
...| sort -nr | head -n1

# Printing the minimum elemnt in a text with numbers

...| sort -r | head -n1

# Sorting ocurrences, group and print the 5 largest occurences
ls -l | cut -f1 | sort | uniq -c | sort -nr | head -n5

# List fields ending in a even number
ls chapter*[02468] 


# Remove files safely with pattern matching
# Evaluate the pattern you want to use rm with
ls *.txt # you can also replace it with head 
# Looks good? Go ahead and remove it
rm !$


## consider the following command
ls /my/very/long/directory/that/

# wanna reference the previous argument? you can do so with !$
v !$

# wanna reference the first argument instead of typying it out? use !#:1 and then press tab
ls /my/very/long/directory/that/ !#:1

# Wanna reference the argument of the previous command? do !:1
ls /my/very/long/dir
cp file1.txt !:1 # expands to /my/very/long/dir

# Say you have a very long long command and you want to replace a word
ls -l | cut -f1 | sort | uniq -c | sort -nr | head -n5 # replace with eza
# You can do that by doing ^word_to_replace^new_word
^ls^eza

# say you want to return to a previous directory you were at
# current dir is /etc/conf
cd # now i am at ~ 
cd - # takes me back to /etc/conf

# nesting, say you want to create a directory with multiple directories
mkdir -p mydir/{dir1,dir2,dir3} # creates mydir containing dir1, dir2, dir2 as subdirectories
```

