# Active Directory Configuration



## Overview



Active Directory Domain Services (AD DS) was configured on DC01 to provide centralized identity, authentication, authorization, and administrative management for the `corp.local` domain.



The Active Directory environment was designed to simulate a small enterprise network with separate organizational units, users, security groups, and administrative roles.



## Domain Information



| Setting | Configuration |

|---|---|

| Domain | corp.local |

| Forest | corp.local |

| Domain Controller | DC01 |

| Domain Controller IP | 192.168.222.140 |

| Client Computer | WIN11-01 |

| Client IP | 192.168.222.131 |



## Organizational Unit Structure



The `corp.local` domain was organized into dedicated Organizational Units (OUs):



```text

corp.local

├── Employees

├── IT

├── HR

├── Computers

└── Domain Controllers

&#x20;   └── DC01

```



The Organizational Units provide logical separation between different categories of users and systems.



This structure also provides a foundation for applying Group Policy and delegated administrative permissions based on organizational roles.



## Employees OU



The `Employees` OU contains standard employee accounts.



The OU was used to organize regular domain users and served as the scope for several administrative and security configurations.



Example employee account:



```text

CORP\\john.smith

```



The employee account was used throughout the lab to validate domain authentication and resource access.



## IT OU



The `IT` OU was created to organize IT-related users and administrative accounts.



The environment also includes an `IT Helpdesk` security group used to demonstrate delegated administration.



The Helpdesk role was intentionally given limited permissions rather than unrestricted Domain Administrator privileges.



## HR OU



The `HR` OU was created to organize human resources users.



The HR organizational structure was also used when configuring access to department-specific shared resources.



\## Computers OU



A `Computers` container was present within the domain for computer accounts.



The Windows 11 client was joined to the `corp.local` domain and used as the primary workstation for testing domain authentication, Group Policy, and shared resource access.



\## Domain Controllers OU



The `Domain Controllers` OU contains the domain controller computer account:



```text

DC01

```



This OU is automatically created by Active Directory and is used to organize domain controller computer accounts and apply domain controller-specific policies.



\## User Accounts



Domain user accounts were created through Active Directory Users and Computers.



The accounts were organized according to their appropriate organizational roles.



Example:



```text

CORP\\john.smith

```



The account was used to demonstrate:



\- Domain authentication

\- Access to shared resources

\- NTFS permission enforcement

\- Group-based access control

\- Group Policy application



\## Security Groups



Security groups were created to support role-based access control.



Groups allow permissions to be assigned to a collection of users instead of configuring access individually for every account.



The general access model used in the lab was:



```text

User

&#x20; │

&#x20; ▼

Security Group

&#x20; │

&#x20; ▼

Resource

&#x20; │

&#x20; ▼

Permissions

```



This approach improves consistency and simplifies future administration.



\## Domain Authentication



Domain authentication was validated from WIN11-01 using:



```cmd

whoami

```



The resulting account was:



```text

corp\\john.smith

```



This confirmed that the Windows 11 workstation was successfully authenticating the user through the `corp.local` domain.



\## Domain Controller Discovery



The Windows 11 client was tested to verify that it could locate the domain controller using:



```cmd

nltest /dsgetdc:corp.local

```



The command successfully returned:



```text

DC: \\\\DC01.corp.local

Address: \\\\192.168.222.140

Dom Name: corp.local

Forest Name: corp.local

```



This confirmed that WIN11-01 could successfully locate and communicate with the Active Directory domain controller.



\## DNS Integration



Active Directory relies on DNS for domain controller discovery and service location.



The environment was tested using:



```cmd

nslookup DC01.corp.local

```



The domain controller successfully resolved to:



```text

192.168.222.140

```



Active Directory DNS service records were also verified using:



```cmd

nslookup -type=SRV \_ldap.\_tcp.dc.\_msdcs.corp.local

```



The successful response identified DC01 as the LDAP service for the domain.



\## Active Directory Health Validation



The health of the domain controller and Active Directory DNS environment was validated using:



```cmd

dcdiag /test:dns

```



The test successfully completed for DC01 and the `corp.local` domain.



This provided an additional validation that the domain controller and its DNS configuration were functioning correctly.



\## Administrative Tools



Active Directory administration was performed using:



\- Active Directory Users and Computers

\- Group Policy Management

\- Windows Server administrative tools

\- Command-line diagnostic utilities



Active Directory Users and Computers was used to manage:



\- Users

\- Security groups

\- Organizational Units

\- Computer accounts

\- Delegated permissions



\## Access Control Model



The environment was designed around centralized, group-based access control.



Users receive access through their membership in appropriate security groups rather than through individually assigned permissions whenever possible.



This supports the principle of least privilege and provides a more manageable enterprise configuration.



\## Key Concepts Demonstrated



\- Active Directory Domain Services

\- Domain controller administration

\- Organizational Units

\- Domain user management

\- Security group management

\- Domain authentication

\- Domain controller discovery

\- Active Directory-integrated DNS

\- Group-based access control

\- Role-based administration

\- Least-privilege access

\- Active Directory troubleshooting

