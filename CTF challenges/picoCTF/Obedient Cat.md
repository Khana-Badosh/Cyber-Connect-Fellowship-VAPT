# Obedient Cat – CTF Write-Up

<br/>

## Description
This file has a flag in plain sight (aka "in-the-clear").  
[Access the challenge](https://play.picoctf.org/practice/challenge/147?page=1&search=ob)

## Objective
The goal of this challenge was to retrieve the flag from a downloadable file.

The description clearly states that the flag is "in-the-clear", meaning it is not encrypted, encoded, or hidden it is simply readable inside the file.

## Solution

### Method 1: Manual File Inspection
#### Step 1: Download the File
- Click the provided link in the challenge and download the file to your local system.
#### Step 2: Open the File
- Open the downloaded file using any text editor (Notepad, VS code etc).
- After opening the file, the flag is visible directly in plain text inside the file.
- Copy the flag and submit it.

### Method 2: Using Command Line / Terminal (Linux)
#### Step 1: Download the File
- Open your terminal and run:

```bash
wget <file_url>   
```
- This command stands for (World Wide Web + get), it is used to download files from the internet.
#### Step 2: Access the Contents of the File
- In the directory where the downloaded file is located, run the following command:
```bash
cat <filename>   
```
- The cat command stands for “concatenate”, but in most basic use cases, it is used to display the contents of a file in the terminal.
- You would now see a flag displayed in the terminal. 
- Copy the flag and submit it. 

## Additional Learning
The `man` command shows the manual for any Linux command. It explains what the command does, its options / flags, and usage examples. Use Space to scroll down, `b` to scroll up, and `q` to quit the manual. For example, `man cat` explains how to read and display file contents.
```bash
# View the manual for the wget command
man wget

# View the manual for the cat command
man cat

# View the manual for the ls command
man ls
```
