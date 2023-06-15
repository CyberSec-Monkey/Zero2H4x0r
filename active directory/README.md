# Active Directory Theory

**OVERVIEW**
Active Directory (AD) functions as a centralized directory service, similar to a phone book, containing various objects such as printers, computers, and users. Here are some key points to understand:

- AD authenticates users through Kerberos tickets.
- It enables non-Windows devices, like firewalls, to authenticate to the Active Directory.
- Users can access multiple devices/services using the same username and password, which are entered once during initial login.
- AD is the most widely used identity management system globally, with around 95% of Fortune 1000 companies implementing it.
- Exploitation of AD often involves abusing its features rather than relying on patchable vulnerabilities.

## PHYSICAL AD COMPONENTS

### Active Directory Domain Services

Domain Controller:
- A server that hosts a copy of the AD DS directory store.
- Provides authentication and authorization services.
- Replicates updates to other domain controllers in the domain and forest.
- Allows administrators to manage user accounts and network resources.

AD DS Data Store:
- Consists of database files and processes that store and manage directory information for users, services, and applications.
- The primary database file is called Ntds.dit and is stored in the %SystemRoot%\NTDS folder on domain controllers.
- Access to the data store is restricted to domain controller processes and protocols.

## LOGICAL AD COMPONENTS

### AD DS Schema

The AD DS Schema defines the rules for creating objects within the Active Directory.

### Domains

Domains are used to group and manage objects within the Active Directory. They provide administrative boundaries and security boundaries. A domain controller manages each domain.

### Trees

Trees represent a hierarchy of domains within the Active Directory. Domains within a tree share a common namespace and trust relationship.

### Forest

A forest is a collection of one or more domain trees in the Active Directory. It represents the top-level structure of the AD and provides a security boundary.

### Organizational Units (OUs)

Organizational Units (OUs) are containers within the Active Directory that organize and manage objects such as users, groups, computers, and other OUs. OUs help in applying Group Policies and delegating administrative control.

### Trust

Trust is a method for users to gain access to resources in another domain. It establishes a relationship between the trusting domain and the trusted domain. Trust relationships can be transitive, allowing access across multiple trusted domains.

### Objects

- User: Represents a user account and enables network access for users.
- InetOrgPerson: Similar to user accounts, used for compatibility with other directory services.
- Contacts: Primarily used to assign email addresses to external users, without enabling network access.
- Groups: Used to simplify the administration of access control by grouping users or other objects together.
- Computers: Enable authentication and auditing of computer access to resources.
- Printers: Used to simplify the process of locating and connecting to printers.
- Shared Folders: Enable users to search for shared folders based on properties.
