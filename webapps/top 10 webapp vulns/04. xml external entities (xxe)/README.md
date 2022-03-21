<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>XML External Entities (XXE)</title>
</head><body>XXE ---- OWASP JUICE SHOP<br/>
<br/>
<br/>
Can be used for things liike DOS, RCE, info disclosre etc<br/>
<br/>
google XXE payloads... thats fine<br/>
https://github.com/payloadbox/xxe-injection-payload-list<br/>
<br/>
<b>https://github.com/swisskyrepo/PayloadsAllTheThings<br/>
</b><br/>
<br/>
XXE attacks systems that parse XML input<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
XXE wont run in docker... RIP<br/>
<br/>
Methodology<br/>
<br/>
Create a malicious file<br/>
<br/>
<br/>
&lt;?xml version=&quot;1.0&quot; encoding=&quot;ISO-8859-1&quot;?&gt; <br/>
	&lt;!DOCTYPE foo [ <ul><li style="list-style-type: none">&lt;!ELEMENT foo ANY &gt; </li>
</ul>
	&lt;!ENTITY xxe SYSTEM &quot;file:///etc/passwd&quot; &gt;]&gt;&lt;foo&gt;&amp;xxe;&lt;/foo&gt;<br/>
<br/>
call it something.xml &gt; save it somehjwere accesible<br/>
<br/>
<br/>
navigate to login page &gt; login as user (creaate account if required)<br/>
<br/>
NOTE - this is called authenticatred testing &gt;&gt;&gt; IE we are currently an authenticated user or middle level user<br/>
Normally you would now click around and see what you ahve access to and can do.<br/>
Burp suite pro can crawl through a website for you.,.<br/>
<br/>
User can upload files<br/>
<br/>
<img height="300" src="image.png" width="377"/><br/>
<br/>
an upload feature should restrict file types and enforce it... First test that it works... then we test bypass the restriction<br/>
<br/>
<br/>
BUrp should be running but we are going to try upload the malicious file and intercept the submission to check the responce.<br/>
Note when trying to upload the file may not be vissible... this is a feature of &quot;all supported types&quot; being selected. This also indicated what the system is expecting to receive.<br/>
Just change it to &quot;all files&quot;<br/>
<br/>
<img src="image 2.png"/><br/>
<br/>
<br/>
<img height="300" src="image 3.png" width="382"/><br/>
<br/>
<br/>
Capture submission with BURP and send to repeater for replayability<br/>
<br/>
<img height="550" src="image 4.png" width="847"/><br/>
<br/>
No restriction so we are able to upload and run the malicious XML file... IF &gt;&gt;&gt; IF it worked in docer it would output the etc/passwd file contents to the responce...<br/>
<br/>
Any partially successfull attack can be submitted as a finding as it is still evidence of vulnerability! you dont need to fully exploit it.<br/>
The ability to bypass the file type &quot;white listing&quot; is also a finding to be submitted<br/>
<br/>
WHY <br/>
External entities are being parsed<br/>
<br/>
DEFENSE<br/>
<br/>
Disable DTTDs Disable external entities.<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
</body></html>