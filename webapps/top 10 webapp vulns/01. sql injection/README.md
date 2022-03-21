<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>SQL Injection</title>
</head><body>SQL INJECTION ---- OWASP JUICE SHOP<br/>
<br/>
An attack where malicious SQL statements are injected into a SQL database<br/>
<br/>
Can disclose senstive information from the database. Modify the database.. potentiall get a shell<br/>
<br/>
<br/>
<br/>
Statements<br/>
<br/>
SELECT - get data from table<br/>
INSERT - INsert date into table<br/>
DELETE - remove data from table<br/>
UPDATE - Modiy data in a table<br/>
DROP - Delete a table<br/>
UNION - Combines data from multiple queries<br/>
WHERE - Filter based on proivided info<br/>
AND/OR/NOT - Filter based opn multiple conditons<br/>
ORDER BY - Sort resultes<br/>
* - wild care<br/>
' and &quot; - string delimiters<br/>
--, /* and # comments<br/>
* and % wild cards<br/>
; - End statement<br/>
<br/>
SELECT * FROM Users;<br/>
<br/>
Note - when not getting an error responce, you could be facing a case of blind SQL injection. <br/>
inject sleep commands and see if the site processes it.<br/>
input: test' (sleep 10)<br/>
<br/>
ATTACK<br/>
<br/>
Navigate to the login portal<br/>
<img height="400" src="image.png" width="386"/><br/>
<br/>
<br/>
Run burp suite and direct traffic through the proxy<br/>
<br/>
plug in some test data and intercept the request<br/>
<br/>
<img height="250" src="image 2.png" width="583"/><br/>
<br/>
<br/>
Send it to repeater and submit data again to capture responce for analysis<br/>
<br/>
<br/>
Responce !<br/>
Invalid email or password.<br/>
<br/>
add a ' to test email and check for responce. Trying to identify is field is vulnerable to sql injection<br/>
<br/>
This returned an error which provides additional details that can be used to craft further attacks.<br/>
<br/>
<img height="350" src="image 3.png" width="428"/><br/>
<br/>
<br/>
<br/>
SQLITE_ERROR - SQLite <br/>
<br/>
&quot;SELECT * FROM Users WHERE email = 'test'' AND password = '098f6bcd4621d373cade4e832627b4f6' AND deletedAt IS NULL&quot;<br/>
<br/>
Can be user to craft injections<br/>
<br/>
Login in as ADMIN.... admin account is usuall the first account.. account 0 or 1<br/>
<br/>
using the added ' we can break the first pat of the syntax then include an alway true statement<br/>
<br/>
&quot;SELECT * FROM Users WHERE email = 'test'<b>' OR 1=1; --</b><i>AND password = '098f6bcd4621d373cade4e832627b4f6' AND deletedAt IS NULL&quot; (All of this gets ignored)</i><br/>
<br/>
<br/>
this grants Admin and completes thee challange<br/>
<br/>
<img height="400" src="image 4.png" width="465"/><br/>
<br/>
<br/>
DEFENCES<br/>
<br/>
Parameterised Statements<br/>
ensures that inputs are passed through safely. Only accepts what is expected<br/>
<br/>
Sanitising Input<br/>
dont allow unneccesarry characters IE ' and OR and 1=1<br/>
<br/>
<br/>
<br/>
</body></html>