---
description: How to build bash oneliners
---

# BashWars

### grep

#### Search string without case sensative

```bash
grep -i 'example' input.txt
```

#### Counting the number of matches

```bash
grep -c 'example' input.txt
```

#### Search with regex

```bash
grep -E 'example[0-9]+' input.txt
```

#### Printing strings without matches

```bash
grep -v 'example' input.txt
```



### cut

#### Retrieving characters in a range&#x20;

To extract the fifth through tenth characters from each string:

```bash
cut -c 5-10 input.txt
```

#### Extracting fields using a delimiter&#x20;

To extract the second field, where the fields are separated by commas:

```bash
cut -d ',' -f 2 input.txt
```



### sort

#### Sort strings alphabetically&#x20;

```bash
sort input.txt
```

#### To sort strings in reverse order:

```bash
sort -r input.txt
```

#### Sorting numeric values

```bash
sort -n input.txt
```

#### Removing duplicates when sorting

```bash
sort -u input.txt
```



### uniq

#### Remove duplicate strings

```sh
uniq input.txt
```

#### Count duplicate strings

```sh
uniq -c input.txt
```



### tr

#### Replacing characters

To replace all colons to spaces:

```sh
tr ':' ' ' < input.txt
```

#### Remove characters

To remove all numbers:

```sh
tr -d '0-9' < input.txt
```

#### Case conversion

To convert all lowercase letters to uppercase:

```sh
tr 'a-z' 'A-Z' < input.txt
```



### head & tail

#### Printing the first N lines

To print first 10 strings in file:

```sh
head -n 10 input.txt
```

#### Printing the last N lines

To print last 10 strings in file:

```sh
tail -n 10 input.txt
```



### xargs

#### Passing arguments to a command

To pass a list of files to the rm command:

```sh
ls | xargs rm
```

#### Limiting the number of arguments

To pass only two arguments at a time:

```sh
ls | xargs -n 2 echo
```

#### Applying a command in parallel

To execute a command in parallel on each file:

```sh
ls | xargs -P 4 -n 1 echo
```



### find

#### Find file by name

To search for all files named file.txt in the current directory and subdirectories:

```sh
find . -name 'file.txt'
```

#### Find file by size

To search for all files larger than 1 MB:

```sh
find . -size +1M
```

#### 3. Find and execute command

To delete all file with .tmp extension:

```sh
find . -name '*.tmp' -exec rm {} \;
```



### wc

#### Count strings in file

```sh
wc -l input.txt
```

#### Count word in file

```sh
wc -w input.txt
```

#### Count symbols in file

```sh
wc -m input.txt
```



### AWK

#### Take info from output by column

```bash
cat file.txt | awk '{print #1}'
```

#### Count strings in file

```bash
awk 'END {print NR}' file.txt
```

#### Delete empty strings in file

```bash
awk 'NF > 0' file.txt
```

#### Sum column values&#x20;

To sum the values ​​in a specific column (for example, the third column):

```bash
awk '{sum += $3} END {print sum}' file.txt
```

#### Counting unique values ​​in a column&#x20;

To count the number of unique values ​​in the first column:

```bash
awk '!seen[$1]++ {unique++} END {print unique}' file.txt
```



### sed

#### Replacing text&#x20;

To replace all occurrences of the word "oldtext" with "newtext":

```bash
sed 's/oldtext/newtext/g' file.txt
```

#### Delete strings

To delete lines containing a specific word, such as "delete":

```bash
sed '/delete/d' input.txt
```

#### Inserting text after a line&#x20;

To insert the **line** "Inserted text" after each line containing the word "pattern":

```bash
sed '/pattern/a\Inserted text' file.txt
```

To insert the **line** "Inserted text" before each line containing the word "pattern":

```bash
sed '/pattern/i\Inserted text' file.txt
```

#### Replace text only on certain lines&#x20;

To replace the text "oldtext" with "newtext" only on lines containing the word "pattern":

```bash
sed '/pattern/s/oldtext/newtext/g' file.txt
```

#### Removing the first N rows&#x20;

To remove the first 5 lines from a file:

```bash
sed '1,5d' file.txt
```

#### Printing Specific Strings&#x20;

To output lines 10 to 20:

```bash
sed -n '10,20p' file.txt
```



### jq

#### Format string to json

```bash
cat file.txt | jq
```

#### Retrieving a value by key&#x20;

To extract the value for the name key from JSON:

```bash
jq '.name' file.json
```

To retrieve a value from a nested key name.age:

```bash
jq '.name.age' file.json
```

#### Filtering array elements&#x20;

To filter array elements where the age field is greater than 30:

```bash
jq '.people[] | select(.age > 30)' file.json
```

#### JSON structure conversion&#x20;

To change the JSON structure, for example to output only the name and age:

```bash
jq '.people[] | {name: .name, age: .age}' file.json
```

#### Retrieving all values ​​of a specific key&#x20;

To retrieve all id key values ​​from an array of objects:

```bash
jq '.items[].id' file.json
```

#### Counting elements in an array&#x20;

To count the number of elements in the items array:

```bash
jq '.items | length' file.json
```

#### Replacing values ​​in JSON&#x20;

To replace all status key values ​​with active:

```bash
jq '(.items[].status) |= "active"' file.json
```
