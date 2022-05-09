This lab is  created by ghanimah.com (canadian cyber security online plaform for specially lab). 

NOTE: I have performed lab provided by ghanimah lab in order to gain live practical experience. 

What is Masscan ?

Masscan is a network port scanner, similar in many ways to the well-known Nmap command. The goal of Masscan, however, is to enable security researchers to run port scans on large swathes of the Internet as quickly as possible.

Asynchronous transmission means the scanner doesn't have to wait for replies before sending out probes. masscan was created for the sole purpose of scanning the entire internet as fast as possible, according to its author Robert Graham, this can be done in less than 6 minutes at around 10 million packets per second.

Here is given some common scan type through Masscan.

masscan -p 445,139  ipaddress/24  -e tun0 
masscan -p 80  ipaddress/24 -e tun0 
masscan -p 1433  ipaddress -e tun0 
masscan -p 1433,80,445 ipaddress,ip address --rate=1000 -e tun0 
masscan -p 1433,80,445 ipaddress,ipaddress,ipaddress --rate=1000 -e tun0 -oX file.xml


Regards
Jamal H. Shah
