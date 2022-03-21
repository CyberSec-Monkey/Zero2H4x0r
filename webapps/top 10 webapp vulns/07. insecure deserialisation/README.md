<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Insecure Deserialisation</title>
</head><body>INSECURE DESERIALISATION --- Theoretical<br/>
<br/>
Resources<br/>
https://owasp.org/www-project-top-ten/2017/A8_2017-Insecure_Deserialization.html<br/>
<br/>
Does not work in Juice Shop<br/>
<br/>
Note - Difficult to find<br/>
<br/>
Nrmally &gt; data serialised for tranfers &gt; deserialised at other end to be used<br/>
<br/>
As attacker We serialise our attack send it to the webapp which deserialises and and executres it<br/>
<br/>
I need to look more into this... Deep!<br/>
<br/>
<br/>
Defend!! dont accept serialised data from untrusted sources<br/>
<br/>
Read this<br/>
https://github.com/frohoff/ysoserial<br/>
</body></html>