
```bash
# Printing the maximum element in a text with numbers
...| sort -nr | head -n1

# Printing the minimum elemnt in a text with numbers

...| sort -r | head -n1

# Sorting ocurrences, group and print the 5 largest occurences
ls -l | cut -f1 | sort | uniq -c | sort -nr | head -n5

# List fields ending in a even number
ls chapter*[02468] 


# Remove files safely with pattern matching\
# Evaluate the pattern you want to use rm with
ls *.txt # you can also replace it with head 
# Looks good? Go ahead and remove it
rm !$
 
```
