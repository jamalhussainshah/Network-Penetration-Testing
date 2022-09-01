
![R](https://user-images.githubusercontent.com/95676591/187852721-9ea3a692-af6b-44a2-8314-67aec52fad5b.jpg)

![Screenshot_2022-08-31_23_04_29](https://user-images.githubusercontent.com/95676591/187853522-43da1e40-9197-438b-8d1b-a179377faff3.png)



## All procedure of installation of flanscan is shown in snapshot during installation and also given one case study in order find vulnerability.

Flan Scan is a lightweight network vulnerability scanner. With Flan Scan you can easily find open ports on your network, identify services and their version, and get a list of relevant CVEs affecting your network.

Flan Scan is a wrapper over Nmap and the vulners script which turns Nmap into a full-fledged network vulnerability scanner. Flan Scan makes it easy to deploy Nmap locally within a container, push results to the cloud, and deploy the scanner on Kubernetes.


### Getting Started


Clone this repository

Make sure you have docker setup:

        $ docker --version
        
Add the list of IP addresses or CIDRS you wish to scan to shared/ips.txt.

Build the container:

        $ make build
        
Start scanning!
      
        $ make start
        
By default flan creates Latex reports, to get other formats run:

        $ make html
        
        
Additional supported formats are md (markdown), html and json.

When the scan finishes you will find the reports summarizing the scan in shared/reports. You can also see the raw XML output from Nmap in shared/xml_files.



### Custom Nmap Configuration

By default Flan Scan runs the following Nmap command:

            $ nmap -sV -oX /shared/xml_files -oN - -v1 $@ --script=vulners/vulners.nse <ip-address>
            
The -oX flag adds an XML version of the scan results to the /shared/xml_files directory and the -oN - flag outputs "normal" Nmap results to the console. The -v1 flag increases the verbosity to 1 and the -sV flag runs a service detection scan (aside from Nmap's default port and SYN scans). The --script=vulners/vulners.nse is the script that matches the services detected with relevant CVEs.

Nmap also allows you to run UDP scans and to scan IPv6 addresses. To add these and other flags to Flan Scan's Nmap command after running make build run the container and pass in your Nmap flags like so:

          $ docker run -v $(CURDIR)/shared:/shared flan_scan <Nmap-flags>
