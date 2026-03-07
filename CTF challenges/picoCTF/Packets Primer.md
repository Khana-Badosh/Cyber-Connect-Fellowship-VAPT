# Packets Primer – CTF Write-Up

<br/>

## Description
Use packet analysis on the provided packet capture file to find the flag.
<br> [Access the challenge](https://play.picoctf.org/practice/challenge/286?page=1&search=pri)

## Objective
The goal of this challenge is to use a packet analysis software (e.g. Wireshark) to filter through network traffic, reconstruct data streams, and identify the specific packet containing the hidden flag.

## Solution

1. **Download the Capture:**
   Click the provided link in the challenge and download the `.pcap` file to your local system.

2. **Open the File in Wireshark:**
   Launch Wireshark and navigate to `File > Open`, then select the downloaded `.pcap` file.

3. **Analyze the Packet List:**
   Once the file is opened, there will be a list of captured packets.
   * **Observation:** You will notice packets 1, 2, and 3 have a `Length` of `0`. These are the "handshake" packets used to start a connection as indicated by the `[SYN] → [SYN, ACK] → [ACK]` sequence.
   * **The Target:** Look for a packet with a non-zero length. **Packet 4** stands out with a length of **60 bytes**.

<img src="https://github.com/user-attachments/assets/ba675ec5-3b95-4c98-ab90-cb2accef2d1d" alt="Wireshark Capture" style="width:100%; height:auto;">

4. **Inspect Packet 4:**
   Click on Packet 4. In the "Info" column, you will see `[PSH, ACK]`.
   
   > **What is a PSH (Push) Flag?**
   >
   > In TCP, the "Push" flag tells the receiving computer to stop buffering data and push it immediately to the application. In CTFs, this is a major hint that this packet contains the actual payload.

5. **Follow the Data Stream:**
   Right-click on Packet 4 and select `Follow > TCP Stream`.
   
   > **What does "Follow Stream" do?**
   >
   > A network conversation is often broken into many small packets. "Follow Stream" is like taking a pile of individual pages and binding them back into a book. It ignores the technical headers (the "envelope") and shows you only the text (the "letter") being sent between the two computers.

6. **Extract the Flag:**
   A new window will pop up showing the reconstructed text of the conversation. The flag will be visible here in plaintext.
```bash
p i c o C T F { p 4 c k 3 7 _ 5 h 4 r k _ c e c c a a 7 f }
```
1. **Clean the Flag Format:**
   Although the flag appears with spaces in the Stream view, these spaces must be removed for the flag to be valid. This spacing often occurs due to the way specific protocols (like UTF-16 encoding) represent characters in the packet.
```bash
picoCTF{p4ck37_5h4rk_ceccaa7f}
```

## Additional Learning

#### 1. The Three-Way Handshake (Packets 1-3)
> Before data is sent, the computers perform a handshake `[SYN] → [SYN, ACK] → [ACK]`. These packets always have a length of `0` because they are just introductions and don't carry any actual data.
#### 2. ARP Packets (Packets 6-9)
> You may notice yellow-colored packets labeled ARP (Address Resolution Protocol). These packets are how a computer asks, "Who has this IP address?" so it can find the physical hardware MAC address of the destination. These are background "plumbing" packets and almost never contain the flag.
#### 3. Why 'Length 0' matters
> A packet with `Len=0` means the packet is empty. While it's possible to hide data in the headers of such a packet, usually beginner challenges store the flag in the payload, which requires a `Len` greater than 0.