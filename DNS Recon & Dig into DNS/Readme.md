

### What is DNS Recon?

DNSRecon is a Python script that provides the ability to perform: Check all NS Records for Zone Transfers. Enumerate General DNS Records for a given Domain (MX, SOA, NS, A, AAAA, SPF and TXT). Perform common SRV Record Enumeration.

### What is DNSRecon used for?

DNSRecon can perform a variety of functions ranging from security assessments to basic network troubleshooting by allowing users to: Check DNS server cache records for A, AAAA and CNAME records given a list of host records in a text file.

some important commands for DNS Recon and dig into DNS.

                              host ip

                              nslookup 
                              set type=ns
                              website

                              dig website -t ns +short
                              dig website AAAA
                              dig website CNAME

                              for ip in 'website' ; do nmap -Pn $ip; done

### Dig

To find more information, we can use the dig tool. Dig stands for domain information groper, and it does just that.  A typical dig command will have some of the following:


                              

dig [@server] [-b address] [-c class] [-f filename] [-k filename] [-m] [-p port#] [-q name] [-t type] [-x addr] [-y [hmac:]name:key] [-4] [-6] [name] [type] [class] [queryopt...]

Since that looks a little overwhelming, let's break it down:

@server - The name or IP of the name server to query. Example - 8.8.8.8
-b address - The source IP of the query. This would set the source to the address of one of the host's network interfaces. Example - 0.0.0.0
-c class - This defaults to IN (for Internet) but you can enter any valid class.
-f <filename> - A list of lookup requests, read from the file.
-k <filename> - A file which contains a TSIG key.
-m - Memory usage debugging.
-p <port> - Allows you to specify a non-standard port.
-q <name> - Assigns a name to the query.
-t <type> - Specifies the type of DNS record to obtain.
-x <address> - Tells dig to perform a reverse lookup. You would supply an IP address. You would not need to supply the name, class, or type.
-y - Specification for a TSIG key itself. These can be generated by dnssec-keygen.
-4 or -6 - forces dig to only use IPv4 or IPv6 query transport.
name - Resource to be looked up. Example - bestestredteam.com
type -  Specifies the type of DNS record to obtain.  
class -  This defaults to IN (for Internet) but you can enter any valid class.  
queryopt - Allows options that can change what is looked up and/or what is displayed in the results.

### DNSrecon

Similar to Dig, we can use another enumeration and scanning tool called DNSrecon. A typical command will look something like:

dnsrecon [-h] [-d DOMAIN] [-n NS_SERVER] [-r RANGE] [-D DICTIONARY] [-f] [-t TYPE] [-a] [-s] [-g] [-b] [-k] [-w] [-z] [--threads THREADS] [--lifetime LIFETIME] [--tcp] [--db DB] [-x XML] [-c CSV] [-j JSON] [--iw] [-v]

Let's once again look at what these command flags mean. I'll skip over the ones that are similar to Dig and focus on the ones that are unique.

-r <range> - Allows reverse lookup brute force.
-D <dictionary> - A file with sub-domains and hostnames to use for brute force.
-f - Filters out brute force results that resolve to the wildcard defined IP address.
-a - Attempts a zone transfer with standard enumeration
-g - Google enumeration.
-b - Bing enumeration.
-k - crt.sh enumeration
-w - Deep whois record analysis
-z - DNSSEC Zone Walk
--db <file>, -x <file>, -c <file>, -j <file>  - Allows you to save found records in SQLite 3, XML, CSV, or JSON respectively.
--iw - Continue to brute force even if a wildcard record is discovered.
-v - Show attempts during brute force.

### Zone Transfers

A zone transfer is a DNS transaction typically used for easily replicating DNS databases across DNS servers. However, if a sever is vulnerable, it can also be used as part of your information gathering phase. With a successful zone transfer, you obtain whatever records are stored in that zone.  There are multiple tools we can use for to perform a zone transfer. We've already talked about Dig and DNSrecon, both of which can attempt a zone transfer by setting the type to AXFR. So the commands would be:

          dig axfr @nsztm1.digi.ninja zonetransfer.me

          dnsrecon -d zonetransfer.me -a
                       
          
          
Another tool, and a quick way to test for zone transfers is DNSenum. The command would be dnsenum zonetransfer.me. DNSenum also enumerates records making it a good "one stop shop" tool for DNS investigations.


The above commands utilize zonetransfer.me, a "domain which is easy to remember and which will always have zone transfer enabled." This site can be a great way to demonstrate the risk associated with the information gained from a zone transfer.

### DNS Cache Poisoning

Also known as DNS spoofing, this attack is used to direct users to a different server than the expected host. This means a penetration tester (or attacker) could redirect legitimate traffic to their own controlled server. From here, they could harvest credentials or deploy a payload.
