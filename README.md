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

_File systems that Linux supports_

- ext2
- ext3
- ext4
- XFS
- Btrfs
- FAT

_File Allocation Table (FAT)_

An older file system compatible with different operating systems.

_ext2_

Used to be the native Linux file system of some older Linux distributions.

_ext3_

Much faster in recovering data and better ensures data integrity in abrupt system shutdowns.

_ext4_

Supports volumes up to one exabyte and files up to 16 terabytes.

_XFS_

A 64-bit, high-performance journaling file system that provides fast recovery and can handle large files efficiently.

_Btrfs_

Supports volumes of up to 1 exabyte in size and up to 18 quintillion files on each volume.

### Device Mapper

Creates virtual device and passes data from that virtual device to one or more physical devices.

### Raid

Redundant Array of Independent Disks (RAID) is a method of combining multiple physical disk drives into a single logical unit.

_Striping_

Combines multiple physical disks into a single logical unit.

_Mirroring_

Combines multiple physical disks into a single logical unit and duplicates the data on each disk.

_Parity_

Used in RAID drive arrays for fault tolerance by calculating the data across multiple disks and storing the results on a separate disk.

#### RAID Levels

_RAID 0_

- Striping
- No redundancy
- No fault tolerance
- High performance
- No data protection

_RAID 1_

- Mirroring
- Redundancy
- Fault tolerance
- High performance
- Data protection

_RAID 5_

- Striping with parity
- Redundancy
- Fault tolerance
- High performance
- Data protection
- Requires at least 3 disks
- Can withstand the loss of one disk
- Parity is distributed across all disks

_RAID 6_

- Striping with double parity
- Redundancy
- Fault tolerance (can withstand the loss of two disks)
- High performance
- Data protection
- Requires at least 4 disks
- Parity is distributed across all disks
- More expensive than RAID 5

_RAID 10_

- Striping with mirroring
- Redundancy
- Fault tolerance
- High performance
- Data protection
- Requires at least 4 disks
- Can withstand the loss of one disk in each mirrored pair

_/proc/mdstat_

Contains a snapshot of the kernel's RAID status.

#### Logical Volume Manager (LVM)

Maps whole physical devices and partions into one or more virtual containers called volume groups.

- Dynamically create, delete, and resize volumes
- Map logical volumes across physical devices
- Create virtual snapshots of each logical volume

_Mount Point_

An access point that is typically an empty directory where a file system is loaded or mounted to make it accessible to users.

#### Commands

_mount_
Loads a file system to a specified directory to make it accessible to users and applications.

```bash
mount # Mount file system
mount [options] {device_name} {mount_point}
```

_umount_

Unmounts a file system from a specified directory.

```bash
umount # Unmount file system
umount [options] {device_name} {mount_point}
```

_fstab_

A list of file systems to be mounted, their mount points, and any options that might be needed for specific file systems.

_systemd.mount_

Used to create an new mount unit to mount a file system.

_/etc/mtab_

Reports the status of currently mounted file systems.

_lsblk_

Displays information about block storage devices currently available on the system

_blkid_

Prints each block device in a flat format and includes some additional information.

_fsck_

Used to check the correctness and validity of a file system.

_resize2fs_

Used to resize ext2, ext3, and ext4 file systems.

_tune2fs_

Used to adjust tunable file system parameters on ext2, ext3, and ext4 file systems.
tune2fs can also add a journal to an existing ext2 or ext3 file system.

Superblock

Contains metadata about the file system, such as the file system type, size, status, and information about other metadata structures.

_dumpe2fs_

Used to display the superblock and blocks group information for the file system.

Isscsi

Used to list information about SCSI devices connected to the system.

_fcstat_

Used to display statistics for Fibre Channel devices.

### Linux Directory Structure

Contains all of the files and directories that are required for the system to function.

Types of files and directories:

- Text files
- Executable files
- Input and output files
- Directories
- Links
- Domain sockets
- Named pipes
- Special files

_Directories_
Contain files and other directories.

_Special Files_
System files stored in the /dev directory.

_Links_

Make a file accessible in multiple part of the system's file tree

_Domain Sockets_
Provide inter-process networking that is protected by the file system's access control lists.

_Named Pipes_
Enable processes to communicate with each other without using a network sockets

### File System Hierarchy Standard (FHS)

Specifies a set of guidelines and standards that define the directory structure and directory contents in Linux distributions.

_/_

The root directory of the entire file system hierarchy.

_/bin_

Contains executable programs that are required by all users.

_/boot_

Contains files required to boot the system.

_/dev_

Contains special files that represent devices attached to the system.

_/etc_

Contains system configuration files.

_/home_

Stores users' home directories and files.

_/lib_

Stores shared program libraries required by the kernel, command-line utilities, and binaries

_/media_

Contains mount points for removable media devices.

_/mnt_

Contains mount points for temporary file systems.

_/opt_

Contains optional software packages.

_/proc_

Contains information about system resources and processes.

_/root_

The home directory of the root user.

_/sbin_

Stores binaries used for completing the booting process which are also used by the root user

_/sys_

Contains information about devices, drivers, and some kernel features.

_/tmp_

Contains temporary files that are created by applications and users.

_/usr_

A read-only directory that stores small programs and files accessible by all users.

_/var_

Contains files that are expected to change in size and content as the system is running.

### Current Working Directory (CWD)

The location on the system being accessed at any point in time

### Troubleshooting Storage Issues

Ensure storage devices are recognized by the system and available to the user

- Missing devices
- Missing volumes
- Missing mount points
- Degraded storage
- Performance issues
- Resource exhaustion
- Storage integrity issues

_ulimit_

Used to set limits on system resources.

```bash
ulimit # Display resource limits
ulimit -a # Display all resource limits
ulimit -aH # Display all resource limits in human readable format
ulimit -aS # Display all resource limits in machine readable format
ulimit -c # Display core file size
ulimit -c unlimited # Set core file size to unlimited
```

_df/du_

Facilitate the monitoring of disk space usage.

```bash
df # Display disk space usage
df -h # Display disk space usage in human readable format
df -a # Display all file systems
df -T # Display file system type
df -i # Display inode usage
df -x tmpfs # Exclude file system type
df -x devtmpfs # Exclude file system type
df -x squashfs # Exclude file system type
df -x tmpfs -x devtmpfs -x squashfs # Exclude multiple file system types
du # Display disk usage
du -h # Display disk usage in human readable format
du -a # Display all files
du -s # Display total disk usage
du -c # Display total disk usage
du -h -a -s -c # Display total disk usage in human readable format
du -h -a -s -c -x tmpfs -x devtmpfs -x squashfs # Exclude multiple file system types
```

#### I/O Scheduling

The process where the OS determines the order of input and output operations as they pertain to block storage devices.

_iostat_

Used to monitor I/O statistics.

```bash
iostat # Display I/O statistics
iostat -x # Display extended I/O statistics
iostat -x 1 # Display extended I/O statistics every 1 second
iostat -x 1 5 # Display extended I/O statistics every 1 second for 5 iterations
```

- Transfers per second (tps)
- Number of blocks read per second (kB_read/s)
- Number of blocks written per second (kB_wrtn/s)
- Total number of blocks read (kB_read)
- Total number of blocks written (kB_wrtn)

_ioping_

Used to monitor I/O latency.
Troubleshoots I/O performance issues.

```bash
ioping # Display I/O latency
ioping -c 10 # Display I/O latency for 10 iterations
```

#### Storage Quota

Storage space alloted to a user for a file storage on a computer.

## Files and Directories

### Searching for Files

_locate_

Used to search for files by name.

```bash
locate # Search for files by name
locate -i # Search for files by name (case insensitive)
locate -c # Display number of matching entries
locate -l 5 # Display 5 matching entries
locate -S # Display statistics
locate -d {database} # Search a specific database
locate -e {file} # Search for an exact match
locate -r {regex} # Search using a regular expression
locate -b {file} # Search for a file name only
locate -q {file} # Suppress error messages
locate -n {number} {file} # Display number of matching entries
locate -o {file} # Display only files that exist
locate -r {regex} | grep {regex} # Search using a regular expression
```

_updatedb_

Used to update the locate database.

```bash
updatedb # Update the locate database
```

_find_

Used to search for files by name, size, type, and other criteria.

```bash
find # Search for files by name, size, type, and other criteria
find {directory} # Search for files by name, size, type, and other criteria
find {directory} -name {file} # Search for files by name
find {directory} -iname {file} # Search for files by name (case insensitive)
find {directory} -iname {file} -type f # Search for files by name (case insensitive) and type
find {directory} -iname {file} -type d # Search for directories by name (case insensitive) and type
find {directory} -iname {file} -type l # Search for links by name (case insensitive) and type
find {directory} -iname {file} -type b # Search for block devices by name (case insensitive) and type
find {directory} -iname {file} -type c # Search for character devices by name (case insensitive) and type
find {directory} -iname {file} -type s # Search for sockets by name (case insensitive) and type
find {directory} -iname {file} -type p # Search for named pipes by name (case insensitive) and type
find {directory} -iname {file} -type f -size +1M # Search for files by name (case insensitive), type, and size
find {directory} -iname {file} -type f -size -1M # Search for files by name (case insensitive), type, and size
find {directory} -iname {file} -type f -size 1M # Search for files by name (case insensitive), type, and size
find {directory} -iname {file} -type f -size +1M -size -10M # Search for files by name (case insensitive), type, and size
find {directory} -iname {file} -type f -size +1M -size -10M -exec ls -lh {} \; # Search for files by name (case insensitive), type, and size and execute command
```

_which_

Used to locate the binary file of a command.

```bash
which # Locate the binary file of a command
which {command} # Locate the binary file of a command
```

_whereis_

Used to locate the binary file, source code, and manual page of a command.

```bash
whereis # Locate the binary file, source code, and manual page of a command
whereis {command} # Locate the binary file, source code, and manual page of a command
```

_cat/concatenates_

Can display, combine, and create files.

```bash
cat # Display, combine, and create files
cat {file} # Display file
cat {file1} {file2} # Combine files
cat {file1} {file2} > {file3} # Combine files and create new file
cat {file1} {file2} >> {file3} # Combine files and append to existing file
```

_head_

Used to display the first 10 lines of a file.

```bash
head # Display the first 10 lines of a file
head {file} # Display the first 10 lines of a file
head -n 5 {file} # Display the first 5 lines of a file
```

_tail_

Used to display the last 10 lines of a file.

```bash
tail # Display the last 10 lines of a file
tail {file} # Display the last 10 lines of a file
tail -n 5 {file} # Display the last 5 lines of a file
tail -f {file} # Display the last 10 lines of a file and continue to monitor the file for changes
```

_less_

Used to display the contents of a file one page at a time.

```bash
less # Display the contents of a file one page at a time
less {file} # Display the contents of a file one page at a time
```

_more_

Used to display the contents of a file one page at a time.

```bash
more # Display the contents of a file one page at a time
more {file} # Display the contents of a file one page at a time
```

_copy/cp_

Used to copy files and directories.

```bash
cp # Copy files and directories
cp {file} {directory} # Copy file to directory
cp {file1} {file2} # Copy file1 to file2
cp -r {directory1} {directory2} # Copy directory1 to directory2
```

_mv_

Used to move files and directories.

```bash
mv # Move files and directories
mv {file} {directory} # Move file to directory
mv {file1} {file2} # Move file1 to file2
mv {directory1} {directory2} # Move directory1 to directory2
```

_touch_

Tests the permissions or creates files that will be processed by some applications.

```bash
touch # Tests the permissions or creates files that will be processed by some applications
touch {file} # Create file
touch -a {file} # Change access time
touch -m {file} # Change modification time
touch -c {file} # Do not create file
touch -r {file1} {file2} # Use file1 as reference for file2
touch -t {yyyymmddhhmm.ss} {file} # Use timestamp to create file
```

_rm_

Used to remove files and directories.

```bash
rm # Remove files and directories
rm {file} # Remove file
rm -r {directory} # Remove directory
rm -f {file} # Force remove file
rm -rf {directory} # Force remove directory
```

_unlink_

Used to remove files and directories.

```bash
unlink # Remove files and directories
unlink {file} # Remove file
unlink -r {directory} # Remove directory
unlink -f {file} # Force remove file
unlink -rf {directory} # Force remove directory
```
