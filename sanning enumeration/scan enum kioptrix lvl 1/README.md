# Scan and Enum (kioptrix lvl1)

- Obtain VM from [www.vulnhub.com](https://www.vulnhub.com)
- A great resource for vulnerable VMs

Identify attacker IP:
- `ifconfig` or `ip -a`
- Attacker IP: 192.168.247.128

Conduct an ARP scan to scan network for potential victim IPs:
- `arp-scan -l`
- Note: may have to use `sudo`
- Exclude .1, .2, .254, and attacker IP
- Potential victim: 192.168.247.129
<img height="177" src="image 2.png" width="650"/><br/>

OR

Use netdiscover:
- `netdiscover -r <ip>` (192.168.247.0/24)
- Requires root. Use `sudo`
- 192.168.247.129

<img height="550" src="image.png" width="573"/><br/>
NMAP SCAN (network mapper):
- Scans for open ports and services
- `nmap -T4 -p- -A 192.168.247.129`
- `-sS` for stealth scan (not used in this case)
- `-T4` for speed (1-5)
- `-p-` for scanning all ports (exclude for top 1000)
- `-A` for all information
<img height="650" src="image 3.png" width="586"/><br/>
Enumerating Ports:
- Focus on HTTP and SMB (historically bad)
- Ports 80 and 443

Start by checking the IP in a browser (both HTTPS and HTTP):
- Default web page, no identifiable purpose
- Provides info: running Apache, powered by RedHat Linux
- Clicking links gives 404 page with further info disclosures (Apache version)
<img height="400" src="image 4.png" width="494"/><br/>
Default web page. no idetifiable purpose. Posssible poor hygine.<br/>
provides info - running apache. Powerd by redhat linux. <br/>
clicking links givves 404 page with further info discloures. Apache version<br/>

<img height="100" src="image 5.png" width="283"/><br/>
<br/>
NIKTO WEB VULNERABILITY SCANNER<br/>
NIKTO WEB VULNERABILITY SCANNER:
- Syntax: `nikto -h (host) http(s)://<ip>`
- If HTTPS doesn't work, try HTTP
- Outdated services are a finding to be noted in the report
- Results could indicate potential vulnerabilities that can be exploited
- Also provides basic directory busting and potential RCE
<img height="650" src="image 6.png" width="502"/><br/>

DIRECTORY ENUMERATION tools:
- dirb
- dirbuster (preferred)
- gobuster

DIRBUSTER syntax:
- `dirbuster &`
- Opens a GUI
- Enter target URL: `http(s)://<ip>:<port>/`
- Select "Go Faster" to use more threads
- Choose a word list from `/usr/share/dirbuster` folder
- In the file extension, list all extensions to look for
- Once scan finished, enumerate all the pages looking for useful inf
<img height="300" src="image 7.png" width="418"/><br/>
in file extension. lists all the extension to look for. NOTE will increase time to scan as each extension is scanned for ever word in the list.<br/>
<img height="350" src="image 8.png" width="511"/><br/>
ENUMERATING SMB PORT 139:
- From nmap: 139/tcp open netbios-ssn Samba smbd (workgroup: MYGROUP)
METASPLOIT:
- Syntax: `msfconsole`
- Use `search` to find exploits and modules
- We have SMB, so find a module to identify SMB version
- Use `search smb` or `search smb version`
- Auxiliary module: `auxiliary/scanner/smb/smb_version`
- Use the module: `use auxiliary/scanner/smb/smb_version`
- Set options using `set <field>`
- Syntax: `set RHOST <ip>`
- Run the module: `run`
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
SMBCLIENT:
- Syntax: `smbclient -L <ip>` (list out files) `\\<ip>\` (additional slashes for character escaping in Linux)
- If prompted for password, just hit enter
- Provides information on file shares

<img height="250" src="image 11.png" width="570"/><br/>
if prompted for password. Just hit enter<br/>
still provided information on fileshares... 2 of them<br/>
IPC$<br/>
ADMIN$
ENUMERATE
retry command... remove -L (list) and append the fileshares<br/>
<img height="100" src="image 12.png" width="586"/><br/>
denied.. but tried
SSH ENUMERATION:
- From nmap: 22/tcp open ssh OpenSSH 2.9p2 (protocol 1.99)
- Enumerating is difficult as it's close to exploitation
- Try connecting up to the password request without entering a password
- Look for a banner and information disclosure
RESEARCHING THE VULNERABILITIES:
- Use Google
- Port 80/443:
  - Apache httpd 1.3.20 ((Unix) (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
  - Mod_ssl/2.8.4 is vulnerable to a remote buffer overflow (CVE-2002-0082, OSVDB-756)
- Port 139 (SMB):
  - Samba 2.2.1a is vulnerable
- Port 22 (SSH):
  - OpenSSH 2.9p2
ALTERNATE RESEARCH TOOL: SEARCHSPLOIT
- Syntax: `searchsploit <info>`
- Can use for validation or if Google is not available

NESSUS:
- Web app vulnerability scanner
- Download, create an account, set up, and run
- Follow online guides as required
- Ungroup the results and start with critical findings
- Look for exploitable items and common themes (insufficient patching)
- Export the Nessus file and use other tools to convert to Excel for clients
- Always verify, do not take the scan as gospel
