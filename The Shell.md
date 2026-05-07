---
title: The Shell

---

# Day1 The Shell
> aka the terminal
- textual interface to the computer
- a program on the computer that lets u inputs commands and outputs 
- shell runs in the context of a terminal
## Born Again Shell: bash
> based on Linux
- `[A_Username@HostNameOfTheMachine:~]$`
prompt
`~`: the location the user is at in the file system, e.g. `~`: home directory
`$`: u are not the admin of the machine
- ```man AProgramName```
`man`: the command for manual of the program
- ```cd ADirectory```
`cd`: change directory
- relative path of a directory: 
`[user@machine:~] cd /one/two/three` -> `[user@machine:/one/two] cd ./three`
    - `.`: current directory
    - `..`: parent directory
`[user@machine:/one] cd ./two/.././two/..` -> `[user@machine:/one] `
- ```$PATH```
`PATH`: a variable that outputs the directory of the file in the computer
- ```ls ADirectory```
`ls`: LiSt all the content in the directory
- ```cat AFile```
`cat`: output the content of the file
- `grep Something File`or `grep -r Something Directory`
`grep`: search file/directory contain string Something
- `>` and `<`
可以看作赋值
`[] date
Mon Mar 14 16:10
[] date >time.txt
[] cat <time.txt
Mon Mar 14 16:10
[] date >>time.txt
[] cat time.txt
Mon Mar 14 16:10
Mon Mar 14 16:12`
- `if; then`
`if grep 14 time.txt; then echo "it's 14"
- `fi` to end `if`
- `while; do`
`while grep 1 time.txt; do echo "here's 1; sleep 10"` sleep for 10 seconds for one lop
- `for` loop
`for ... in ... ; do ...`

- dashes e.g. `ls -a` or `ls --all`
dashes are called "flags" for s functions in the manual, usually order does not matter

- "globbing" allows the Shell to automatically expand "wildcards" into a list of matching file paths before a command runs
e.g. core "wildcards"
    - asterisk `*`: matches any number of characters, including zero character
    e.g.`*.txt`matches all files ending in `.txt` 
    - question mark `?`: matches exactly one single character
    e.g. `image?.jpg` matches `image1.jpg` but not `image12.jpg`
    - square brackets `[]`: matches any one character from a defined set or range
    e.g. `file[1-3].log` matches `file1.log`, `file2.log`, or `file3.log`