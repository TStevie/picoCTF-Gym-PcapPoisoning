# picoCTF-Gym-PcapPoisoning
Writeup for medium difficulty forensic challenge PcapPoisoning

## What's the Goal?
From picoCTF - How about some hide and seek heh? Download this file and find the flag.

## Steps I used to Solve
1. I immediately noticed the file was a pcap (packet capture) file that I usually associate with Wireshark. I went ahead and opened the pcap within Wireshark and noticed the address of 172.16.0.2 sent a login request over FTP (file transfer protocol).
2. I threw the file into Network Miner as well to gather as much information on the hosts as I could before digging too far into Wireshark. ![image](https://github.com/user-attachments/assets/abf10432-673c-45fe-b40d-98bec4d160a4)
3. We notice that the 172.16.0.2 address is running MacOS, and that host 10.253.0.6 is a server. Let's filter this into Network Miner's sessions: ![image](https://github.com/user-attachments/assets/b2bc1307-bb1a-4f84-b675-e15cab6a8653)
4. I see there's two sessions from our 172 host to the server, and two from another MacOS host to the server. I then decided to dig into these four sessions. Here I switch to Wireshark.
5. Since I know the frame numbers, I can find what I'm interested in much quicker. Frame 2 is where I start and see a SYN request sent to the server over port 22 (SSH) ![image](https://github.com/user-attachments/assets/625049e7-ff09-4713-aa84-1bb6e0eb01c7)
6. The fourth frame is what I initially noticed first, the attempted login over FTP from our 172.16.0.2 host. ![image](https://github.com/user-attachments/assets/8589a09e-5bbc-402e-aea9-12750edab2a7)
7. I then find frame 507, which is color coded from Wireshark's default settings as a "Bad TCP". Upon expanding the SEQ/ACK analysis and then the TCP Analysis Flags, I see this rule was applied because it's a suspected RTO (retransmission) from frame 4.
8. Within the packet bytes section on frame 507, we can see the flag we're searching for. ![image](https://github.com/user-attachments/assets/38177e13-b2d8-4cfc-bf9b-6ec4b81e4663)

## Quicker Version
When in Wireshark or Network Miner, throw a "picoCTF" in the string filter and search, voila ![image](https://github.com/user-attachments/assets/ea7b96dc-fa12-4850-a45b-ab0e99a4402a)

