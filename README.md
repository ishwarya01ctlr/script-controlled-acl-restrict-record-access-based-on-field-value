# Script-Controlled ACL – Restrict Record Access Based on Field Value

## Project Overview

This project demonstrates how to implement a Script-Controlled Access Control List (ACL) in ServiceNow to restrict users from viewing records based on specific conditions.

In this project, users belonging to the EEE branch are allowed to view EEE records, while administrators have full access.

## Objective

The objective of this project is to:

- Implement Script-Controlled ACLs in ServiceNow.
- Restrict record access based on field values.
- Control Read, Create, Write, and Delete operations.
- Use custom roles to control user permissions.
- Prevent unauthorized access to records.

## Technologies Used

- ServiceNow
- Access Control Lists (ACL)
- JavaScript
- User Administration
- Custom Roles
- Custom Tables

## User and Role Creation

A test user named **EEE User** was created.

The following custom roles were created:

- bb1
- bb2
- bb3
- bb4

These roles were assigned to the required user.

## Custom Table

A custom table named **Institution Details** was created.

**Table Name:**

`u_institution_details`

### Fields

- Student Roll Number – Auto Number
- Student Name – Reference (User)
- Faculty Name – Reference (User)
- Branch – Choice
- Email – String
- Phone Number – String
- Description – Multi String

### Branch Choices

- ECE
- EEE
- CSE

## Read ACL

A Read ACL was created for the `u_institution_details` table.

**Operation:** Read

**Required Role:** bb1

**Data Condition:** Branch is EEE

The ACL script allows administrators full access and controls access for users based on the required role.

```javascript
(function () {
    // Allow admin users full access
    if (gs.hasRole('admin')) {
        return true;
    }

    // Allow only EEE branch users to see EEE records
    if (gs.hasRole('bb1')){
        return true;
    }

    // Deny access for all others
    return false;
})();
