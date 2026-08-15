\# User and Group Management



\## Overview



Active Directory users, security groups, and Organizational Units were configured to demonstrate centralized identity management and role-based access control within the `corp.local` domain.



The structure was designed to simulate a basic enterprise environment where users are organized by department and access to resources is controlled through security groups.



\## Organizational Units



The domain contains dedicated Organizational Units for different organizational roles:



```text

corp.local

├── Employees

├── IT

├── HR

├── Computers

└── Domain Controllers

&#x20;   └── DC01

```



Organizational Units provide logical containers for users and computers.



They also provide a scope for applying Group Policy and delegating administrative permissions.



\## Employee Accounts



User accounts were created within the appropriate Organizational Units to represent domain employees.



A primary test account used throughout the lab was:



```text

CORP\\john.smith

```



The account was used to validate:



\- Domain authentication

\- Group membership

\- Shared resource access

\- NTFS permissions

\- Group Policy application



\## Security Groups



Security groups were created to support role-based access control.



Instead of assigning permissions directly to individual users, users can be placed into security groups that are assigned access to specific resources.



The general access model is:



```text

User

&#x20; │

&#x20; ▼

Security Group

&#x20; │

&#x20; ▼

Shared Resource

&#x20; │

&#x20; ▼

NTFS Permissions

```



This approach makes permissions easier to manage as the environment grows.



\## Departmental Organization



The environment includes organizational structures for:



\- Employees

\- IT

\- HR



These organizational roles were used to demonstrate how Active Directory can separate users and administrative responsibilities.



\## Group-Based Access Control



Department-specific access was configured through security groups.



For example, users who require access to an HR resource can be placed into the appropriate HR security group rather than receiving individual permissions.



This provides a scalable approach to managing access.



\## Domain Authentication



The Windows 11 client was used to verify successful domain authentication.



The currently logged-in account was verified using:



```cmd

whoami

```



The resulting account was:



```text

corp\\john.smith

```



This confirmed that the user was authenticated through the `corp.local` domain.



\## Domain Controller Discovery



The Windows 11 client was tested to verify that it could locate the Active Directory domain controller using:



```cmd

nltest /dsgetdc:corp.local

```



The command successfully identified:



```text

DC01.corp.local

```



at:



```text

192.168.222.140

```



This confirmed successful communication between the domain client and Active Directory infrastructure.



\## User Account Management



User accounts were created and managed using Active Directory Users and Computers.



Administrative tasks included:



\- Creating user accounts

\- Assigning users to Organizational Units

\- Managing security group membership

\- Resetting passwords

\- Managing account properties

\- Testing domain authentication



\## Security Group Management



Security groups were used to organize users according to their required access and administrative responsibilities.



Examples of roles represented in the environment include:



```text

Employees

IT

HR

IT Helpdesk

```



Group membership allows access permissions and administrative rights to be managed centrally.



\## Access Control Benefits



Group-based access control provides several advantages:



\- Centralized permission management

\- Easier onboarding and offboarding

\- Reduced administrative overhead

\- Consistent access policies

\- Improved scalability

\- Support for least-privilege access



For example, removing a user from a security group can immediately remove access to resources associated with that group.



\## Administrative Tools



User and group management was performed using:



\- Active Directory Users and Computers

\- Group Policy Management

\- Windows Server administrative tools

\- Command-line diagnostic utilities



Active Directory Users and Computers provided the primary graphical interface for managing users, groups, and Organizational Units.



\## Validation



The user and group configuration was validated by authenticating domain users from WIN11-01 and testing access to domain resources.



The following commands were used during validation:



```cmd

whoami

```



and:



```cmd

nltest /dsgetdc:corp.local

```



Successful results confirmed that the client could authenticate users and locate the domain controller.



\## Key Concepts Demonstrated



\- Active Directory user management

\- Security group management

\- Organizational Unit management

\- Domain authentication

\- Role-based access control

\- Group-based permissions

\- Centralized identity management

\- Domain controller discovery

\- User account administration

\- Security group administration

\- Least-privilege access control

