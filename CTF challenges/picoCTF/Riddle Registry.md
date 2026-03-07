# Riddle Registry – CTF Write-Up

<br/>

## Description
This challenge provides a downloadable PDF file that appears to contain nothing but gibberish. The description hints that the visible content is a decoy and that the real flag is hidden within the file’s metadata.
<br> [Access the challenge](https://play.picoctf.org/practice/challenge/530?page=1&search=riddle)

## Objective
The goal of this challenge was to retrieve the flag from the provided PDF file. The hints indicated that the flag would not appear in human-readable form and would likely be hidden within the file’s metadata.

## Solution
1. Click the provided link in the challenge and download the PDF file to your local system.
2. Open the PDF and review its contents to confirm that it only contains gibberish and no obvious hints.
3. Try selecting the text within the PDF to check for any hidden plain-text content.
4. Since the hints suggest looking beyond the visible text, inspect the file metadata using one of the following methods.

> ### Method 1: Metadata using the GUI
> - Open your Downloads folder and locate the downloaded file named `confidential.pdf`.
> - Right-click the file to open the context menu.
> - Select `Properties`.
> - Navigate to `Document Properties` to view the metadata.

> ### Method 2: Metadata using the CLI (Linux)
> - We will use the open-source utility `exiftool` to read the metadata of the PDF document.
> - To download the utility, run the appropriate command for your distribution:
>
> - Ubuntu / Debian-based distributions:
> ```bash
> sudo apt install libimage-exiftool-perl
> ```
> 
> ```bash
> sudo apt install exiftool
> ```
>
> - RHEL-based distributions:
> ```bash
> sudo dnf install perl-Image-ExifTool
> ```
>
> - Arch-based distributions:
> ```bash
> sudo pacman -S perl-image-exiftool
> ```
>
> - Once the utility is installed, navigate to your Downloads folder using `ls` and `cd`.
> - Run the following command to view the metadata of the PDF:
> ```bash
> exiftool confidential.pdf
> ```
> - The file metadata will now be displayed in the terminal.

5. Among the metadata fields, the `Author` field contains a suspicious string that could potentially be the flag:
```bash
Author: cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9lZTQ1NDk1MH0=
```
6. This string is Base64 encoded, identified by the following characteristics:
> - **Character Set:** It uses alphanumeric characters (A-Z, a-z, 0-9) and may include `+` or `/`.
> - **Padding:** The `=` sign at the end is a standard padding character used in Base64 to ensure the string length is a multiple of four.
> - **Case Sensitivity:** The mix of upper and lower-case letters is typical for this encoding.
7. To decode the string, use the built-in Linux base64 utility:
```bash
echo "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9lZTQ1NDk1MH0=" | base64 -d
```
> - **echo**   : Prints the encoded string so the system can grab it.
> - **|**      : Acts as a bridge, funneling the output of echo directly into the next command.
> - **base64** : Calls the Linux utility responsible for handling Base64 data.
> - **-d**     : Invokes the decoder.
8. Resulting Flag:
```bash
picoCTF{puzzl3d_m3tadata_f0und!_ee454950}  
```
