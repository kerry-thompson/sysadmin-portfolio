# Linux Lab 2: File Permissions and Access Control

**Date:** December 14, 2024  
**System:** Ubuntu 24 home lab

## Objective
Master Linux file permissions including numeric and symbolic notation, special permissions (sticky bit, SGID), and implementing secure team collaboration scenarios.

## Commands Practiced
- `chmod` - Change file permissions (numeric and symbolic)
- `chown` - Change file ownership
- `ls -l` / `ls -ld` - View permissions
- Special permissions: sticky bit (1777), SGID (g+s)

## Scenarios Completed

### 1. Basic Permissions (rwx)
Practiced setting permissions using both methods:
- **Numeric:** 755, 644, 700, 770
- **Symbolic:** u+x, g-w, o=r

**Permission breakdown:**
- r (4) = read
- w (2) = write
- x (1) = execute

### 2. Team Collaboration Directory
Set up `/projects/webapp/` with proper team access:
- Owner: project lead
- Group: developers
- Permissions: 770 (owner and group access only)
- Others: no access

### 3. Sticky Bit Implementation
Configured `/projects/webapp/logs/` with sticky bit (1777):
- **Purpose:** Prevent users from deleting others' files
- **Test:** Created files as different users
- **Result:** Users can only delete their own files
- **Real-world use:** Shared temp/log directories like /tmp

### 4. SGID for Group Inheritance
Applied SGID to `/projects/webapp/src/`:
- **Permissions:** drwxrws--- (note the 's' in group)
- **Effect:** New files inherit directory's group
- **Benefit:** Automatic team access without manual chown

**Comparison:**
- **Without SGID:** Files owned by user's primary group (bob:bob)
- **With SGID:** Files owned by directory's group (bob:developers)

## Permission Quick Reference

### Numeric Permissions
```
7 = rwx (4+2+1)
6 = rw- (4+2)
5 = r-x (4+1)
4 = r-- (4)
0 = --- (none)
```

**Common patterns:**
- 755 = rwxr-xr-x (scripts, directories)
- 644 = rw-r--r-- (regular files)
- 700 = rwx------ (private files)
- 770 = rwxrwx--- (team directories)

### Special Permissions
- **Sticky bit (1xxx):** Users can only delete their own files
- **SGID (2xxx):** New files inherit directory's group
- **SUID (4xxx):** Execute with file owner's permissions

## Real-World Applications

### 1. Shared Project Directories
```bash
# Create team directory with SGID
sudo mkdir /projects/team-app
sudo chown :developers /projects/team-app
sudo chmod 2770 /projects/team-app
```

### 2. Secure Log Directories
```bash
# Create logs with sticky bit
sudo mkdir /var/log/app-logs
sudo chmod 1777 /var/log/app-logs
```

### 3. Manager-Only Releases
```bash
# Production releases directory
sudo chown :managers /releases
sudo chmod 755 /releases
```

## Key Takeaways

1. **Use SGID on shared team directories** - Eliminates manual group assignment
2. **Sticky bit for collaborative spaces** - Prevents accidental deletions
3. **770 for team-only access** - No public access to sensitive projects
4. **644 for readable files** - Standard for documentation
5. **Test with actual users** - Verify permissions work as intended

## Testing Methodology

Created test users (brady, kerry, bob, alice, outsider) to verify:
- ✅ Group members can access team directories
- ✅ Non-members cannot access restricted directories
- ✅ Sticky bit prevents cross-user deletions
- ✅ SGID properly inherits group ownership

## Commands Reference
```bash
# Change permissions (numeric)
chmod 755 file.sh

# Change permissions (symbolic)
chmod u+x file.sh
chmod g-w file.txt
chmod o=r file.txt

# Change ownership
chown user:group file.txt
chown :group file.txt  # group only

# Set sticky bit
chmod +t directory
chmod 1777 directory

# Set SGID
chmod g+s directory
chmod 2770 directory

# View permissions
ls -l file.txt
ls -ld directory/
```

## Next Steps
- Continue learning system administration fundamentals
- Practice permission troubleshooting scenarios
- Apply these skills in real projects and Azure environments
