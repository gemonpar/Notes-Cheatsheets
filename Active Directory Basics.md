# Active Directory Basic Concepts
Active Directory is a technology designed by Microsoft which objective is to define a bunch of centralized objects 
whose are the components of a network.

## Domain
The domain represents a logic grouping of a set of computers connected on a network which share an Active Directory
database. The database is probably the most important element in an AD and is managed by the central servers in the 
domain, also known as Domain Controllers. A domain is basically a tag that typically represents a DNS name.

## Domain Controllers
These are Windows Server-based systems that can access and manipulate the AD database.  each domain has at least one 
controller and it is possible to install more domain controllers dedicated to processing requests from stations if is
needed. You can also create subdomains so that users can access resources in other subdomains that are part of the 
same Forest.

## Forest
It is the set of all subdomains (including the root domain) and its name is the same as that of the root domain. 

## Netbios Name
A domain can be represented by its corresponding DNS name and also by its NetBIOS name. The netbios name is usually 
used in multiple operations, a typical case can be the login process on a workstation using one user of the domain.

## Operating level
There is a minimum mode of operation, this dictates which features can be used in the forest or domains.The mode mapping 
allows you to define the minimum version of windows server that must be met by the DCs that you intend to manage the AD.

## Trusts
Users can access resources from other domains in the same Forest thanks to the concept of Trust. Trusts represent a 
connection between two domains, however it is a logical connection based on authorization mechanisms and does not 
refer to a network connection. 

"Trust" objects have a sense that determines which domain you trust and which is the trusted domain. When one domain 
is trusted for another, the Trust object is of type "Inbound" or "Incoming". When one domain trusts another, the Trust 
object is of type "Outbound" or "Outcoming". Each trust can be unidirectional or bidirectional and transitive or non-transitive.

###  Types of Trust
- **Hierarchical:** Between a parent domain and a child domain.
- **Forest:** A domain in one forest can access resources from another domain in another forest.
- **External:** Direct trust between domains from different forests.
- **Realm:** Connect an AD with a windowless domain.
- **Shortcut:** When 2 domains in the same forest communicate constantly but are not directly connected, this type of Trust
can be created to avoid “jumping” over different Trusts.

### Trust Transitivity
Trust objects can be transitive or non-transitive. Non-transitive trust only affects the two ends of the relationship (trusting 
domain and trusting domain). On the other hand, transitive trust relationships can act as a bridge and be used by a third party 
to access the resources of the trusted domain. In this way, any domain in the Forest can traverse trust relationships and access 
other domains in the same Forest, this is also known as “intra-forest” relationships.

## Users
Active Directory manages users in the environment by treating them as a special type of object that is stored in the central database.
Important conpcepts about a domain user:
- Although the username serves to identify you, the SID (Security Identifier) can also be used for this purpose. The SID is the 
combination of the Domain SID and the RID (Relative Identifier). Some tools show the SID instead of the username.
- User secrets are elements used by the Domain Controller to carry out the authentication process. The Passwords are not 
stored in plain text, but user secrets derived from them are, which are NT Hashes and Kerberos keys.
- The LM and NT hashes are stored in two places: the Windows SAM (Security Account Manager) and the AD database, 
which by default is available on DCs in the path C:\Windows\NTDS\ntds.dit.
- Although NT hashes are not passwords, they can be used in some cases for Pass-The-Hash/Overpass-The-Hash attacks.
- Computers registered in an AD are also represented by a user account, which is the name of the workstation with a "$" at the end.
- User Account Control is one of the properties of the User class (not to be confused with the User Account Control mechanism for 
preventing programs from running in elevated contexts). This property is made up of a series of attributes that are relevant to the 
security of the user account and the domain, especially the DONT_REQUIRE_PREAUTH property, since it means that the account does not 
require Kerberos pre-authentication.
- Probably the most important user accounts are Administrator and krbtgt. The first one has high privileges in the system and the 
second one allows the encryption of TGT tickets, which means that if an attacker compromises said account, they will be able to create 
this type of tickets without any problem. This technique is known as Golden Ticket.

## Groups
Groups are stored in the AD database and can be identified by the SID or SamAccountName attribute. One of the most important groups is Domain
Admins, therefore, checking which users are part of said group is important for the attacker. Another important group is the Enterprise Admins group, 
since it allows all its members to have administrator permissions throughout the Forest. Unlike Domain Admins, the EnterpriseAdmins group is defined 
only in the Root Domain of the Forest.

There are three types of groups:
- **Universal Groups:** Groups that have members from the same forest and grant permissions in the forest and trusted forests. The Enterprise Admins group is a Universal Group.
- **Global Groups:** Groups that have members from the same domain and grant permissions in the forest and trusted domains. The Domain Admins group is a Global Group.
- **DomainLocal Groups:** You can have members of the domain or any trusted domain and grant permissions only in the domain. The Administrators group is a DomainLocal Group.

## NTDS Database
The database of an AD contains all the objects that are available in the environment and is shared/synchronized with all DCs. By default, 
it is located in the file C:\Windows\NTDS\ntds.dit on each DC.

The NTDS has two main features:
- It is a distributed database.
- It has an object-based structure and class hierarchies.

The fundamental element of the database are the classes, which are composed of a set of properties and inheritance relationships. 
The most important classes are: User, Computer and Group.
