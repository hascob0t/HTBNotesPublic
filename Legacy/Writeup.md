# Legacy - Writeup

### Ports found 135 (netbios-ssn), 445 (microsoft ds/smb), 3389 (ms-wbt-server)

When you find a port one thing that you can do is to locate if there are nse scripts that you can run against a specific port. 
This command can be used to find nse scripts that can be ran against smb: **locate \*.nse | grep smb-vuln**
You can then use the following command to use a vuln against the port using nmap: **nmap --script vuln -p445 10.10.10.4**
