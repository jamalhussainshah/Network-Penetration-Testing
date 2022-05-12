This lab in created by ghanimah.com (The world best cyber security learning platform).

IMPORTANT: This tool is used in order to find vulnerbility of network and its necessary to take first permission in written from your customer. 


Empire is a post-exploitation framework used for the management of compromised victim hosts. Empire offers a range of command and control modules allowing command execution and data exfiltration capabilities. Empire's HTTP-based stagers initiate C2 connections to the attacking host via HTTP requests.


PowerShell Empire, an open source penetration testing framework, is used by malicious actors to conduct post-exploitation activity on compromised networks prior to delivering the BitPaymer ransomware payload.

Empire: PowerShell & Python3 Post-Exploitation Framework
After entering the main menu, the user will see the number of active agents, listeners and loaded modules. The first step normally is to set-up a local listener through the listener management menu. After this, the user can choose to set up various stagers including dlls, macros, one-liners and more. The user can also choose to perform commands through agents and check which infiltrated systems are online. Lastly, the user has the option to execute modules on different agents

Features:
includes a pure-PowerShell 2.0 Windows agent
Compatible with Python 3.x Linux/OS X agents
Deploy Post-Exploitation modules from keyloggers to Mimikatz.
Designed in a way to avoid detection


Mimikatz is a Windows x32/x64 program to extract passwords, hash, PINs, and Kerberos tickets from memory. It is used as an attack tool against Windows clients, allowing the extraction of cleartext passwords and password hashes from memory.

Mimikatz is an open-source application that allows users to view and save authentication credentials like Kerberos tickets. Benjamin Delpy continues to lead Mimikatz developments, so the toolset works with the current release of Windows and includes the most up-to-date attacks


What is a situational awareness system?
Situation awareness system (SAS) are security systems that help in collecting, visualizing, and analyzing information related to the surrounding and remote environment to facilitate surveillance as well as security.

SITUATIONAL AWARENESS
The situational awareness modules in Empire allow you to gather additional information about the environment after you have compromised your initial host and established an agent. There are lots of situational awareness modules which help gather data on the compromised host, the network the host resides on, as well as the Active Directory environment (if on a domain joined system).



We’re going to focus on network and Active Directory modules, both of which will help you to eventually move to other systems in the environment.    

Network:

One of the most basic tasks that Empire allows you to do once you have compromised a host is to scan for open ports on other hosts on the network. This is crucial to identifying other live systems and potential targets for exploitation or lateral movement. To perform a port scan, you can use the network/portscan module. There are a number of options you can configure to help drill down your target hosts and ports.

                   

Empire’s network/portscan module options.
                                                                                                                                                              
         

Once you have configured the module to scan the hosts and ports you desire, running the execute command will start the module. Typically, we like to scan for specific ports which commonly have misconfigured services running on them. For example, to scan for systems which might have misconfigured web server technologies like Tomcat or Jenkins, you could scan the network for ports 80, 443, and 8080. After the module is finished running it will return the output of any systems it found with the ports you specified open. Hopefully you find some additional targets go after!

Active Directory:

In addition to generic network discovery and enumeration modules, Empire comes with a number of other modules which focus on enumerating the Active Directory environment of a compromised host. Among the most useful of these are the modules that focus on group and user enumeration. These will help identify important Active Directory groups and users which might be valuable for you to target to gain access to specific resources.

                   

PowerView based modules which focus on Active Directory enumeration.

Directory enumeration.                                
         

PRIVILEGE ESCALATION
While many enumeration tasks can be done without any special privileges, you will often want to perform actions that require elevated privileges on the compromised system (such as dumping credentials from memory). If your current agent is not running as a user with admin rights, Empire has some privilege escalation modules at your disposal.    

                   
Empire’s privilege escalation modules.
                              
         

PowerUp:

Empire has a number of modules related to the PowerShell privilege escalation script, PowerUp. One module in particular, powerup/allchecks, will run a large number of checks on your host for common misconfigurations which could allow for privilege escalation. The output from this module tends to be a bit verbose, and sometimes it will return false positives. Be patient and work through your various options here! If you’re lucky, this module could identify clear text administrative credentials or trivially exploited privilege escalation issues.  

BypassUAC:

Sometimes, your agent will be running as a user who has admin rights but the agent is not running in an elevated process. In this scenario you can attempt to elevate the agent to administrative privileges by running the bypassuac module. This module attempts to establish a new agent in a high integrity process.

Specific Vulnerabilities:

There are also a number of privesc modules which will check for specific known vulnerabilities. For example, the privesc/ms16-032 module will attempt to exploit a known Windows kernel vulnerability. These modules typically result in a new agent running as SYSTEM if successful.

CREDENTIAL GATHERING
After gaining Administrator privileges, one of the most important and common tasks to perform is to gather other credentials from the compromised system. Benjamin Delpy’s Mimikatz is probably the most well known utility for this, and Empire has it ported into several different credential gathering modules.

                   

Empire’s credential gathering modules.
                                                                                                
         

These modules will attempt to gather credentials, either in plain text or as hashes, and store them in Empire’s local credential database. These can then be used to move laterally to other systems or to establish agents with different privileges. The most basic example of a credential gathering module is to run the built-in mimikatz command which will dump any cached credentials on the system.

For a more targeted approach, you can use modules such as DCSync to get the hashes of specific users identified through the situational awareness module. DCSync requires Domain Admin privileges but will return the hash of a specified user in the current domain. This is particularly useful for gaining access to specific applications or data which only particular users have access to.

                   

Options for the mimikatz/dcsync module.
                                                                                                                                                                        

After gaining any hashed credentials through one of the credential gathering modules, you’ll need a way to use that hash to assume the privileges of its user account. You can accomplish this through the Mimikatz pass-the-hash (pth) module. This module will create a new process using the hash provided which can be injected into to establish a new agent with the privileges of that process/user. An important detail to note for this module is that it will create an interactive process. So, if you execute this module while running as a user who is currently logged on it will spawn a visible cmd.exe process by default.  

LATERAL MOVEMENT  
After gaining some situational awareness of the network, escalating to Administrator and gathering credentials, you will probably be ready to move to other systems in the environment. To accomplish this, you’ll use one of Empire’s lateral movement modules.

                   

Empire’s lateral movement modules.
                                                                                                        

You’ll notice that there are significantly fewer modules included in this category. This is because, essentially, lateral movement is only accomplished a few different ways. The most common way to move laterally is to use a built-in remote management tool such as WMI or PSExec.

WMI:

Using the Windows Management Instrumentation (WMI), you can run remote commands on a Windows system which you have administrative access to. This makes it trivial to establish agents on systems. Empire has a module for performing WMI lateral movement which will execute a stager for a specified listener to establish an agent on the target host.
                  

Options for the invoke_wmi module.
                                         

PSExec:

PSExec is a part of the SysInternals suite of tools. It also facilitates remote management of Windows systems and requires administrative privileges on the target system. PSExec works by creating and executing a service on the target host. This is can be a very identifiable behavior and is liable to be detected by any defensive tools running on the endpoint.
