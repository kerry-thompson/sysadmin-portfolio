# Linux Lab 1: User and Group Management

**Date:** December 14, 2024  
**System:** Ubuntu 24 home lab

## Objective
Master Linux user and group administration including creating users, managing groups, setting passwords, and implementing role-based access control.

## Commands Practiced
- `useradd` - Create new users
- `usermod` - Modify user accounts
- `groupadd` - Create new groups
- `passwd` - Set user passwords
- `groups` - View group memberships
- `id` - Display user and group IDs

## Scenarios Completed

### 1. User Creation
Created multiple user accounts with proper home directories and group assignments:
- Created developer users (bob, alice)
- Set up administrative users
- Configured user passwords

### 2. Group Management
Implemented role-based access control using groups:
- Created `developers` group for development team
- Created `qa_team` group for quality assurance
- Created `managers` group for management access

### 3. User-Group Assignments
Assigned users to appropriate groups based on roles:
- Added developers to `developers` group
- Configured multi-group memberships
- Verified group assignments with `groups` and `id` commands

## Key Learnings

**User Management:**
- Users need home directories (`-m` flag)
- Primary vs. secondary groups
- Password policies and user security

**Group Management:**
- Groups enable role-based access control
- Users can belong to multiple groups
- Group membership affects file access permissions

**Real-World Applications:**
- Managing team access to shared resources
- Implementing least-privilege security
- Organizing users by department or function

## Commands Reference
```bash
# Create user with home directory
sudo useradd -m username

# Add user to group
sudo usermod -aG groupname username

# Create new group
sudo groupadd groupname

# Set user password
sudo passwd username

# View user's groups
groups username

# View detailed user info
id username
```

## Next Steps
- Continue to Lab 2: File Permissions
- Practice managing larger user bases
- Explore password policies and account expiration
