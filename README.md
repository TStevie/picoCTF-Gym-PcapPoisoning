# picoCTF-Gym-PcapPoisoning
Writeup for medium difficulty forensic challenge PcapPoisoning

## What's the Goal?
From picoCTF - How about some hide and seek heh? Download this file and find the flag.

## Steps I used to Solve
1. I immediately noticed the file was a pcap (packet capture) file that I usually associate with Wireshark. I went ahead and opened the pcap within Wireshark and noticed the address of 172.16.0.2 sent a login request over FTP (file transfer protocol).
2. I threw the file into Network Miner as well to gather as much information on the hosts as I could before digging too far into Wireshark. ![image](https://github.com/user-attachments/assets/abf10432-673c-45fe-b40d-98bec4d160a4)
