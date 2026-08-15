# Validation and Testing

## Overview

The Active Directory environment was validated from both the Windows Server domain controller and the Windows 11 domain client.

Testing focused on network connectivity, DNS resolution, domain controller discovery, domain authentication, Active Directory health, Group Policy application, and SMB resource access.

## Network Connectivity

Basic network connectivity between WIN11-01 and DC01 was tested using:

```cmd
ping 192.168.222.140
```

The Windows 11 client successfully received replies from DC01.

This confirmed that the two virtual machines could communicate over the VMware NAT network.

## DNS Resolution

DNS resolution was tested from WIN11-01 using:

```cmd
nslookup DC01.corp.local
```

The query successfully returned:

```text
Name:    DC01.corp.local
Address: 192.168.222.140
```

This confirmed that the Windows 11 client was correctly using DC01 as its DNS server.

## Domain Controller Discovery

The Windows 11 client was tested to verify that it could locate the domain controller using:

```cmd
nltest /dsgetdc:corp.local
```

The command successfully returned DC01 as the domain controller for the `corp.local` domain.

Example result:

```text
DC: \\DC01.corp.local
Address: \\192.168.222.140
Dom Name: corp.local
Forest Name: corp.local
```

This confirmed successful Active Directory domain discovery.

## Domain Authentication

The currently authenticated user was verified using:

```cmd
whoami
```

The result was:

```text
corp\john.smith
```

This confirmed that the Windows 11 client was successfully authenticating the user through the `corp.local` domain.

## IP Configuration

Network configuration was reviewed using:

```cmd
ipconfig /all
```

The Windows 11 client was configured with:

```text
IPv4 Address: 192.168.222.131
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.222.2
DNS Server: 192.168.222.140
```

DC01 was configured with:

```text
IPv4 Address: 192.168.222.140
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.222.2
DNS Server: 127.0.0.1
```

## Active Directory DNS Health

The DNS health of the domain controller was tested using:

```cmd
dcdiag /test:dns
```

The test completed successfully.

The results confirmed that:

```text
DC01 passed test DNS
corp.local passed test DNS
```

This verified that the domain controller's DNS configuration was functioning correctly.

## Active Directory Service Discovery

Active Directory LDAP service discovery was tested using:

```cmd
nslookup -type=SRV _ldap._tcp.dc._msdcs.corp.local
```

The query returned DC01 as the LDAP server for the domain.

This confirmed that the required Active Directory DNS service records were present.

## Group Policy Update

The Windows 11 client was instructed to immediately refresh its Group Policy configuration using:

```cmd
gpupdate /force
```

The command completed successfully and requested the latest policy configuration from the domain controller.

## Group Policy Verification

The effective Group Policy configuration was reviewed using:

```cmd
gpresult /r
```

The results were used to confirm that the:

```text
Corporate Security Policy
```

GPO was applied to the Windows 11 client.

## SMB Share Testing

The Windows 11 client was used to access the shared resources hosted on DC01.

The available shares were accessed using:

```text
\\DC01
```

The following shared resources were visible:

```text
General
IT
HR
```

## NTFS Permission Testing

The HR folder was configured with restricted NTFS permissions.

Access was tested using the domain account:

```text
CORP\john.smith
```

When the account attempted to access the restricted HR resource without the appropriate authorization, Windows returned an access-denied message.

This confirmed that the configured NTFS permissions were actively enforcing access restrictions.

## Delegated Administration Testing

The delegated Helpdesk configuration was validated using a dedicated Helpdesk account.

The account was a member of:

```text
IT Helpdesk
```

The account was delegated permission to reset passwords for users within the Employees OU.

This demonstrated that administrative permissions could be limited to a specific task and Organizational Unit rather than granting unrestricted domain administrative privileges.

## Validation Summary

| Test | Purpose | Result |
|---|---|---|
| `ping` | Network connectivity | Passed |
| `ipconfig /all` | Network configuration | Verified |
| `nslookup` | DNS resolution | Passed |
| `nslookup SRV` | AD service discovery | Passed |
| `nltest /dsgetdc` | Domain controller discovery | Passed |
| `whoami` | Domain authentication | Passed |
| `dcdiag /test:dns` | DNS/AD health | Passed |
| `gpupdate /force` | Group Policy refresh | Passed |
| `gpresult /r` | Group Policy verification | Passed |
| SMB access | Shared resource testing | Passed |
| NTFS access test | Permission enforcement | Passed |
| Helpdesk delegation | Least-privilege validation | Passed |

## Troubleshooting Performed

During initial configuration, the Windows 11 client experienced connectivity and domain discovery issues.

The client temporarily received an APIPA address in the `169.254.x.x` range because it could not reach the VMware DHCP service.

After restoring network connectivity, the client received:

```text
192.168.222.131
```

The client was then able to communicate with DC01 at:

```text
192.168.222.140
```

DNS resolution and domain controller discovery subsequently succeeded.

This troubleshooting process demonstrated practical diagnosis of:

- DHCP connectivity
- IPv4 configuration
- DNS configuration
- Domain controller discovery
- Active Directory connectivity

## Final Validation

The completed environment successfully demonstrated communication between the Windows 11 domain client and the Windows Server domain controller.

The final validation confirmed:

- Network connectivity
- Functional DNS
- Active Directory domain discovery
- Domain authentication
- Active Directory DNS health
- Group Policy deployment
- SMB resource access
- NTFS permission enforcement
- Delegated administration

The validation results provide evidence that the `corp.local` Active Directory environment was functioning as intended.
