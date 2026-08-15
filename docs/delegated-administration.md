# Delegated Administration

## Overview

Delegated administration was configured in the `corp.local` Active Directory environment to demonstrate role-based administrative access and the principle of least privilege.

An `IT Helpdesk` security group was created and delegated limited administrative permissions within the `Employees` Organizational Unit.

The goal was to allow Helpdesk personnel to perform common account-management tasks without granting unrestricted Domain Administrator privileges.

## IT Helpdesk Group

A security group named:

```text
IT Helpdesk
```

was created in Active Directory.

The group represents a hypothetical enterprise helpdesk team responsible for basic user account support.

Helpdesk users can be added to this group to inherit the delegated permissions assigned to the group.

## Delegated Permission

The `IT Helpdesk` group was delegated the ability to reset passwords for users within the:

```text
Employees
```

Organizational Unit.

The delegation was configured using the Delegation of Control Wizard in Active Directory Users and Computers.

The delegated task was intentionally limited to password reset operations.

## Delegation Scope

The delegation was applied specifically to the Employees OU rather than the entire domain.

The resulting structure is:

```text
corp.local
└── Employees
    │
    └── IT Helpdesk
         │
         └── Reset User Passwords
```

This limits the scope of the Helpdesk group's administrative permissions.

## Least-Privilege Model

The delegation demonstrates the principle of least privilege.

Instead of granting the Helpdesk account membership in a highly privileged group such as Domain Admins, the account receives only the permissions required to perform its intended support function.

The administrative model is:

```text
Helpdesk User
      │
      ▼
IT Helpdesk Group
      │
      ▼
Delegated Permission
      │
      ▼
Employees OU
      │
      ▼
Password Reset
```

This reduces the potential impact of compromised or misused administrative credentials.

## Helpdesk Account

A dedicated Helpdesk user account was configured to validate the delegated permissions.

The account was intended to represent a normal IT support employee rather than a domain administrator.

The Helpdesk account was associated with the:

```text
IT Helpdesk
```

security group.

## Permission Validation

The delegated permissions were tested using the Helpdesk account.

The test was designed to confirm that the account could perform the delegated password-reset operation for users within the Employees OU.

The validation process consisted of:

1. Signing in using the Helpdesk account.
2. Opening Active Directory Users and Computers.
3. Navigating to the Employees OU.
4. Selecting a test user.
5. Attempting to reset the user's password.
6. Confirming that the delegated operation was permitted.

## Security Boundary

The delegation was intentionally scoped to the Employees OU.

This prevents the Helpdesk role from automatically receiving equivalent administrative privileges over the entire domain.

The configuration demonstrates how Active Directory can separate administrative responsibilities between different teams.

## Administrative Separation

A typical enterprise environment may separate administrative responsibilities such as:

```text
Domain Administrators
       │
       ├── Domain-wide administration
       │
       └── Infrastructure management

IT Helpdesk
       │
       ├── Password resets
       ├── Basic account support
       └── Limited user administration
```

The lab demonstrates this separation by providing the Helpdesk group with a specific delegated task instead of unrestricted administrative access.

## Active Directory Tools

Delegated administration was configured using:

- Active Directory Users and Computers
- Delegation of Control Wizard
- Active Directory security groups

These tools allow administrators to assign granular permissions to specific users or groups at the Organizational Unit level.

## Security Benefits

Delegated administration provides several security and operational benefits:

- Supports least-privilege access
- Reduces unnecessary administrative privileges
- Separates administrative responsibilities
- Simplifies helpdesk operations
- Limits the scope of compromised accounts
- Provides a scalable administrative model

## Validation

The delegated administration configuration was validated using a dedicated Helpdesk account.

The test confirmed that the Helpdesk account could perform the intended password-reset operation within the Employees OU without requiring unrestricted Domain Administrator privileges.

## Key Concepts Demonstrated

- Active Directory delegation
- Delegation of Control Wizard
- Security groups
- Organizational Unit permissions
- Password reset delegation
- Role-based administration
- Least-privilege access
- Helpdesk administration
- Administrative separation
- Active Directory security
