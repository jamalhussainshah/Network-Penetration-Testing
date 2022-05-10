 This lab is created by ghanimah.com (Canadian Cyber security online practice plafform) for education purpose .
 
 
 Banner Grabbing with Netcat

The first step in enumerating a VoIP network involves a technique called banner grabbing   or banner scraping . Banner grabbing is simply a method of connecting to a port on a remote target to identify more information about the associated service running on that port. Banner grabbing is one of the easiest and highest yield attack methods that hackers employ to inventory your VoIP applications and hardware. By connecting to most standard services and applications, they can glean the specific service type (for example, Apache HTTPd, Microsoft IIS, and so on), the service version (for example, Apache HTTPd 1.3.37, Microsoft IIS 6.0, and so on), and tons of other useful information about the target. 




Banner grabbing is a technique used to gain information about a computer system on a network and the services running on its open ports. Administrators can use this to take inventory of the systems and services on their network.

 Countermeasurs Banner Grabbing Countermeasures

There's really not much you can do to prevent simple banner grabbing and service identification. Because of the open-source nature of some applications, such as Asterisk or SER or Apache, you can take an extreme approach and hack the source code to change the advertised banners. This is not a long- lasting resolution, however, and will rarely stop a determined hacker who has other techniques at her disposal.

The best solution is to constantly upgrade your applications and services with the latest updates available. Also, you should make sure to disable those services that are not needed in your VoIP environment; for instance, there's probably no good reason to leave telnet services running on your VoIP phone or PBX.

If and whenever possible, restrict access to the remaining administrative services to specific IP addresses. For example, if an administrative web interface to your Asterisk server listens on TCP port 8111, then apply the appropriate firewall or network switch rules to ensure outsiders cannot arbitrarily connect to that port with their browser. 


Attached some asigned practical snapshot. 

Jamal H. Shah
