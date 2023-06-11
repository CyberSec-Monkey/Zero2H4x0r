<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Stored Passwords</title>
</head><body>Escalation via Stored Passwords<br/>
<br/>
Run history and search through. Passwords may be saved.<br/>
ls -la can lead to the location of bash history. read by cat .bash_history<br/>
<br/>
You are looking for sensitive items and leads.. maybe its a sensitive location.<br/>
<br/>
Automated tools like linpeas will also do this.<br/>
<br/>
the colour hunting trick will also do this search..<br/>
<br/>
Payload all the things under methodolgy under lunx priv esc &gt; looking for passwords provides the manual searchs.<br/>
<br/>
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md#looting-for-passwords<br/>
<br/>
<b>grep --color=auto -rnw '/' -ie &quot;PASSWORD&quot; --color=always 2&gt; /dev/null<br/>
</b><b>find . -type f -exec grep -i -I &quot;PASSWORD&quot; {} /dev/null \; </b><br/>
<br/>
The find tool might find hidden files.<br/>
<br/>
Be sure to also search through files and folders manually as sensitive info may be stored in files.<br/>
<br/>
ie config files might provide credentails or credentail locations. (open vpn)<br/>
<br/>
<br/>
<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /home/user/myvpn.ovpn<br/>
2. From the output, make note of the value of the “auth-user-pass” directive.<br/>
3. In command prompt type: cat /etc/openvpn/auth.txt<br/>
4. From the output, make note of the clear-text credentials.<br/>
5. In command prompt type: cat /home/user/.irssi/config | grep -i passw<br/>
6. From the output, make note of the clear-text credentials.<br/>
<br/>
<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
1. In command prompt type: cat ~/.bash_history | grep -i passw<br/>
2. From the output, make note of the clear-text credentials.<br/>
<br/>
<br/>
<br/>
</body></html>