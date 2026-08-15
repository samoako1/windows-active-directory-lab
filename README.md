\# Windows Enterprise Active Directory Lab



A virtualized Windows enterprise environment built to demonstrate Active Directory administration, centralized identity management, DNS, Group Policy, access control, shared resources, and delegated helpdesk administration.



\## Overview



This project simulates a small enterprise Windows environment using VMware Workstation Pro, Windows Server, and Windows 11.



The environment was designed to demonstrate common IT infrastructure and identity management workflows, including domain authentication, Organizational Unit administration, security groups, file sharing, Group Policy deployment, and delegated administrative access.



\## Objectives



\- Deploy Windows Server as an Active Directory Domain Controller

\- Configure Active Directory Domain Services (AD DS)

\- Configure integrated DNS

\- Deploy and join a Windows 11 domain client

\- Configure Organizational Units, users, and security groups

\- Implement group-based access control

\- Configure SMB shared resources and NTFS permissions

\- Deploy and verify Group Policy

\- Implement delegated helpdesk administration

\- Validate authentication, DNS, policy, and access controls



\## Environment



| Component | Configuration |

|---|---|

| Hypervisor | VMware Workstation Pro |

| Domain Controller | DC01 |

| Server OS | Windows Server |

| Client | WIN11-01 |

| Client OS | Windows 11 |

| Domain | corp.local |

| Network | VMware NAT |

| AD DS | Active Directory Domain Services |

| DNS | Windows Server DNS |

| File Sharing | SMB |

| Policy | Group Policy |

| Access Control | NTFS + Security Groups |



\## Architecture



```text

&#x20;                VMware Workstation Pro

&#x20;                        │

&#x20;                 VMware NAT Network

&#x20;                 192.168.222.0/24

&#x20;                        │

&#x20;         ┌──────────────┴──────────────┐

&#x20;         │                             │

&#x20;      DC01                         WIN11-01

&#x20; 192.168.222.140                192.168.222.131

&#x20;         │                             │

&#x20; Windows Server                  Windows 11

&#x20;         │                             │

&#x20;    AD DS + DNS                 Domain Client

&#x20;         │                             │

&#x20;      corp.local ◄─────────────────────┤

&#x20;         │

&#x20;    ┌────┼─────────┐

&#x20;    │    │         │

&#x20;   OUs Users     Groups

&#x20;    │

&#x20;   GPOs

&#x20;    │

&#x20;SMB Shares

&#x20;    │

Delegated Administration

\## Active Directory



The `corp.local` domain contains dedicated Organizational Units for:



\- Employees

\- IT

\- HR

\- Domain Controllers



User accounts and security groups were configured to support role-based administration and resource access.



\## Shared Resources



Department-specific SMB shares were configured with NTFS permissions.



Access was tested using domain accounts to demonstrate both authorized and unauthorized access.



\## Group Policy



A `Corporate Security Policy` GPO was created and linked to the Employees OU.



The policy demonstrates centralized Windows security configuration including:



\- Password requirements

\- Account lockout controls

\- Policy deployment to domain clients



The resulting policy application was verified from the Windows 11 client.



\## Delegated Administration



An `IT Helpdesk` security group was created and delegated permission to reset user passwords within the Employees OU.



The delegation was validated using a dedicated Helpdesk account without granting unrestricted domain administrative privileges.



\## Validation



The environment was validated using:



\- `ping`

\- `nslookup`

\- `nltest`

\- `dcdiag`

\- `gpupdate`

\- `gpresult`

\- Active Directory Users and Computers

\- Group Policy Management

\- SMB access testing



\## Key Skills Demonstrated



\- Windows Server administration

\- Active Directory Domain Services

\- DNS administration

\- Domain authentication

\- Organizational Unit management

\- User and group administration

\- Security groups

\- Group-based access control

\- NTFS permissions

\- SMB file sharing

\- Group Policy

\- Delegated administration

\- Least-privilege access control

\- Windows networking and troubleshooting



\## Documentation



Detailed configuration procedures, validation steps, and screenshots are available in the `docs/` and `screenshots/` directories.



\## Future Improvements



Potential extensions include:



\- Additional Windows domain clients

\- DHCP configuration

\- Fine-Grained Password Policies

\- Additional delegated administration roles

\- Windows Server redundancy

\- Certificate Services

