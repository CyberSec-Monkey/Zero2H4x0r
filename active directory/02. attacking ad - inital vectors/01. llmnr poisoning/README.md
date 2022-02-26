**Attacking AD - Initla Vectors**
<br/>
Inital attempts to attack AD<br/>
<br/>
Have to find a wat into the network<br/>
<br/>
abuse windows features<br/>
<br/>
Heaths reccomended article<br/>
https://adam-toscher.medium.com/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa<br/>
<br/>
<br/>
<br/>
ATTACKS<br/>
<br/>
LLMNR POISONING<br/>
link local multi name resolution<br/>
basically DNS when DNS fails<br/>
<br/>
<br/>
What is it - used to ID hosts when DNS fails<br/>
<br/>
key flaw - uses a user's username and NTLMv2 hash when appropriatly responded to<br/>
<br/>
<br/>
Basic overview.. a request is sent from victim to the server asking to connect to a source<br/>
server doesnt know what/where...<br/>
<br/>
Victim broadcasts request for connect to service<br/>
<br/>
Attacker conducting a MitM attack responds and requests creds on premise it will connect<br/>
<br/>
Uses RESPONDER<br/>
<br/>
Best to run early morning or post lunch. requires a lot of traffic<br/>
<br/>
Hashs are captured<br/>
<br/>
HASHCAT to attempt to crack<br/>
<br/>
<br/>
CONDUCTING THE ATTACK<br/>
<br/>
boot repsonder<br/>
<br/>
syntax &gt; sudo responder -I eht0 -rdwv <br/>
<br/>
Forcing traffic from victim to attacker (to generate some capturabel traffic)<br/>
<br/>
results in win<br/>
<br/>
<img height="200" src="image.png" width="646"/><br/>
<br/>
Normal circumstances... wait and MitM<br/>
<br/>
Time to crack HASHCAT<br/>
<br/>
-m 5600 + NetNTLMv2<br/>
<br/>
--force to force it to run despite being in a vm adn using CPU<br/>
<br/>
I was lucky and mine ran. YOu should run on base OS and use GPU. Hashcat can be downloaded for windows<br/>
<br/>
<br/>
<img height="300" src="image 2.png" width="691"/><br/>
<br/>
windows &gt; run in comand prompt as admin<br/>
<br/>
syntax &gt; &lt;exe name&gt;.exe -m &lt;module no&gt; &lt;hash file&gt; &lt;wordlist file&gt; -O<br/>
<br/>
<br/>
LLMNR Poisoning Defenses<br/>
<br/>
<br/>
Turn off LLMNR AND NBT-NS (NBT-NS is the back up for when LLMNR fails)<br/>
<br/>
If cant or wont disable LLMNR<br/>
<br/>
Then enable Network access control...<br/>
MAC whitelisting<br/>
<br/>
Strong password policy ENFORCED<br/>
<br/>
