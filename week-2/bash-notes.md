**Week 2**  
# TASK - Bandit levels  
## Level 0  

*In this level task was to connect to the Bandit remote server*  

Command `ssh` is used to connect to the remote server. The `ssh` command provides a secure encrypted connection between two hosts over an insecure network. This connection can also be used for terminal access, file transfers, and for tunneling other applications.  

Informations:
```
Username: bandit0
Password: bandit0
Port: 2220
Host: bandit.labs.overthewire.org
```
Using this command we will connect to the remote server with unusual port 2220.
 ```
$ ssh bandit@bandit.labs.overthewire.org -p 2220
```

![Login](.//bandit-screenshots/LogIn.png)  

## Level 0-1

*In this level task is to find the password stored in **_readme_** file*

With command `ls` everything stored in particular directory will be listed. Hidden files will be listed using command `ls -la`. Command `cat` is used to display content of a file. With command `history` we will print all previously executed commands.

```
    $  ls
    $  cat readme
    $  history
```

![Level_0-1](.//bandit-screenshots/Level_0-1.png)

## Level 1-2

*In this level task is to find the password stored in a file called **_"-"_**.*  

Since **_"-"_** is special character we will need to provide path to the file.
```
     $  cat ./-
```

![Level_1-2](.//bandit-screenshots/Level_1-2.png)  

## Level 2-3  

*In this level task is to find the password stored in a file called **_spaces in this file name_***  

We can solve this task in 2 ways. Since file name contains spaces we can print this file putting the file name in quotes `" "` or adding backslash `\` after every word.

```
    $  cat "spaces in this filename" 
    OR
    $  cat spaces\ in\ this\ filename
```

![Level_2-3](.//bandit-screenshots/Level_2-3.png)

## Level 3-4  

*In this level task is to find the password stored in a hidden file in the **_inhere_** directory*  

We will use command `ls -la` to list all files.
```
    $  ls -la #list all files
    $  cd inhere/ #enter the "inhere" directory
    $  ls -la 
    $  cat .hidden #after listing all files (and hidden ones) we can print file we need
```
![Level_3-4](.//bandit-screenshots/Level_3-4.png)  

## Level 4-5

*In this level task is to find the password stored in the only human-readable file in **_inhere_** directory*  

Command `file` returns the data type found in that file. For example human readable files are **Unicode**, **ASCII**.  

```
    $  ls
    $  cd inhere/
    $  ls -la
    $  file ./*     #we will return data type of every file in this directory with  wildcard *
    $  cat ./-file07 
```
![Level_4-5](.//bandit-screenshots/Level_4-5.png)  

## Level 5-6  

*In this level task is to find the password stored in a file somewhere under the **_inhere_** directory with following properties:*
- human readable
- 1033 bytes in size
- not executable

Using the command `find .` we will search for a file in this directory and we will use given parametres to search for exact file.  
Parametres:  
`readable` - human readable  
`size` - size of file ("c" bytes)  
`executable` - search for executable file. If you need not executable we will use "!"

```
    $  ls
    $  cd inhere/
    $  find . -readable -size 1033c ! -executable
    $  cd maybehere07
    $  cat .file2
```  


![Level_5-6](.//bandit-screenshots/Level_5-6.png)  

## Level 6-7  

*In this level task is to find the password stored **_somewhere on the server_** and has following properties:*
- owned by user bandit7  
- owned by group bandit6  
- 33 bytes in size  

Using the command `find /` will search whole server, and we will give it following parameters:  
`user` - user of file  
`group` - group that belongs  
`size` - size of file ("c" for bytes)  

```
    $  find / -user bandit7 -group bandit6 -size 33c
    $  cat /var/lib/dpkg/info/bandit7.password
```

![Level_6-7](.//bandit-screenshots/Level_6-7.png)  

## Level 7-8  

*In this level task is to find the password in **_data.txt_** next to the word **millionth***  

Command `grep` is a string and pattern matching utility that displays matching lines from multiple files. (bing.com)  

```
    $  grep "millionth" data.txt   #type the word we search for and the file we are searching in
```

![Level_7-8](.//bandit-screenshots/Level_7-8.png)  

## Level 8-9  

*In this level task is to find the password in the file **data.txt** and is the only line of text that occurs only once*  

Command `sort` will sort the file, and command `uniq` will filter the input and print the output. We will use command `sort` with command `uniq` because `uniq` will drop repeated lines only if they are one to another. We need to sort file first, and then to find the line that occurs only once.  

```
    $  sort data.txt | uniq -u
```

![Level_8-9](.//bandit-screenshots/Level_8-9.png)  

## Level 9-10  

*In this level task is to find the password stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters*  

Command `string` will find human-readable strings inside the file.

```
    $  strings data.txt | grep ===
```  

![Level_9-10](.//bandit-screenshots/Level_9-10.png)  

## Level 10-11  

*In this level task is to find the password stored in the file **data.txt**, which contains base64 encoded data*

Command `base64` will encrypt or decrypt data from the file.  
Parameter `d` is used for decryption.  
```
    $  base64 -d data.txt
```

![Level_10-11](.//bandit-screenshots/Level_10-11.png)  

## Level 11-12  

*In this level task is to find the password stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions*  

**ROT13** ("rotate by 13 places", sometimes hyphenated ROT-13) is a simple letter substitution cipher that replaces a letter with the 13th letter after it in the latin alphabet. (bing.com)  

Command `tr` allows you to replace characters with some other characters.  
```
    $ tr <old_char> <new_char> 
```  

We need to replace every character in the alphabet with its 13th pair. 

```
    $  cat data.txt | tr "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz" "NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm"
```

![Level_11-12](.//bandit-screenshots/Level_11-12.png)