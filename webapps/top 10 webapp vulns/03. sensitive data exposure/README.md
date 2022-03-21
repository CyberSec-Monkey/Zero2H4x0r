<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Sensitive Data Exposure</title>
</head><body>SENSITIVE DATA EXPOSURE ---- OWASP JUICE SHOP<br/>
<br/>
<br/>
Information on how to test, how to prevent end exmaples here<br/>
https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure.html<br/>
<br/>
<br/>
Essentially digging through all the files regardless of type like a rat looking for the juicy bits of information.<br/>
<br/>
<br/>
ATTACK<br/>
<br/>
Note - useing burp.. crawl all over the site thern enumerate through EVERY THING use the search _ &quot;key/s&quot; &quot;password&quot; etc<br/>
<br/>
Maybe see that headers dont have HSTS enabled... thus can downgrade from HTTPS to HTTP<br/>
<br/>
<b>https://securityheaders.com/<br/>
<br/>
</b>and scan the site.. lots of info<br/>
<br/>
use nmap to test the ssl cyphers<br/>
<br/>
syntax &gt; nmap --script=ssl-enum-ciphers -p 443 &lt;site&gt;.com</body></html>