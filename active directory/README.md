**Active Directory Theory**

<br/>
**OVERVIEW**
<br/>
like a phone book. Book is filled with objects. IE printers, computers users etc<br/>
<br/>
Authenticates useing Kerberos tickets<br/>
Non windows devices can also authenticate to Acitve Directory. IE Firewall.<br/>
<br/>
Allows multiple devices/services to be accessed by a user using the same username and password. genereally entered once during intial log on.<br/>
<br/>
Most commonly used identiy management in the world.<br/>
<br/>
95% Fortune 1000 companies implement AD.<br/>
<br/>
Can be exploited by abusing featuyres as opposed to patchable exploits.<br/>
<br/>
<br/>
<br/>
PHYSICAL AD COMPONENETS<br/>
<br/>
Active Directory Domain Services<br/>
<br/>
Domain controller <br/>
- a server hosting the the copy of the AD DS directoryu store<br/>
- provides authenticationa nd authorisation services<br/>
- replicate updates to other domain cotrollers in domain and forest<br/>
- allow admin access to manage user accounts and network resources<br/>
<br/>
<br/>
During real world - dont just focus on compromosing domain. Client will want a complete picture<br/>
<br/>
AD DS Data store<br/>
- contains teh DB files and process that sotre and amnage directory infomraotin for users, services and applicaitons<br/>
- consists of the Ntds.dit file<br/>
- defualt stored in %SystemRoot%\NTDS folder on all domain controllers<br/>
- Is accessible only thorugh the comain cotroller processes and protocols<br/>
<br/>
<br/>
LOGICAL AD COMPONENETS<br/>
<br/>
AD DS Schema<br/>
<br/>
Defines the rules for object creation<br/>
<br/>
Domains<br/>
<br/>
Used to group and manage objects<br/>
- like a domain controller.. smaller<br/>
<br/>
Tress<br/>
A heirachy of domains in AD DS<br/>
- Shares namespace<br/>
- shares trust<br/>
<br/>
Forest<br/>
a copllection of one or more domain trees<br/>
<br/>
<br/>
Organizational Units (Ous)<br/>
Active directory containers that can contain users, groups, compuiters and other Ous<br/>
<br/>
Trust<br/>
method for users to gain acess to resources in another domain<br/>
- Directional Trust flow from trusting domain to trusted domain<br/>
- Transititve trust relationship is extended beyond the 2 domain trust to include other trusted domains (will trust everything the otehr domain trusts)<br/>
<br/>
Objects<br/>
User - Enables network access to user<br/>
InetOrgPerson - similar to user accouns. Used for compatibility with other directory servies<br/>
Contacts - used to primarily assign e-mail addresses to external users. Does not enable netowrk access<br/>
Groups - Used to simplify the admin of access control<br/>
Computers - Enable authentication and auditing of computers acces to resources<br/>
Printers - Used to simplify the process of locating and connecting to printers<br/>
Share folders - Enable users to search for shared folders based on properties<br/>
<br/>
<br/>
