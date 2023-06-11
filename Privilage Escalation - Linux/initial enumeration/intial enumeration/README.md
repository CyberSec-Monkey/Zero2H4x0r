<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Intial Enumeration</title>
</head><body><b>Quick win Enumeration - No tools</b><br/>
<br/>
Basic process for quick wins<br/>
<br/>
1. figure out who I am<br/>
2. what is the architectuer of the system<br/>
3. waht sudo priveldges do I have<br/>
4. what is the history<br/>
<br/>
<br/>
<b>System Enumeration</b><br/>
<br/>
<br/>
<b>hostname</b>- quick look at type of machine<br/>
<br/>
<b>uname - a</b>- will provide taht and what kernal/version its running<br/>
<br/>
<b>cat /proc/version</b>- also p[rovides kernal data<br/>
<br/>
<b>cat /etc/issue</b>- give distribution and version<br/>
<br/>
<b>lscpu</b>- provides CPU data &amp; articeture<br/>
<br/>
<b>ps aux</b>- what services are running<ul><li style="list-style-type: none">look for inmdicators that may be useful, IE inditcators of a webserver running, file shares, cron etc</li>
<li style="list-style-type: none"/>
</ul>
<br/>
<br/>
<b>User Enumeration</b><br/>
<br/>
<br/>
<b>whoami</b>- get current user<br/>
<b><br/>
</b><b>id</b>- current user with additonal info about groups<br/>
<br/>
<b>sudo -l</b>- what cammands can be run as root without password<br/>
<br/>
<b>cat /etc/passwd</b>- provides a list of users<br/>
<br/>
<b>cat /etc/shadow</b>- the passwords for the users<br/>
<br/>
<b>cat /etc/group</b>- a list of allt he user groups<br/>
<br/>
<b>history</b>- a list of all previously run commands by that user<br/>
<br/>
<b>sudo su -</b>- can we change user. is it allowed<br/>
<br/>
<br/>
<b>Network Enumeration</b><br/>
<br/>
Important to id network architecurte. ID internally open ports etc.<br/>
<br/>
<b>ifconfig</b>or <b>ip a</b>- Check system ip address, id connection to internal networks. how many NICs<br/>
<br/>
<b>ip route</b>- routing to other systems/networks<br/>
<br/>
<b>arp -a</b>or <b>ip neigh</b>- see who the machine is talking to<br/>
<br/>
<b>netstat -ano</b>- id what ports are open adn what communications channels exist. can see internally open ports<br/>
<br/>
<br/>
<b>Password Hunting<br/>
<br/>
</b>quick win - get good at searching through files.<b><br/>
</b><br/>
using search features to find passwords saved or entered throughout the system<br/>
<br/>
<b>grep --color=auto -rnw '/' -ie &quot;PASSWORD&quot; --color=always 2&gt; /dev/null</b>- will search sytem everywhere for the word &quot;PASSWORD&quot; and output it. Try things &quot;PASS&quot; &quot;PASSWORD=&quot;<br/>
<br/>
<br/>
<b>locate password | more</b>- again try variations. we are looking for passwords saved<br/>
<br/>
<b>find / -name authorized_keys <br/>
<br/>
find / -name id_rsa 2&gt;/dev/null<br/>
<br/>
<br/>
<br/>
<br/>
</b></body></html>