# Legacy - Writeup

### Ports found 135 (netbios-ssn), 445 (microsoft ds/smb), 3389 (ms-wbt-server)

When you find a port one thing that you can do is to locate if there are nse scripts that you can run against a specific port. 
This command can be used to find nse scripts that can be ran against smb: **locate \*.nse | grep smb-vuln**
You can then use the following command to use a vuln against the port using nmap: **nmap --script vuln -p445 10.10.10.4**.

The vulnerability that will be found is called eternalblue or MS17-010. There is diffrent ways to exploit this vulnerability. In this case I use the easiest way possible which was using a script I found in the following page: **https://github.com/helviojunior/MS17-010**. The script used was called send_and_execute.py.
If you run this against a vulnerable machine you instantly get RCE on that machine. In this machine that was enough to become root. 

### Notable Commands
- locate \*.nse | grep smb-vuln
- nmap --script vuln -p445 10.10.10.4

### Lessons Learned
- There is an vulnerability scanner inside namp USE IT!
- If there is a MS*** exploit theres probably a script that can exploit it. 
