# Find your shell
- `echo $0`
- `cat /etc/shells` -> Available shells

# Types of Linux Shells
## Gui Based
- Gnome
- KDE
## Command Line
- sh
- bash (born again shell), offers extra features over sh
- csh, tcsh
- ksh

# Shell Scripting
A shell script is an executable file containing multiple  shell commands that are executed sequentially.

- The file can contain:
    - Shell (#!/bin/bash)
    - Comments (# comments)
    - Commands (echo, cp, grep)
    - Statements (if, while, for etc.)

* Shell script should have executable permissions.
* Shell script has to be called from absolute path
* If called from current location then `./script.bash`

## Defining Variables

- No space between variable and the value

```
name="Cihad"
echo "Hello, my name is $name"
```

## Input / Output
Two commonds
- read 
- echo

```
What is your name?
read name
echo
echo "Hello $name, nice to meet you
```

If you want to assign a command to a variable, put space at the beginning and the end of the command
- a= hostname 

## if-then Scripts

***Check the variable***
```
#!/bin/bash

count=100
if [ $count -eq 100 ]
then
 echo Count is 100
else
 echo Count is not 100
fi
```

***Check if a file error.txt exist***
```
#!/bin/bash
clear
if [ -e /home/iafzal/error.txt ]
 then
 echo "File exist"
 else
 echo "File does not exist"
fi
```

***Check if a variable value is met***
```
#!/bin/bash
a=`date | awk '{print $1}'`
if [ "$a" == Mon ]
 then
 echo Today is $a
 else
 echo Today is not Monday
fi
```

***Check the response and then output***
```
#!/bin/bash
clear
echo
echo "What is your name?"
echo
read a
echo
echo Hello $a sir
echo
echo "Do you like working in IT? (y/n)"
read Like
echo
if [ "$Like" == y ]
then
echo You are cool
elif [ "$Like" == n ]
then
echo You should try IT, it’s a good field
echo
fi
```

***Other If statements***
```
If the output is either Monday or Tuesday
if [ “$a” = Monday ] || [ “$a” = Tuesday ]
Test if the error.txt file exist and its size is greater than zero
if test -s error.txt
if [ $? -eq 0 ] If input is equal to zero (0)
if [ -e /export/home/filename ] If file is there
if [ "$a" != "" ] If variable does not match
if [ error_code != "0" ] If file not equal to zero (0)
```


***Comparisons:***
```
-eq equal to for numbers
== equal to for letters
-ne not equal to
!== not equal to for letters
-lt less than
-le less than or equal to
-gt greater than
-ge greater than or equal to
```

***File Operations:***
```
-s file exists and is not empty
-f file exists and is not a directory
-d directory exists
-x file is executable
-w file is writable
-r file is readable
```

## for-loop Scripts

***Simple for loop output***
```
#!/bin/bash
for i in 1 2 3 4 5
do
echo "Welcome $i times"
done
```

```
#!/bin/bash
for i in eat run jump play
do
echo S
```

***for loop to create 5 files named 1-5***
```
#!/bin/bash
for i in {1..5}
do
 touch $i
done
```

***for loop to delete 5 files named 1-5***
```
#!/bin/bash
for i in {1..5}
do
 rm $i
done
```

***List all users one by one from /etc/passwd file***
```
#!/bin/bash
i=1
for username in `awk -F: '{print $1}' /etc/passwd`
do
echo "Username $((i++)) : $username"
done
```

## do-while Scripts

***Script to run for a number of times***
```
#!/bin/bash
c=1
while [ $c -le 5 ]
do
 echo "Welcone $c times"
 (( c++ ))
done
```

***Script to run for a number of seconds***
```
#!/bin/bash
count=0
num=10
while [ $count -lt 10 ]
do
 echo
 echo $num seconds left to stop this process $1
 echo
 sleep 1
num=`expr $num - 1`
count=`expr $count + 1`
done
echo
echo $1 process is stopped!!!
echo
```

## case Scripts

```
#!/bin/bash
echo
echo Please chose one of the options below
echo
echo 'a = Display Date and Time'
echo 'b = List file and directories'
echo 'c = List users logged in'
echo 'd = Check System uptime'
echo
 read choices
 case $choices in
a) date;;
b) ls;;
c) who;;
d) uptime;;
*) echo Invalid choice - Bye.
```