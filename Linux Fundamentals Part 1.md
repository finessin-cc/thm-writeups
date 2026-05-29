# TryHackMe: Linux Fundamentals Part 1

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Linux Fundamentals          |
| Difficulty    | Beginner                    |
| Date          | May 26, 2021                |

## Task 1: Introduction

Welcome to the first part of the "Linux Fundamentals" room series. This room introduces the basics of Linux, focusing on essential commands and interaction with the terminal. The goal is to familiarize users with Linux fundamentals and prepare them for more advanced topics in subsequent parts.

## Task 2: A Bit of Background on Linux

### Where is Linux Used?

Linux is widely used in various domains including:

- Websites that users visit
- Car entertainment/control panels
- Point of Sale (PoS) systems
- Critical infrastructure such as traffic light controllers or industrial sensors

### Flavours of Linux

Linux is an umbrella term for multiple operating systems based on UNIX. Some common distributions include:

- **Ubuntu**: Popular for its extensibility, suitable for both servers and desktop environments
- **Debian**: Known for stability and reliability

Ubuntu Server can run on systems with as little as 512MB of RAM.

**Question:** What year was the first release of a Linux operating system?
- **Answer:** 1991

## Task 3: Interacting With Your First Linux Machine (In-Browser)

This room provides an interactive Ubuntu Linux machine accessible directly in the browser. Users must deploy the lab machine using the "Start Lab Machine" button.

## Task 4: Running Your First Few Commands

### Essential Commands

| Command   | Description                          |
|-----------|--------------------------------------|
| `echo`    | Output any text provided             |
| `whoami`  | Find out what user we're logged in as|

### Examples

```bash
tryhackme@linux1:~$ echo Hello
Hello
tryhackme@linux1:~$ echo "Hello Friend!"
Hello Friend!
tryhackme@linux1:~$ whoami
tryhackme
```

**Questions:**
- If we wanted to output the text "TryHackMe", what would our command be?
  - **Answer:** `echo TryHackMe`
- What is the username of who you're logged in as on your deployed Linux machine?
  - **Answer:** `tryhackme`

## Task 5: Interacting With the Filesystem

### Core Filesystem Commands

| Command | Full Name           |
|---------|---------------------|
| `ls`    | listing             |
| `cd`    | change directory    |
| `cat`   | concatenate         |
| `pwd`   | print working directory |

### Directory Navigation Example

```bash
tryhackme@linux1:~$ ls
'Important Files' 'My Documents' Notes Pictures
tryhackme@linux1:~/Pictures$ ls
dog_picture1.jpg dog_picture2.jpg dog_picture3.jpg dog_picture4.jpg
tryhackme@linux1:~/Documents$ ls
todo.txt
tryhackme@linux1:~/Documents$ cat todo.txt
Here's something important for me to do later!
tryhackme@linux1:~/Documents$ pwd
/home/tryhackme/Documents
```

**Questions:**
- On the Linux machine that you deploy, how many folders are there?
  - **Answer:** 4
- Which directory contains a file?
  - **Answer:** folder4
- What is the contents of this file?
  - **Answer:** Hello World!
- Use the cd command to navigate to this file and find out the new current working directory. What is the path?
  - **Answer:** `/home/tryhackme/folder4`

## Task 6: Searching for Files

### Using `find` Command

```bash
tryhackme@linux1:~$ find -name passwords.txt
./folder1/passwords.txt
tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt
```

### Using `grep` Command

```bash
tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
```

### Recursive Search with `grep`

```bash
grep -R "PRETTY_NAME" /etc/
/etc/os-release:PRETTY_NAME="Ubuntu"
```

**Question:** Use grep on "access.log" to find the flag that has a prefix of "THM". What is the flag?
- **Answer:** `THM{ACCESS}`

## Task 7: An Introduction to Shell Operators

### Shell Operators

| Symbol / Operator | Description                                         |
|-------------------|-----------------------------------------------------|
| `&`               | Run commands in the background                      |
| `&&`              | Combine multiple commands in one line               |
| `>`               | Redirect output to a file (overwrites content)      |
| `>>`              | Append output to a file                             |

### Examples

```bash
tryhackme@linux1:~$ echo hey > welcome
tryhackme@linux1:~$ cat welcome
hey
tryhackme@linux1:~$ echo hello >> welcome
tryhackme@linux1:~$ cat welcome
hey
hello
```

**Questions:**
- If we wanted to run a command in the background, what operator would we want to use?
  - **Answer:** `&`
- If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?
  - **Answer:** `echo password123 > passwords`
- Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be?
  - **Answer:** `echo tryhackme >> passwords`

## Task 8: Conclusions & Summaries

This room provided a comprehensive introduction to Linux fundamentals including:

- Understanding Linux's widespread usage
- Interacting with the first Linux machine
- Executing fundamental commands (`echo`, `whoami`)
- Navigating the filesystem (`ls`, `cd`, `cat`, `pwd`)
- Searching for files using `find` and `grep`
- Utilizing shell operators for enhanced functionality

These are the most essential functions that will be frequently used when interacting with Linux machines. The skills learned here form the foundation for more advanced Linux administration and cybersecurity tasks.
