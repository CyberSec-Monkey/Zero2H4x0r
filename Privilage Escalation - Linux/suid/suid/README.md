<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>SUID</title>
</head><body><b>Escalation via SUID<br/>
</b><br/>
means Set user id<br/>
<br/>
is poermissions settings<br/>
<br/>
<br/>
the permission bits for folders files _r w x _ _ _ _ _ _<br/>
SUID the S bit set looks like _ r w s _ _ _ _ _ _<br/>
<br/>
Allows users to execute a file with permission of a specified user... this is usually one with higher permissions<br/>
<br/>
<br/>
Not all files with S biut set are vulnerable. It will depend on tis usage. Investigation is requirred...<br/>
<br/>
how to find S bit set..... you can try <b>ls -l</b>or <br/>
<br/>
<b>find / -perm -u=s -type f 2&gt;/dev/null</b><br/>
<br/>
<br/>
Will out put a list of files with with S biut set. <br/>
<br/>
compare list against <b>GTFObins</b>for <b>SUID</b><br/>
<br/>
Tools such ans linpeas can also find SUID.<br/>
<br/>
<br/>
</body></html>