**Pivoting**

<br/>
PIVOTING LAB<br/>
<br/>
<br/>
Access to a machine on 1 subnet... that machine has access to atoher subnet with 1 or more machines. <br/>
<br/>
We need to use acces to machine A to &quot;pivot&quot; to machine B.<br/>
<br/>
METASPLOIT<br/>
<br/>
once you have a shell on machine A... use psexec in metasploit<br/>
<br/>
run ipconfig or route print<br/>
<br/>
this will show there are 2 NICs and indicate other machines.<br/>
<br/>
use AUTOROUTE<br/>
<br/>
syntax &gt;&gt; run autoroute -s &lt;ip&gt; (ie 10.10.10.0/24)<br/>
<br/>
We are building a dedicated route through machine A to the network of Machine B<br/>
<br/>
syntax &gt;&gt; run autoroute -p<br/>
<br/>
<br/>
Now we can enumerate the new network... <br/>
<br/>
Backgroud the autoroute<br/>
<br/>
syntax &gt;&gt; background<br/>
<br/>
<br/>
metasplooit hjas an inbuilt port scanner<br/>
<br/>
find using search<br/>
<br/>
syntax &gt;&gt; search portscan<br/>
<br/>
use a tcp scanner<br/>
<br/>
set all options<br/>
<br/>
testing access to internal machine... now we can attack!<br/>
<br/>
