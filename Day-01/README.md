# Day 01 – Linux Fundamentals

## 1. Learning Environment

| Configuration | Details |
|---|---|
| Linux Distribution | AlmaLinux 8.10 (Cerulean Leopard) |
| Virtualization | VMware Workstation |
| Architecture | x86_64 |
| Kernel Version | 4.18.0-553.111.1.el8_10.x86_64 |
| Firmware | BIOS |
| User Account | anjukrishnan |

## 2. Linux System Information Commands

### 2.1 Identify Linux Distribution

**Command:**

```bash
cat /etc/os-release
```

**Purpose:** Displays Linux distribution name, version, ID and other OS identification information.

### 2.2 Check Hostname

```bash
hostname
```

**Purpose:** Displays the current system hostname.

### 2.3 Display Detailed System Information

```bash
hostnamectl
```

**Purpose:** Displays hostname, operating system, kernel version, virtualization type and system architecture.

### 2.4 Check Date and Time

```bash
date
```

**Purpose:** Displays the current system date, time and timezone.

### 2.5 Check Kernel Information

```bash
uname
```

**Purpose:** Displays the operating system kernel name.

```bash
uname -r
```

**Purpose:** Displays the currently running kernel release.

```bash
uname -a
```

**Purpose:** Displays complete kernel and system information, including hostname, kernel release and architecture.

## 3. Linux User Management – Basic Commands

### 3.1 Identify Current User

```bash
whoami
```

**Purpose:** Displays the username of the currently logged-in user.

### 3.2 Check User ID and Group Information

```bash
id
```

**Purpose:** Displays UID, primary GID, supplementary groups and SELinux security context.

### 3.3 Check Logged-in User Sessions

```bash
who
```

**Purpose:** Displays currently logged-in user sessions, terminals and login times.

## 4. Linux Filesystem Navigation

### 4.1 Print Current Working Directory

```bash
pwd
```

**Purpose:** Displays the absolute path of the current working directory.

### 4.2 Change Directory

```bash
cd Documents
```

**Purpose:** Changes the current directory to Documents.

```bash
cd ..
```

**Purpose:** Moves one level up to the parent directory.

```bash
cd /
```

**Purpose:** Moves to the root directory.

```bash
cd ~
```

**Purpose:** Moves to the current user's home directory.

```bash
cd -
```

**Purpose:** Switches to the previous working directory.

```bash
cd .
```

**Purpose:** Refers to the current directory without changing its location.

## 5. File and Directory Listing

### 5.1 List Files

```bash
ls
```

**Purpose:** Lists files and directories in the current directory.

### 5.2 Detailed File Listing

```bash
ls -l
```

**Purpose:** Displays detailed file information, including permissions, ownership, size and modification time.

### 5.3 Display Hidden Files

```bash
ls -a
```

**Purpose:** Lists all files, including hidden files that begin with a dot (.).

### 5.4 Detailed Listing Including Hidden Files

```bash
ls -la
```

**Purpose:** Displays detailed information about all files, including hidden files.

**Important observations:**

- `-` indicates a regular file.
- `d` indicates a directory.
- `r` represents read permission.
- `w` represents write permission.
- `x` represents execute permission.
- Owner and group information identify file ownership.

## 6. Practical Lab – Linux User Password Recovery

**Scenario:** The password of an existing AlmaLinux 8.10 user account was forgotten.

**Objective:** Recover access to the existing user account without reinstalling the operating system.

**Recovery Method:** GRUB boot entry editing using the `rd.break` kernel parameter.

### Step 1 – Restart the Virtual Machine

Restarted the AlmaLinux virtual machine in VMware Workstation.

Accessed the GRUB boot menu during startup.

### Step 2 – Edit the GRUB Boot Entry

- Selected the first AlmaLinux boot entry.
- Pressed the `e` key to edit the selected boot entry.
- Located the kernel line beginning with `linux`.
- Moved the cursor to the end of the kernel boot line.

### Step 3 – Add Recovery Parameter

Added the following parameter at the end of the kernel line:

```text
rd.break
```

**Purpose:** Interrupts the normal boot process and provides access to the initramfs recovery environment.

Pressed:

```text
Ctrl + X
```

**Purpose:** Boots the system using the modified GRUB entry.

### Step 4 – Remount the Installed Filesystem

At the recovery prompt:

```bash
switch_root:/#
```

Executed:

```bash
mount -o remount,rw /sysroot
```

**Purpose:**

- `mount` – Manages mounted filesystems.
- `-o` – Specifies mount options.
- `remount` – Remounts an already mounted filesystem.
- `rw` – Enables read-write access.
- `/sysroot` – Mount point of the installed Linux system.

### Step 5 – Enter the Installed Linux System

```bash
chroot /sysroot
```

**Purpose:** Changes the apparent root directory to `/sysroot`, allowing commands to operate inside the installed AlmaLinux system.

### Step 6 – Reset the User Password

```bash
passwd Anjukrishnan
```

**Purpose:** Changes the password of the specified Linux user account.

Entered the new password and confirmed it.

**Expected success message:**

```text
passwd: all authentication tokens updated successfully.
```

### Step 7 – Request SELinux Relabeling

```bash
touch /.autorelabel
```

**Purpose:** Creates a marker file that instructs the system to perform SELinux filesystem relabeling during the next boot.

### Step 8 – Exit the Recovery Environment

First command:

```bash
exit
```

**Purpose:** Exits the chroot environment and returns to the recovery shell.

Second command:

```bash
exit
```

**Purpose:** Exits the recovery shell and allows the normal boot process to continue.

### Step 9 – Verify Successful Login

Waited for the SELinux relabeling and normal boot process to complete.

Logged in using the existing username and newly configured password.

**Result: Password recovery completed successfully. AlmaLinux 8.10 login verified.**

## 7. Server Information Verification – Troubleshooting Exercise

Collected the following information using Linux commands.

| Requirement | Command | Verified Result |
|---|---|---|
| OS Version | `cat /etc/os-release` | AlmaLinux 8.10 |
| Hostname | `hostname` | localhost.localdomain |
| Logged-in User | `whoami` | anjukrishnan |
| Kernel Version | `uname -r` | 4.18.0-553.111.1.el8_10.x86_64 |
| Working Directory | `pwd` | /home/anjukrishnan |

## 8. Day-End Assessment

| Assessment | Result |
|---|---|
| Linux Fundamentals Quiz | 5/5 |
| Basic Command Practice | Completed |
| Filesystem Navigation | Completed |
| Server Information Verification | Successful |
| GRUB Password Recovery | Successful |

## 9. Key Learning Outcomes

- Understood Linux system architecture basics.
- Identified AlmaLinux distribution and kernel information.
- Practiced basic user and group identification.
- Explored Linux filesystem navigation.
- Listed regular and hidden files.
- Inspected basic file permissions and ownership.
- Performed GRUB-based password recovery using `rd.break`.
- Used `mount`, `chroot`, `passwd` and SELinux relabeling commands.
- Verified successful login after password recovery.

**Day 01 Status: Completed**

**Environment:** AlmaLinux 8.10 on VMware Workstation.

**Documentation note:** This record describes practical exercises actually performed and verified in the lab. Passwords and sensitive credentials are intentionally excluded.
