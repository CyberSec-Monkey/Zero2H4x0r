**Passive recon (no active scanning)**<br/>
<br/>
(not covered in course) physical/social - go onsite, social engineering. Photos, drone footage.<br/>
- location, images<br/>
- job information, employee names numbers, managers, badges<br/>
<br/>
<br/>
<br/>
Identifying the target<br/>
- public bug bounty programs (bug crowd)<br/>
ROE - always check inscope! ALWAYS check out of scope!<br/>
<br/>
HUNTER.IO<br/>
gather email addresses<br/>
www.hunter.io<br/>
<br/>
Free plan = about 20 searches per month<br/>
putting in domain IE: tesla.com will produce names and emails @tesla.<br/>
Will also provide the source of the email address.<br/>
Sometimes names will be associated with job role or department.<br/>
can give clues as to email formats... and potentially valid user names<br/>
combine with a linkedIn search<br/>
<br/>
knowing email format can enable password spraying<br/>
<br/>
BREECHED CREDENTIALS<br/>
github.com/hmaverickadams<br/>
<br/>
Breech parse tool<br/>
bash script<br/>
provides a 40+gb file<br/>
data files containing emails and passwords collated from crednetial dumps<br/>
Heath provides a tool to search through give an @ (ie @tesla.com) and place intol a file tesla.txt<br/>
<br/>
Credential stuffing is when you know the password for a cred... try different formats<br/>
<br/>
Password spraying - take known creds and spray common passwords at them to get a hit<br/>
<br/>
WEB INFO GATHERING<br/>
HUNTING SUBDOMAINS<br/>
Tool - Sublister<br/>
install with apt insall sublist3r<br/>
Run with sublist3r<br/>
give domain<br/>
cmd - sublist3r -d tesla.com<br/>
use -t for thread.... speed it up<br/>
<br/>
ALT certificate fingerprinting<br/>
open browser go to crt.sh **** this will find sub sub domains<br/>
enter domain and it will return listed certificates<br/>
<br/>
<br/>
Better tool - OWASP AMASS<br/>
use github to install and use.<br/>
slow, long to run<br/>
<br/>
<br/>
Subdomains - important to ensure we check ALL possible domains... without it limited to a single domain<br/>
<br/>
<br/>
IDENTIFY WEB TECHNOLOGIES<br/>
www.builtwith.com<br/>
enter domain and get back list of trechs and features<br/>
check frameworks<br/>
<br/>
Better to use WAPPALYZER<br/>
an addon for firefox<br/>
is built into the browser. Requires navigation to the site and click wappalyzer<br/>
Knowing Technology can give indication to possible vulnerabilites.<br/>
You can enumerate version numbers on Tech looking for active vulnerabilites.<br/>
<br/>
Built into Kali - WHJATWEB<br/>
whatweb &lt;url&gt;<br/>
harder to read but can give additional info and versions.<br/>
<br/>
GATHERING INFO WITH BURPSUITE<br/>
Built into kali. Free version is fine<br/>
Burp is a web proxy... will intercept traffic<br/>
Steps<br/>
temp project &gt; next&gt; start burp<br/>
go to firefox &gt; preferences<br/>
settings<br/>
manual proxy config<br/>
127.0.0.1 port 8080 use for all protocols<br/>
new tab<br/>
https://burp &gt; accept if prompted<br/>
click CA certificate.. save file<br/>
gp back to prefernces<br/>
privacy and security<br/>
new certificate<br/>
select that cert<br/>
select both check boxes then import<br/>
<br/>
go to a website... it wont load as burp is intercepting packets.. either turn off or forward<br/>
Look at responces to reqests for info<br/>
<br/>
Note - server names is information disclosure low but still<br/>
<br/>
GOOGLE FU<br/>
know how to google things<br/>
use google search syntax &gt;&gt;&gt; google it<br/>
to narrow down to just the site use 'site:'<br/>
site:tesla.com<br/>
remove www to get subdomains '-www'<br/>
<br/>
looking for files<br/>
'filetype:'<br/>
site:tesla.com filetype:pdf<br/>
<br/>
SOCIAL MEDIA<br/>
is OSINT &gt; use linkedIn and twitter<br/>
go to company page.... images.. prob badge photos<br/>
people and positions<br/>
can use scrapers to get names<br/>
enter names into email format<br/>
get all the info on the ppl<br/>
<br/>
<br/>
