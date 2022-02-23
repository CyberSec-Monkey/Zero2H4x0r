# Scan and Enum (kioptrix lvl1)

Obtain VM from www.vulnhub.com<br/>
<br/>
a great resourecs for vuln VMs<br/>
<br/>
identify attacker IP <br/>
ifconfig or ip -a<br/>
192.168.247.128<br/>
<br/>
conduct an arp scan to scan network for potential victim IPs<br/>
arp-scan -l<br/>
Note: may have to use sudo<br/>
<br/>
will return all systems on network. Exclude .1,.2,.254 and attacker IP.<br/>
potenital victim - 192.168.247.129<br/>
<br/>
<img height="177" src="image 2.png" width="650"/><br/>
<br/>
OR<br/>
<br/>
use netdiscover<br/>
netdiscover -r &lt;ip&gt; (192.168.247.0/24) <br/>
again requires root. use Sudo<br/>
<br/>
-192.168.247.129<br/>
<br/>
<img height="550" src="image.png" width="573"/><br/>
<br/>
<br/>
NMAP SCAN (network mapper)<br/>
scans for open ports and services<br/>
<br/>
nmap -T4 -p- -A 192.168.247.129<br/>
<br/>
-sS stealth scan &gt; it is not<br/>
<br/>
-T4 = speed 1-5<br/>
-p- = ports -p- all ports. exclude for top 1000<br/>
good idea to scan all ports to ensure services not missed<br/>
can also list specific ports<br/>
-A give me all the info.. eveything<br/>
<br/>
<img height="650" src="image 3.png" width="586"/><br/>
<br/>
outputs open ports, serivces being run and version numbers if possible. Gives system info include OS with a certainty percentage<br/>
<br/>
ENUMERATING PORTS<br/>
<br/>
HTTP and SMB! historically bad<br/>
<br/>
PORTs 80 and 443<br/>
<br/>
start by checking the IP in a browser both https and http<br/>
<img height="400" src="image 4.png" width="494"/><br/>
<br/>
Default web page. no idetifiable purpose. Posssible poor hygine.<br/>
provides info - running apache. Powerd by redhat linux. <br/>
clicking links givves 404 page with further info discloures. Apache version<br/>
<br/>
<img height="100" src="image 5.png" width="283"/><br/>
<br/>
NIKTO WEB VULNERABILITY SCANNER<br/>
<br/>
is loud &gt; good security will block it.<br/>
<br/>
syntax &gt; nickto -h (host) http(s):// &lt;ip&gt;<br/>
<br/>
if https doesnt work try http<br/>
<img height="650" src="image 6.png" width="502"/><br/>
<br/>
outdated services are a finding to be notated on report. More outdated, more severe.<br/>
results could indicate potential vulnerabilities that can be exploited.<br/>
<br/>
ALSO porivdes basic dir busting. provides some basic directories that may be vulnetrable.<br/>
biggest find is the potential RCE.<br/>
<b>mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-0082, OSVDB-756.</b><br/>
<br/>
<br/>
DIRECTORY ENUMERATION<br/>
tool options<br/>
dirb<br/>
dirbuster &gt; Heath prefered<br/>
gobuster<br/>
<br/>
DIRBUSTER<br/>
syntax &gt; dirbuster&amp;<br/>
opens a GUI.<br/>
enter target URL &gt; http(s)://&lt;ip&gt;:&lt;port&gt;/<br/>
<br/>
select go faster to use more threads<br/>
<br/>
choose a word list from usr &gt; share &gt; dirbuster folder<br/>
<img height="300" src="image 7.png" width="418"/><br/>
<br/>
in file extension. lists all the extension to look for. NOTE will increase time to scan as each extension is scanned for ever word in the list.<br/>
admin.php<br/>
admin.txt<br/>
admin.zip<br/>
admin.rar etc<br/>
<br/>
<img height="350" src="image 8.png" width="511"/><br/>
<br/>
once scan finished... enumerate ALL the pages looking for useful info.<br/>
<br/>
ENUMERATING SMB PORT 139<br/>
<br/>
from nmap &gt; 139/tcp  open netbios-ssn Samba smbd (workgroup: MYGROUP)<br/>
<br/>
METASPLOIT<br/>
<br/>
syntax &gt; msfconsole<br/>
is a framework<br/>
<br/>
can use 'search' to find exploits and modules<br/>
we ahve SMB so find a module to ID SMB version<br/>
<br/>
seach smb = 125 results<br/>
<br/>
search smb version = 14 results<br/>
<br/>
auxiliary/scanner/smb/smb_version<br/>
<br/>
to use the module <br/>
syntax &gt; use &lt;module&gt;<br/>
use auxiliary/scanner/smb/smb_versio<b>n<br/>
</b><b><br/>
</b><img height="450" src="image 9.png" width="434"/><br/>
entering options will show required and option details<br/>
<br/>
use set &lt;field&gt; to set options<br/>
syntax set RHOST &lt;ip&gt;<br/>
<br/>
<img height="150" src="image 10.png" width="483"/><br/>
<br/>
msf6 auxiliary(scanner/smb/smb_version) &gt; options<br/>
<br/>
Module options (auxiliary/scanner/smb/smb_version):<br/>
<br/>
 Name   Current Setting Required Description<br/>
 ----   --------------- -------- -----------<br/>
 RHOSTS          yes    The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasplo<br/>
                   it<br/>
 THREADS 1        yes    The number of concurrent threads (max one per host)<br/>
<br/>
msf6 auxiliary(scanner/smb/smb_version) &gt; set RHOSTS 192.168.247.129<br/>
RHOSTS =&gt; 192.168.247.129<br/>
msf6 auxiliary(scanner/smb/smb_version) &gt; run<br/>
<br/>
[*] 192.168.247.129:139  - SMB Detected (versions:) (preferred dialect:) (signatures:optional)<br/>
[*] 192.168.247.129:139  -  Host could not be identified: Unix (Samba 2.2.1a)<br/>
[*] 192.168.247.129:   - Scanned 1 of 1 hosts (100% complete)<br/>
[*] Auxiliary module execution completed<br/>
<br/>
returned a version number for SMB &gt; 2.2.1a<br/>
<br/>
SMBCLIENT &gt; will atempt to connect to file share. this will test the ability to connect anomoys access. if can connect. we can look through files for infomation.<br/>
<br/>
syntax &gt; smbclient -L (list out files) \\\\&lt;ip&gt;\\ (additional slashes are for character escaping in linux.<br/>
<br/>
<img height="250" src="image 11.png" width="570"/><br/>
if prompted for password. Just hit enter<br/>
still provided information on fileshares... 2 of them<br/>
IPC$<br/>
ADMIN$<br/>
<br/>
ENUMERATE IT<br/>
retry command... remove -L (list) and append the fileshares<br/>
<img height="100" src="image 12.png" width="586"/><br/>
denied.. but tried<br/>
<br/>
SSH ENUMERATION<br/>
<br/>
from nmap &gt; 22/tcp  open ssh     OpenSSH 2.9p2 (protocol 1.99)<br/>
<br/>
enumerating is difficult because its close to exploitaiton... a single password guess is no longer enumeration.<br/>
<br/>
attempt to connect all the way up to password request (if exists) do not enter a password... we a re looking for a banner and thus information disclosure.<br/>
<br/>
RESEARCHING THE VULNERABILITES<br/>
Google!!! start googleing!!!<br/>
<br/>
<br/>
port 80/443<br/>
80/tcp  open http    Apache httpd 1.3.20 ((Unix) (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)<br/>
<b>mod_ssl/2.8.4 - mod_ssl 2.8.7 and lower are vulnerable to a remote buffer overflow which may allow a remote shell. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-0082, OSVDB-756.</b><br/>
<br/>
Google &gt; <b>mod_ssl/2.8.4</b>exploit<br/>
exploit DB<br/>
https://www.exploit-db.com/exploits/764<br/>
<br/>
Github alternate <br/>
https://github.com/heltonWernik/OpenLuck<br/>
<br/>
Google &gt; Apache httpd 1.3.20 exploit<br/>
exploit DB<br/>
https://www.exploit-db.com/exploits/19975<br/>
<br/>
port 139 (SMB)<br/>
139/tcp  open netbios-ssn Samba smbd (workgroup: MYGROUP)<br/>
Unix (Samba 2.2.1a)<br/>
<br/>
Google &gt; Samba 2.2.1a exploit<br/>
exploit DB<br/>
https://www.exploit-db.com/exploits/10<br/>
https://www.exploit-db.com/exploits/7<br/>
<br/>
rapid 7 (metasploit)<br/>
https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/<br/>
NOTE<br/>
Description<br/>
<br/>
This exploits the buffer overflow found in Samba versions 2.2.0 to 2.2.8. This particular module is capable of exploiting the flaw on x86 Linux systems that do not have the noexec stack option set. NOTE: Some older versions of RedHat do not seem to be vulnerable since they<b>apparently do not allow anonymous access to IPC</b><br/>
WE tested and DID have anon access to IPC. CHECK!<br/>
<br/>
<br/>
Port 22 (SSH)<br/>
22/tcp  open ssh     OpenSSH 2.9p2 (protocol 1.99)<br/>
<br/>
<br/>
ALTERANTE RESEARCH TOOL &gt;&gt;&gt;&gt; SEARCHSPOLIT<br/>
dont be too specific<br/>
syntax &gt; searchsploit &lt;info&gt;<br/>
searchsploit samaba 2.2<br/>
<br/>
Can use for validation or if google not available<br/>
<br/>
<br/>
<br/>
BIG RANDOM NOTE&gt;&gt;&gt;&gt; NESSUS<br/>
web app vulnerability scanner... downlaod create account.. set up and run.. get results...<br/>
follow online guides as required.<br/>
<br/>
Once scanned.. ungroup<br/>
start with critical and move down list<br/>
look for things that are exploitable<br/>
look for common themes IE insufficient patching<br/>
you can export the nessus file and use otehr tools to tunr to pretty excel for client.<br/>
ALWAYS verify, do not take scan as gossple<br/>
<br/>
<br/>
<br/>
