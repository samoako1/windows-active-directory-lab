# Group Policy

## Overview

Group Policy was implemented to demonstrate centralized security configuration across the `corp.local` Active Directory environment.

A Group Policy Object named `Corporate Security Policy` was created and linked to the Employees Organizational Unit.

The policy provides a centralized method for applying Windows security settings to domain users and computers.

## GPO Configuration

The Group Policy Object was created in Group Policy Management on DC01.

The GPO was named:

```text
Corporate Security Policy
```

The policy was linked to:

```text
corp.local
└── Employees
```

Linking the GPO to the Employees OU allows the policy to apply to the users and computers within that organizational scope.

## Password Policy

The Corporate Security Policy included password security requirements.

The configured password controls included:

- Minimum password length
- Password complexity requirements
- Password history
- Minimum password age
- Maximum password age

These settings establish a consistent password security baseline for domain accounts.

## Account Lockout Policy

Account lockout controls were also configured to help protect against repeated failed authentication attempts.

The policy included:

- Account lockout threshold
- Account lockout duration
- Account lockout counter reset interval

These settings demonstrate a basic defense against password-guessing and repeated authentication attempts.

## Group Policy Deployment

After configuring the GPO, the Windows 11 client was instructed to refresh its Group Policy configuration.

The following command was used:

```cmd
gpupdate /force
```

The command forces the client to immediately request updated Group Policy settings from the domain controller.

## Group Policy Verification

The effective Group Policy configuration on WIN11-01 was verified using:

```cmd
gpresult /r
```

The resulting report was used to confirm that the `Corporate Security Policy` GPO was successfully applied to the client.

## Policy Application

The Group Policy workflow used in the lab was:

```text
GPO Created
    │
    ▼
GPO Linked to Employees OU
    │
    ▼
Windows 11 Client Requests Policy
    │
    ▼
gpupdate /force
    │
    ▼
Policy Applied
    │
    ▼
gpresult /r
    │
    ▼
Policy Verified
```

This demonstrates the complete process of creating, deploying, and validating a centralized Windows security policy.

## Centralized Security Management

Group Policy allows administrators to configure security settings centrally rather than manually configuring every workstation.

This provides several benefits:

- Consistent security settings
- Reduced manual configuration
- Centralized policy management
- Easier administration
- Improved security standardization
- Policy enforcement across domain systems

## Organizational Unit Scope

The Employees OU was used as the scope for the Corporate Security Policy.

Organizational Units allow policies to be targeted to specific organizational groups rather than applying every policy universally across the domain.

This provides greater administrative flexibility.

## Policy Validation

The Group Policy configuration was validated using:

```cmd
gpupdate /force
```

followed by:

```cmd
gpresult /r
```

The successful appearance of the `Corporate Security Policy` in the applied policy results confirmed that the policy was being processed by the Windows 11 client.

## Administrative Tools

Group Policy was configured and managed using:

- Group Policy Management
- Active Directory Users and Computers
- Windows command-line utilities

The primary Group Policy management interface was Group Policy Management on DC01.

## Security Considerations

The Group Policy configuration demonstrates centralized enforcement of basic account security controls.

Password requirements help establish stronger authentication standards, while account lockout controls provide an additional defense against repeated failed login attempts.

Using Group Policy also reduces configuration drift because security settings can be centrally managed.

## Key Concepts Demonstrated

- Group Policy Objects
- Group Policy Management
- GPO linking
- Organizational Unit policy scope
- Password security
- Account lockout
- Centralized Windows security configuration
- Policy deployment
- `gpupdate`
- `gpresult`
- Active Directory administration
- Windows security management
