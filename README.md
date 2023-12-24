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
```
