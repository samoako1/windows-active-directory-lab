# Lab Setup

## Purpose

This lab was designed to simulate a small Windows enterprise environment and demonstrate foundational Windows infrastructure, identity management, and access control concepts.

The environment was built using VMware Workstation Pro with a Windows Server domain controller and a Windows 11 domain client.

## Virtualized Environment

| System | Role | IP Address |
|---|---|---|
| DC01 | Domain Controller / DNS Server | `192.168.222.140` |
| WIN11-01 | Windows 11 Domain Client | `192.168.222.131` |

Both systems were configured on the same VMware NAT network.

## Network Configuration

The virtual machines communicate through the VMware NAT network.

| Setting | Configuration |
|---|---|
| Network | `192.168.222.0/24` |
| Gateway | `192.168.222.2` |
| Domain Controller | `192.168.222.140` |
| Windows 11 Client | `192.168.222.131` |

DC01 was assigned a static IPv4 address to provide a consistent endpoint for Active Directory and DNS services.

## Domain Controller

The Windows Server virtual machine was configured as the primary domain controller for the environment.

The server was named:

```text
DC01
```

The server was promoted to a Domain Controller after installing Active Directory Domain Services.

The Active Directory domain was configured as:

```text
corp.local
```

DC01 provides the following core services:

- Active Directory Domain Services
- DNS
- Domain authentication
- Centralized identity management
- User and group management
- Organizational Unit management
- Group Policy management
- Domain controller discovery

## Domain Client

A Windows 11 virtual machine was deployed as the primary domain client.

The workstation was named:

```text
WIN11-01
```

The client was joined to the `corp.local` domain and used to validate domain authentication, DNS resolution, Group Policy deployment, and access to shared resources.

A domain user account was used to authenticate to the workstation:

```text
CORP\john.smith
```

## DNS Configuration

DC01 was configured to provide DNS services for the Active Directory domain.

The domain controller was configured to use itself as the primary DNS server:

```text
127.0.0.1
```

WIN11-01 was configured to use DC01 as its DNS server:

```text
192.168.222.140
```

This configuration allows the Windows 11 client to resolve domain resources and locate Active Directory services.

## Active Directory Domain Services

Active Directory Domain Services was installed on DC01 and the server was promoted to a Domain Controller.

The resulting domain structure provided centralized management of:

- Users
- Security groups
- Organizational Units
- Computers
- Authentication
- Group Policy
- Resource permissions

## Organizational Structure

The `corp.local` domain was organized using dedicated Organizational Units:

```text
corp.local
├── Employees
├── IT
├── HR
├── Computers
└── Domain Controllers
    └── DC01
```

This structure provides logical separation of users and systems and allows policies and administrative permissions to be applied based on organizational roles.

## Network Connectivity Validation

Connectivity between the Windows 11 client and domain controller was validated using:

```cmd
ping 192.168.222.140
```

Successful replies confirmed basic network connectivity between WIN11-01 and DC01.

## DNS Validation

DNS resolution was tested from WIN11-01 using:

```cmd
nslookup DC01.corp.local
```

The query successfully resolved the domain controller to:

```text
192.168.222.140
```

This confirmed that the Windows 11 client was correctly using the domain controller for DNS resolution.

## Domain Controller Discovery

The Windows 11 client was tested to ensure it could locate the Active Directory domain controller using:

```cmd
nltest /dsgetdc:corp.local
```

The command successfully returned DC01 as the domain controller for the `corp.local` domain.

This confirmed successful communication between the domain client and Active Directory infrastructure.

## Domain Authentication Validation

Domain authentication was verified on WIN11-01 using:

```cmd
whoami
```

The resulting domain account was:

```text
corp\john.smith
```

This confirmed that the Windows 11 client was successfully authenticating users through the `corp.local` domain.

## Lab Objectives

The completed environment was designed to demonstrate the following enterprise IT and Active Directory concepts:

- Windows Server administration
- Active Directory Domain Services
- Active Directory-integrated DNS
- Domain controller deployment
- Windows 11 domain joining
- Centralized authentication
- Organizational Unit management
- User and security group administration
- Group Policy
- SMB shared resources
- NTFS permissions
- Delegated administration
- Least-privilege access control
- Windows networking and troubleshooting

## Validation Tools

The following Windows tools and commands were used throughout the lab to validate the environment:

- `ipconfig`
- `ping`
- `nslookup`
- `nltest`
- `dcdiag`
- `whoami`
- `gpupdate`
- `gpresult`
- Active Directory Users and Computers
- Group Policy Management

## Environment Summary

The completed environment consists of a Windows Server domain controller providing Active Directory and DNS services to a Windows 11 domain client.

The resulting architecture provides a foundation for centralized identity management, authentication, policy enforcement, file-sharing permissions, and delegated administrative operations within the `corp.local` domain.
