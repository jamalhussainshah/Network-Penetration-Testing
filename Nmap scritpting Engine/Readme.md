
### Nmap Scripting Engine (NSE)

The Nmap Scripting Engine (NSE) is one of Nmap's most powerful and flexible features. It allows users to write (and share) simple scripts to automate a wide variety of networking tasks. Those scripts are then executed in parallel with the speed and efficiency you expect from Nmap. Users can rely on the growing and diverse set of scripts distributed with Nmap, or write their own to meet custom needs.

We designed NSE to be versatile, with the following tasks in mind:

Network discovery

This is Nmap's bread and butter. Examples include looking up whois data based on the target domain, querying ARIN, RIPE, or APNIC for the target IP to determine ownership, performing identd lookups on open ports, SNMP queries, and listing available NFS/SMB/RPC shares and services.
More sophisticated version detection


The Nmap version detection system  is able to recognize thousands of different services through its probe and regular expression signature based matching system, but it cannot recognize everything. For example, identifying the Skype v2 service requires two independent probes, which version detection isn't flexible enough to handle. Nmap could also recognize more SNMP services if it tried a few hundred different community names by brute force. Neither of these tasks are well suited to traditional Nmap version detection, but both are easily accomplished with NSE. For these reasons, version detection now calls NSE by default to handle some tricky services. This is described in the section called “Version Detection Using NSE”.
Vulnerability detection

When a new vulnerability is discovered, you often want to scan your networks quickly to identify vulnerable systems before the bad guys do. While Nmap isn't a comprehensive vulnerability scanner, NSE is powerful enough to handle even demanding vulnerability checks. When the Heartbleed bug affected hundreds of thousands of systems worldwide, Nmap's developers responded with the ssl-heartbleed detection script within 2 days. Many vulnerability detection scripts are already available and we plan to distribute more as they are written. 
Backdoor detection

Many attackers and some automated worms leave backdoors to enable later reentry. Some of these can be detected by Nmap's regular expression based version detection, but more complex worms and backdoors require NSE's advanced capabilities to reliably detect. NSE has been used to detect the Double Pulsar NSA backdoor in SMB and backdoored versions of UnrealIRCd, vsftpd, and ProFTPd. 
Vulnerability exploitation

As a general scripting language, NSE can even be used to exploit vulnerabilities rather than just find them. The capability to add custom exploit scripts may be valuable for some people (particularly penetration testers), though we aren't planning to turn Nmap into an exploitation framework such as Metasploit. 

These listed items were our initial goals, and we expect Nmap users to come up with even more inventive uses for NSE.

Scripts are written in the embedded Lua programming language, version 5.3. The language itself is well documented in the books Programming in Lua, Fourth Edition and Lua 5.2 Reference Manual. The reference manual, updated for Lua 5.3, is also freely available online, as is the first edition of Programming in Lua. Given the availability of these excellent general Lua programming references, this document only covers aspects and extensions specific to Nmap's scripting engine.

NSE is activated with the -sC option (or --script if you wish to specify a custom set of scripts) and results are integrated into Nmap normal and XML output.

A typical script scan is shown in the Example 9.1. Service scripts producing output in this example are ssh-hostkey, which provides the system's RSA and DSA SSH keys, and rpcinfo, which queries portmapper to enumerate available services. The only host script producing output in this example is smb-os-discovery, which collects a variety of information from SMB servers. Nmap discovered all of this information in a third of a second.
Example 9.1. Typical NSE output

![Screenshot_2022-09-01_12_46_59](https://user-images.githubusercontent.com/95676591/187862442-1d993f03-4952-435c-8934-bf80d4a3b280.png)

![Screenshot_2022-09-01_12_46_39](https://user-images.githubusercontent.com/95676591/187862482-ae2f3e84-a64a-479f-b2b3-23e2bd30cdc7.png)

![Screenshot_2022-09-01_12_47_14](https://user-images.githubusercontent.com/95676591/187862602-2ea23e23-7756-4e75-9c30-8ca8b191ac80.png)





