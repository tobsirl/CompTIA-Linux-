# CompTIA Linux+ (XK0-005)

### Basic Linux Tasks

## User and Group Management

### Create, Modify, and Delete Users

#### Commands

```bash
sudo useradd -D # Display default useradd settings

less /etc/login.defs # Display default useradd settings

ls -a /etc/skel # Display default useradd settings

sudo useradd -c "John Doe" jdoe # Create user with comment

sudo useradd -e 2021-12-31 cmason # Create user with expiration date

chage -l cmason # Display user expiration date

chage -E 2021-12-31 cmason # Set user expiration date

chage -M 90 cmason # Set user password expiration

sudo useradd -l -u 1001 -g 1001 -c "John Doe" jdoe # Create user with UID and GID

sudo passwd -l jdoe # Lock user account

sudo passwd -u jdoe # Unlock user account

sudo cat /etc/shadow # Display user account status

sudo usermod -c "John Doe" jdoe # Change user comment

sudo userdel -r jdoe # Delete user and home directory

sudo userdel -r -f jdoe # Delete user and home directory without confirmation

# Group Management
groupadd # Create group
groupmod # Modify group
groupdel # Delete group

sudo groupadd group1 # Create group
sudo groupmod -n group2 group1 # Rename group

# Add user to group
sudo usermod -a -G group1 jdoe

# Remove user from group
sudo gpasswd -d jdoe group1

# Delete group
sudo groupdel group1

# Query Users and Groups
whoami # Display current user
who # Display users currently logged in
id # Display current user's UID and GID
last # Display last logged in users

id jdoe # Display user's UID and GID

who -a # Display all users currently logged in

last -a # Display all users last logged in

# Account Profiles
.bashrc # User's bash profile
.bash_profile # All of the users bash profiles

/etc/profile # System wide bash profile

/etc/profile.d # Directory containing system wide bash profiles

/etc/skel # Directory containing default user files

/etc/bashrc # System wide bash profile

```

## Permissions and Ownership

### Permissions

Access rights assigned to users that enable them to access or modify files and directories.

```bash
# File Permissions
# r = read
# w = write
# x = execute
# - = no permission
# 7 columns
# 1st column = file type
# 2nd-4th column = owner permissions
# 5th-7th column = group permissions
# 8th-10th column = other permissions
-rw-r--r-- 1 tobsirl tobsirl 2.1K Dec 25 11:17 README.md

```

#### Commands

_chmod_

- Syntax: chmod [options] mode[,mode] file1 [file2 ...]
- Options:
  - -c, --changes: Like verbose but report only when a change is made
  - -f, --silent, --quiet: Suppress most error messages
  - -v, --verbose: Output a diagnostic for every file processed
  - -R, --recursive: Change files and directories recursively
  - -h, --no-dereference: Do not dereference symbolic links
  - --preserve-root: Fail to operate recursively on '/'
  - --reference=RFILE: Use RFILE's mode instead of MODE values
  - --version: Output version information and exit
  - --help: Display this help and exit

**Symbolic Mode:**
Enables to set permissions using three components:

Permission Context: u, g, o, a
Permission Operator: +, -, =
Permission Type: r, w, x

**Absolute Mode:**
Enables to set permissions using a three-digit octal number.

4 = read
2 = write
1 = execute

777 = rwxrwxrwx
752 = rwxr-x-w-
722 = rwx-w--w-

_umask_

Used to set default permissions for newly created files and directories.

```bash
chmod # Change file permissions
```

_chown_

Used to change the owner and/or group of a file or directory.

```bash
chown # Change file owner and group

# Syntax:
chown [options] [owner][:[group]] file1 [file2 ...]
chown {username}: {group name} {file/directory}
```

_chgrp_

Used to change the group ownership of a file or directory.

```bash
chgrp # Change file group

# Syntax:
chgrp [options] group file1 [file2 ...]
```

### Special Permissions and Attributes

The less privileged users are able to perform certain tasks that require elevated privileges.

#### Set User ID (SUID)

User is allowed to have similar permissions as the owner of the file.

```bash
# Set SUID
chmod u+s {file/directory}
chmod 4775 {file/directory}

# Remove SUID
chmod u-s {file/directory}
chmod 0775 {file/directory}
```

#### Set Group ID (SGID)

Group is allowed to have similar permissions as the group of the file.

```bash
# Set SGID
chmod g+s {file/directory}
chmod 2775 {file/directory}

# Remove SGID
chmod g-s {file/directory}
chmod 0775 {file/directory}
```

#### Sticky Bit

Prevents users from deleting or renaming files that they do not own.

```bash
# Set Sticky Bit
chmod o+t {file/directory}
chmod 1775 {file/directory}

# Remove Sticky Bit
chmod o-t {file/directory}
chmod 0775 {file/directory}
```

#### Immutable Flag

Attribute of a file or directory that prevents it from being modified, renamed, or deleted.

Immutable flag is useful for files that are highly sensitive and important.

```bash
# Set Immutable Flag
lsattr {file/directory}
lsattr -a {file/directory}
chattr +i {file/directory}
chattr -i {file/directory}
```

### Access Control Lists (ACLs)

ACLs are used to grant permissions to users and groups that are not the owner of the file or directory.

```bash
getfacl {file/directory} # Display ACLs
setfacl {file/directory} # Set ACLs

# Syntax:
setfacl [options] [{-b|-k} {directory|file}] [{-m|-x} acl_entries] file ...
```

### Troubleshooting Permissions

1. Identify the problem
1. Establish a theory of probable cause
1. Test the theory to determine the cause
1. Establish an action plan
1. Implement the solution
1. Verify full system functionality
1. Document findings, actions, and outcomes

## Storage Management

### Types of Storage Devices

1. Hard Disk Drives (HDDs)
2. Solid State Drives (SSDs)
3. USB Flash Drives
4. External storage devices

_Block Devices_

- Read/write in blocks of data (eg. hard drives, SSDs, USB flash drives)

_Character Devices_

- Read/write in streams of data (eg. keyboards, mice, printers)
