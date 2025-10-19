# Operating Systems Lab Report

**Student Name:** Madias Bek  
**Instructor:** Dana Tolegen  
**Subject:** Operating Systems - Linux Essentials  
**Date:** October 19, 2025  
**Time:** 10:20 PM  
**System Used:** Kali Linux  

---

## Lab 15: System and User Security

### Objective
To monitor system login attempts and understand user and group permissions in Linux.

### Tasks Completed

#### 15.2 Running Commands as an Administrator

**Step 1-2: Using the `su` Command**
- Switched to the root user account using `su -` command
- Verified user identity with `id` command
- Returned to original user (ayanami) using `exit` command
- Confirmed identity change using `id` command again

**Step 3-4: Using the `sudo` Command**
- Attempted to view `/etc/shadow` file as regular user (permission denied)
- Successfully viewed `/etc/shadow` using `sudo head /etc/shadow`
- Learned that sudo requires current user's password, not root password

#### 15.3 User Accounts

**Step 1-2: Examining User Account Files**
- Viewed first ten lines of `/etc/passwd` using `head /etc/passwd`
- Used `grep ayanami /etc/passwd` to view specific account record
- Learned the difference between user accounts and system accounts

#### 15.4 Passwords

**Step 1-3: Understanding the Shadow File**
- Attempted to view `/etc/shadow` without permissions
- Checked file permissions using `ls -l /etc/shadow`
- Used `sudo head -3 /etc/shadow` to view encrypted password information

**Step 4-6: Retrieving Account Information**
- Used `getent passwd ayanami` to retrieve account information
- Reviewed man page with `man 5 passwd` to understand field descriptions
- Used `id` and `id root` commands to view user and group information

#### 15.5 Who is On the System

**Step 1-2: Monitoring Active Users**
- Used `who` command to see current logged-in users
- Used `w` command for detailed view of active sessions
- Learned about system uptime and load averages

#### 15.6 Viewing Login History

**Step 1: Login History**
- Used `last` command to view complete login history from `/var/log/wtmp`

### Key Learnings from Lab 15

1. **Administrative Access:** Understood two methods for administrative tasks - `su` (switch user) and `sudo` (superuser do)
2. **Account Types:** Differentiated between regular user accounts and system accounts
3. **File Permissions:** Learned that `/etc/shadow` contains sensitive password data with restricted permissions
4. **Password File Structure:** Understood the seven colon-delimited fields in `/etc/passwd` (name:password:UID:GID:Comment:directory:shell)
5. **Group Membership:** Learned about primary and secondary group memberships
6. **System Monitoring:** Gained knowledge of commands to monitor who is logged in and system login history

---

## Lab 16: Creating Users and Groups

### Objective
To create and manage user accounts and groups in Linux.

### Tasks Completed

#### 16.2 Creating Groups

**Step 1: Switching to Root**
- Switched to root user with `su -` command

**Step 2-4: Group Creation**
- Created two groups using `groupadd -r research` and `groupadd -r sales`
- Used `getent group research` to verify research group creation
- Used `grep sales /etc/group` to verify sales group creation

**Step 5: Group Modification**
- Renamed sales group to clerks using `groupmod -n clerks sales`
- Changed GID to 10003 using `groupmod -g 10003 clerks`
- Verified changes with `grep clerks /etc/group`

**Step 6: Group Deletion**
- Deleted clerks group using `groupdel clerks`
- Verified deletion with `grep clerks /etc/group`

#### 16.3 User Configuration

**Step 1-2: Default User Settings**
- Viewed default useradd values with `useradd -D`
- Modified INACTIVE parameter using `useradd -D -f 30`
- Verified changes with `useradd -D`

**Step 3-5: Editing Configuration File**
- Used `nano /etc/default/useradd` to modify CREATE_MAIL_SPOOL setting
- Changed CREATE_MAIL_SPOOL from "no" to "yes"
- Saved changes and confirmed with `useradd -D`

**Step 6: Creating New User**
- Created student user with `useradd -G research -c 'Linux Student' -m student`
- Verified user creation with `grep student /etc/passwd`
- Checked group memberships with `grep student /etc/group`

**Step 7-8: Adding Secondary Group Membership**
- Added research group as secondary group for ayanami user using `usermod -aG research ayanami`
- Verified group membership with `getent group research`
- Viewed student group with `getent group student`
- Examined passwd and shadow entries for student user

**Step 9: Setting User Password**
- Set password for student user using `passwd student`
- Verified encrypted password in shadow file with `getent shadow student`

**Step 10: Checking Login History**
- Used `last` command to view general login history
- Used `last student` to check if student user had logged in

**Step 11: Deleting User Account**
- Removed student user and home directory using `userdel -r student`
- Verified deletion with `grep student /etc/group`

### Key Learnings from Lab 16

1. **Group Management:** Learned to create, modify, rename, and delete groups using `groupadd`, `groupmod`, and `groupdel` commands
2. **User Creation:** Understood how to create users with specific options including secondary groups, comments, and home directories
3. **Default Settings:** Learned how to view and modify default user creation settings
4. **Configuration Files:** Gained experience editing system configuration files with text editors
5. **Password Management:** Understood how to set and reset user passwords using `passwd` command
6. **User Modification:** Learned to add secondary group memberships using `usermod` command
7. **Account Deletion:** Understood the difference between deleting just the account versus removing home directory and mail
8. **File Verification:** Practiced using `getent`, `grep`, and other commands to verify changes in `/etc/passwd`, `/etc/shadow`, and `/etc/group`
9. **Security Implications:** Learned about orphaned files when deleting groups and the importance of proper user/group management

---

## Conclusion

Both labs were successfully completed in Kali Linux. All commands executed properly, and I gained comprehensive knowledge of Linux system administration fundamentals, particularly in user account management, security, and permissions. The hands-on experience with administrative commands reinforced theoretical understanding of Linux system security and user management principles.
