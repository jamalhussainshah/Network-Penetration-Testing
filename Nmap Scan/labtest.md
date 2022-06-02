
This lab is  created by ghanimah.com (canadian cyber security online plaform for specially lab). 

IMPORTANT: It is necessary to take permission in written from customer before scan through nmap to identify vulnerbility.

Nmap is now one of the core tools used by network administrators to map their networks. The program can be used to find live hosts on a network, perform port scanning, ping sweeps, OS detection, and version detection.

To view all unauthorized devices, you can tell Nmap to scan an entire subnet. NOTE: In penetration testing, you will rarely scan an entire network. Instead, you will only dive into targeted hosts in the network, as the process can be slow and unnecessary.

NOTE: I have performed lab provided by ghanimah lab in order to gain live practical experience. 

Some important commands of namp in order to find vulnerbility in the network system.

sudo nmap -O 172.30.2.36 
sudo nmap -O  --osscan-guess  172.30.2.36
sudo nmap -sV 172.30.2.36 

la -a /usr/share/nmap/scripts/
la -a /usr/share/nmap/scripts/ | grep http
nmap --script=http-auth.nse 172.30.2.44
nmap -p 80,21,23 172.30.2.0/24 172.30.3.0/24 172.30.4.0/24 --open

ls /usr/share/nmap/scripts/ | grep http   
nmap -p 80 --script=http-ntlm-info.nse    
nmap -p 80 --script=http-ntlm-info.nse 172.30.4.25
nmap -p 80 -sV --script=http-ntlm-info.nse 172.30.4.25
nmap -sC -T4 172.30.4.25
nmap --script="default.safe" 172.30.4.25
nmap -p --script="http-*" 172.30.4.25  
nmap -p --script="http-*" 172.30.4.25 


Jamal H.Shah
