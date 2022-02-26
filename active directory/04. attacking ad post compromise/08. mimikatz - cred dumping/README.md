**MIMIKATZ**

MIMIKATZ<br/>
<br/>
<br/>
Tool used to view and steal creds form memory, generate kerberos tickets, and leverage attacks.<br/>
<br/>
Dumps creds stored in memory<br/>
<br/>
SOME ATTACKS<br/>
Cred dumping<br/>
pass-the-hash<br/>
over-pass-the-hash<br/>
pass-the-ticket<br/>
golden-ticket<br/>
silver-ticket<br/>
<br/>
<br/>
<br/>
Reference<br/>
<br/>
https://github.com/gentilkiwi/mimikatz<br/>
<br/>
<br/>
NOTE &gt;&gt; back and forth battle between mimikatz deve and windows...<br/>
sometimes it wont work until its patched<br/>
<br/>
This refernce is for the version that does not need to be compiled<br/>
https://github.com/gentilkiwi/mimikatz/releases<br/>
<br/>
This will be downloaded to the domain controller VM., its assumed we have compromiseed the machine and have the ability to upload/download files to the DC<br/>
<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
<br/>
extrack mimikatz<br/>
<br/>
in terminal navigate to mimkatz folders and execture<br/>
<br/>
mimikatz.exe<br/>
<br/>
<img src="image.png"/><br/>
<br/>
First command to run<br/>
<br/>
privilege::debug<br/>
<br/>
this should return privilige '20' OK <br/>
<br/>
this indactes it works good to proceed. this tests that we have access to something we shouldnt under normal conditions<br/>
<br/>
first part of command is the module<br/>
<br/>
next attack<br/>
<br/>
sekurlsa::logonpasswords<br/>
<br/>
<br/>
<br/>
This will return the computers ... computer names.. NTLM hases for computers.. and logons of anyone who has logged on since last reboot.<br/>
<br/>
Provides NTLM hashes.. these can be passed around<br/>
<br/>
Admin has logged in.. we have the NTLM<br/>
<br/>
wdigest is worht checking<br/>
we can turn it on... necxt time the user logs in it will record the password in plain.<br/>
<br/>
<br/>
Next command<br/>
<br/>
lsadump::sam failed<br/>
<br/>
Next comand<br/>
<br/>
lsadump::lsa /patch<br/>
<br/>
dumps user names and ntlm hashes from the local security authority<br/>
<br/>
LSA - protected subsystem in window authenticatios.. it authenticates and createsds logon connectsion to the local computer<br/>
<br/>
<br/>
we have user names and ntlms<br/>
<br/>
we can try crack the passwords<br/>
<br/>
what % can we crack.. pass this onto the client give metrics<br/>
<br/>
Also can lead to golden ticket attack<br/>
<br/>
<br/>
