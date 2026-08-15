# Windows Enterprise Active Directory Lab

A virtualized Windows enterprise environment built to demonstrate Active Directory administration, centralized identity management, DNS, Group Policy, access control, shared resources, and delegated helpdesk administration.

## Overview

This project simulates a small enterprise Windows environment using VMware Workstation Pro, Windows Server, and Windows 11.

The environment was designed to demonstrate common IT infrastructure and identity management workflows, including domain authentication, Organizational Unit administration, security groups, file sharing, Group Policy deployment, and delegated administrative access.

## Objectives

- Deploy Windows Server as an Active Directory Domain Controller
- Configure Active Directory Domain Services (AD DS)
- Configure integrated DNS
- Deploy and join a Windows 11 domain client
- Configure Organizational Units, users, and security groups
- Implement group-based access control
- Configure SMB shared resources and NTFS permissions
- Deploy and verify Group Policy
- Implement delegated helpdesk administration
- Validate authentication, DNS, policy, and access controls

## Environment

| Component | Configuration |
|---|---|
| Hypervisor | VMware Workstation Pro |
| Domain Controller | DC01 |
| Server OS | Windows Server |
| Client | WIN11-01 |
| Client OS | Windows 11 |
| Domain | `corp.local` |
| Network | VMware NAT |
| AD DS | Active Directory Domain Services |
| DNS | Windows Server DNS |
| File Sharing | SMB |
| Policy | Group Policy |
| Access Control | NTFS + Security Groups |

## Architecture

```text
                 VMware Workstation Pro
                         │
                  VMware NAT Network
                  192.168.222.0/24
                         │
          ┌──────────────┴──────────────┐
          │                             │
        DC01                         WIN11-01
   192.168.222.140                192.168.222.131
          │                             │
    Windows Server                  Windows 11
          │                             │
     AD DS + DNS                  Domain Client
          │                             │
       corp.local ◄────────────────────┤
          │
     ┌────┼─────────┐
     │    │         │
    OUs  Users    Groups
     │
    GPOs
     │
 SMB Shares
     │
Delegated Administration
```

## Active Directory

The `corp.local` domain contains dedicated Organizational Units for:

- Employees
- IT
- HR
- Domain Controllers

User accounts and security groups were configured to support role-based administration and resource access.

For detailed configuration information, see [`docs/active-directory.md`](docs/active-directory.md).

## User and Group Management

Users and security groups were created and organized according to their organizational roles.

Group-based access control was used to manage permissions and support a scalable least-privilege model.

For more information, see [`docs/user-and-group-management.md`](docs/user-and-group-management.md).

## Shared Resources

Department-specific SMB shares were configured with NTFS permissions.

Access was tested using domain accounts to demonstrate both authorized and unauthorized access.

The environment included General, IT, and HR shared resources, with restricted access applied to department-specific resources.

For more information, see [`docs/shared-resources.md`](docs/shared-resources.md).

## Group Policy

A `Corporate Security Policy` GPO was created and linked to the Employees OU.

The policy demonstrates centralized Windows security configuration, including:

- Password requirements
- Account lockout controls
- Policy deployment to domain clients

The resulting policy application was verified from the Windows 11 client using `gpupdate` and `gpresult`.

For more information, see [`docs/group-policy.md`](docs/group-policy.md).

## Delegated Administration

An `IT Helpdesk` security group was created and delegated permission to reset user passwords within the Employees OU.

The delegation was validated using a dedicated Helpdesk account without granting unrestricted domain administrative privileges.

This demonstrates role-based administration and the principle of least privilege.

For more information, see [`docs/delegated-administration.md`](docs/delegated-administration.md).

## Validation

The environment was validated using:

- `ping`
- `ipconfig`
- `nslookup`
- `nltest`
- `dcdiag`
- `whoami`
- `gpupdate`
- `gpresult`
- Active Directory Users and Computers
- Group Policy Management
- SMB access testing
- NTFS permission testing

For detailed validation procedures and results, see [`docs/validation-and-testing.md`](docs/validation-and-testing.md).

## Key Skills Demonstrated

- Windows Server administration
- Active Directory Domain Services
- DNS administration
- Domain authentication
- Organizational Unit management
- User and group administration
- Security group management
- Group-based access control
- NTFS permissions
- SMB file sharing
- Group Policy
- Delegated administration
- Least-privilege access control
- Windows networking and troubleshooting

## Project Documentation

Detailed configuration procedures, validation steps, and supporting screenshots are available throughout the repository.

### Documentation

- [`Lab Setup`](docs/lab-setup.md)
- [`Active Directory Configuration`](docs/active-directory.md)
- [`User and Group Management`](docs/user-and-group-management.md)
- [`Shared Resources`](docs/shared-resources.md)
- [`Group Policy`](docs/group-policy.md)
- [`Delegated Administration`](docs/delegated-administration.md)
- [`Validation and Testing`](docs/validation-and-testing.md)

### Screenshots

Supporting screenshots are organized in the [`screenshots/`](screenshots/) directory.

## Future Improvements

Potential extensions include:

- Additional Windows domain clients
- DHCP configuration
- Fine-Grained Password Policies
- Additional delegated administration roles
- Windows Server redundancy
- Certificate Services
