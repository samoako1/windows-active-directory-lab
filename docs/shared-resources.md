\# Shared Resources



\## Overview



Department-specific shared resources were configured on DC01 to demonstrate Windows SMB file sharing, NTFS permissions, and group-based access control.



The shared resources were designed to simulate a basic enterprise file server environment where users receive access based on their organizational role.



\## Shared Folder Structure



The shared resources were organized on DC01 using department-specific folders:



```text

DC01

├── General

├── IT

└── HR

```



The folders were shared over the Windows Server SMB protocol and made accessible to domain users from WIN11-01.



\## SMB File Sharing



Users accessed the shared resources from the Windows 11 domain client using the UNC path:



```text

\\\\DC01

```



This allowed the client to discover the available network shares hosted by the domain controller.



The shares included:



```text

General

IT

HR

```



\## NTFS Permissions



NTFS permissions were configured on the department-specific folders to control access to the files and directories.



Permissions were assigned using Active Directory security groups where appropriate.



The general permission model was:



```text

Domain User

&#x20;    │

&#x20;    ▼

Active Directory Security Group

&#x20;    │

&#x20;    ▼

Shared Folder

&#x20;    │

&#x20;    ▼

NTFS Permissions

```



Using security groups allows permissions to be managed centrally rather than assigning permissions individually to every user.



\## HR Folder Access



The HR folder was configured as a restricted department resource.



A domain user without the appropriate authorization attempted to access the HR folder from WIN11-01.



The user received an access-denied message.



This demonstrated that the configured NTFS permissions were successfully enforcing the intended access restrictions.



\## Access Testing



Shared resource access was tested from the Windows 11 domain client.



Testing included:



1\. Connecting to the domain controller using `\\\\DC01`.

2\. Viewing available shared folders.

3\. Attempting to access department-specific resources.

4\. Verifying authorized access.

5\. Verifying unauthorized access.



\## Unauthorized Access Validation



The HR folder was specifically tested using a user who did not have the required permissions.



The attempted access resulted in a permission-denied message.



This provides practical evidence that access control was functioning as configured.



\## Authorized Access



Authorized users can be granted access to department-specific folders through membership in the appropriate security group.



This approach allows access to be managed according to organizational responsibilities.



For example:



```text

HR User

&#x20;  │

&#x20;  ▼

HR Security Group

&#x20;  │

&#x20;  ▼

HR Share

```



The same model can be extended to other departmental resources.



\## NTFS and Share Permissions



Windows file-sharing environments can use both share-level and NTFS permissions.



The effective access level is determined by the combination of these permissions.



The lab focused primarily on NTFS permissions to demonstrate granular access control over departmental resources.



\## Security Considerations



The shared-resource configuration follows several basic security principles:



\- Use security groups instead of individual permissions where possible.

\- Restrict access based on organizational responsibilities.

\- Apply least-privilege access.

\- Test both authorized and unauthorized access.

\- Separate department-specific resources.



This approach provides a scalable foundation for enterprise file-sharing administration.



\## Validation



The shared resources were validated from WIN11-01 using Windows File Explorer and UNC paths.



The primary access path was:



```text

\\\\DC01

```



Access to restricted resources was then tested using domain accounts.



The HR access-denied result confirmed that the configured permissions were actively enforcing access restrictions.



\## Key Concepts Demonstrated



\- Windows SMB

\- Network shares

\- UNC paths

\- NTFS permissions

\- Active Directory security groups

\- Group-based access control

\- Departmental file sharing

\- Authorized resource access

\- Unauthorized access prevention

\- Least-privilege access

\- Windows file server administration

