**PowerView**
POWERVIEW &gt; Enumerate the network after compromise with initial vectors<br/>
<br/>
Once a machine has been compromised, you would install powerview to run it from the compromised machine<br/>
With access you could possible transfer the file to or download it.<br/>
<br/>
<br/>
CHEAT SHEET<br/>
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993<br/>
<br/>
<br/>
<br/>
<br/>
DOMAIN ENUMERATION<br/>
<br/>
open cmd prompt then from file location of powerview open powershell with exectuion bypass. (EP is desgined to prevent accidently running scripts you may not intend to)<br/>
<br/>
syntax &gt; powershell -ep bypass<br/>
<br/>
<img src="image.png"/><br/>
<br/>
NOTE &gt; Windows Defenders will detect it being run in PS...<br/>
<br/>
Bypass trhough obsfucation or tunr of AV<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
<br/>
<img src="image 3.png"/><br/>
<br/>
We now hoave the IP of the Domain Controller<br/>
192.168.247.133<br/>
<br/>
LETS LEARN SOME THINGS<br/>
<br/>
<img src="image 4.png"/><br/>
<br/>
<br/>
To get further details &gt;&gt;&gt;<br/>
<br/>
<img src="image 5.png"/><br/>
<br/>
<br/>
Net user can dump alot of information. The bigger teh corporation the more data. Try grepping<br/>
<br/>
Get-NetUser | select cn<br/>
Get-NetUser | select samaccountname<br/>
etc<br/>
<br/>
Get-UserProperty - Properties pwdlastset<ul><li style="list-style-type: none">gets a date for the last time a suser dset their password... arte their old passowrds/accounts arround</li>
<li style="list-style-type: none"/>
</ul>
<br/>
Get-UserProperty - Properties logoncount<br/>
<ul><li style="list-style-type: none">if a user has never logged in it may be a honey pot account... dont touch</li>
</ul>
<br/>
<img src="image 6.png"/><br/>
<br/>
<br/>
<img src="image 7.png"/><br/>
<br/>
This tool is HUGE!!!! play with all the features.... Looks like some commands have changed since courcese amterail was made<br/>
<br/>
As above... in course.. it was XYZ -GroupName XYZ<br/>
now XYZ -Name XYZ<br/>
<br/>
<br/>
<br/>
