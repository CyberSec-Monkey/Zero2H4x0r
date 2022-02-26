**Group Policy Preferences (GPP)**
GROUP POLICY PREFERNCES (GPP)<br/>
<br/>
OVERVIEW<br/>
<br/>
Allows admins to create policies using embedded credentials<br/>
<br/>
credentials were encrypted and placed in a 'cPassword'<br/>
<br/>
the key was released ionto the wild<br/>
<br/>
was Patched in MS14-025 but doest prevent previous uses. Can still be found in the wild<br/>
<br/>
So if an admin had stored a policy and credentails before the patch it could still be found and decrypted<br/>
<br/>
<br/>
Refernce material<br/>
https://www.rapid7.com/blog/post/2016/07/27/pentesting-in-the-real-world-group-policy-pwnage/<br/>
<br/>
<br/>
This sections requires a VIP account on HTB<br/>
<br/>
I will return!!!<br/>
<br/>
NOTES<br/>
---------------<br/>
<br/>
<br/>
<br/>
NMAP scan<br/>
<br/>
if ports 53, 88, 389 and 636 &gt; prob domain controller... maybe router<br/>
<br/>
445 is open <br/>
<br/>
attack uses SMB<br/>
<br/>
try connect smb see share folders<br/>
<br/>
a share folder has anon access (replicaiton)<br/>
<br/>
turn prompt off &gt;&gt;&gt; prompt off &gt;&gt;&gt; dont prompt me<br/>
<br/>
recurse on &gt;&gt;&gt; download all the files I tell it to<br/>
<br/>
looking for the groups.xml file<br/>
<br/>
can use mget * to download all files...<br/>
<br/>
navigate to the groups.xml<br/>
open it <br/>
copy the hash<br/>
<br/>
run in gpp-decrypt<br/>
<br/>
syntax &gt; gpp-decrypt &lt;hash&gt;<br/>
<br/>
from the file and gpp-decypt you now have a username and a password in plain<br/>
<br/>
<br/>
<br/>
<br/>
With creds.. psexec.. may not work<br/>
<br/>
what about kerborosting<br/>
<br/>
