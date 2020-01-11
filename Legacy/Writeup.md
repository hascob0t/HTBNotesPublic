# Legacy - Writeup


Start enumerating this machine by using this command:
**nmap -sC -sV -oA nmap 10.10.10.4**
-sC is safe scripts, -sV is safe versioning and -oA is output all.

Then you will see that 139, and 445 are open which are smb ports. 
Versioning will show that this is an old windows xp machine. You can then search for the exploit.
An alternative way to find the exploit is to use a nmap command that probes for vulnerabilities. 
Here is that command: **nmap --script vuln -p445 10.10.10.4**.
Then you will see the exact vulnerability and you can now use that information to hack this machine.


Alternative way of solving this machine is finding the ms17… enternal blue vulnerbility and exploiting it without metasploit. 
You do this by generating a msfvenom reversheshell .exe payload. 
Then sending it using a python eternalblue exploit that is called send_and_execute.py. 
You will then have a reverse shell back to you.
