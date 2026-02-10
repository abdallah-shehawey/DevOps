# RHEL 9 Administration Guide

A comprehensive summary of Red Hat Enterprise Linux 9 administration topics, including architecture, command-line basics, file systems, user management, services, and process monitoring.

## 1. Introduction to Linux

### Why Learn Linux?

- **Community support**
    
- **High Security & Stability**
    
- **Ease of Maintenance**
    
- **Open Source & Free**
    
- **Runs on any hardware**
    
- **Customization & Flexibility**
    

### Linux Distributions

There are multiple distributions (distros), each with different release policies and support models:

- **RHEL (Red Hat Enterprise Linux):** Industry standard for enterprise.
    
- **CentOS Stream**
    
- **Fedora**
    
- **Ubuntu**
    
- **Debian**
    

### Linux Architecture

The Linux operating system consists of layers:

1. **Hardware:** Physical devices.
    
2. **Kernel:** The core that interacts directly with hardware (drivers, memory, processes).
    
3. **Shell:** The interface (like Bash) that takes user commands and passes them to the kernel.
    
4. **Applications:** User-level programs and libraries.
    

### The Shell (Bash)

- **Normal User (`$`):** Standard privileges (e.g., `username@hostname:~$`).
    
- **Root User (`#`):** Administrative (superuser) privileges (e.g., `root@hostname:~#`).
    
- **Case Sensitivity:** Linux commands and filenames are case-sensitive.
    
- **Syntax:** `command option(s) argument(s)`
    
    - _Right:_ `ls -l /dev`
        
    - _Wrong:_ `ls - l /dev` (spaces matter)
        

## 2. Basic Operations & Shortcuts

### GUI vs CLI

- **GUI (Graphical User Interface):** User-friendly, point-and-click.
    
- **CLI (Command Line Interface):** Powerful, scriptable, resource-efficient, and friendly for remote access.
    

### Remote Access (SSH)

Remote administration is usually performed over **SSH** (Secure Shell) for encrypted connections.

- **Syntax:** `ssh user@host`
    

### Basic Commands

|Command|Description|
|---|---|
|`date`|Display system date and time|
|`cal`|Display a calendar|
|`passwd`|Change user password|
|`file`|Determine file type|
|`cat`|View file contents|
|`less` / `more`|View file contents page by page|
|`head` / `tail`|View beginning/end of files|
|`history`|View command history|
|`ls`|List directory contents|
|`id`|Print user and group IDs|
|`clear`|Clear terminal screen|
|`exit`|Exit the shell|

### Reading Manual Pages

- **`man command`**: Shows the full manual page.
    
- **`command --help`**: Often provides a quick usage summary.
    

### Terminal Shortcuts

- **Ctrl+A:** Jump to the beginning of the line.
    
- **Ctrl+E:** Jump to the end of the line.
    
- **Ctrl+U:** Clear from cursor to beginning.
    
- **Ctrl+K:** Clear from cursor to end.
    
- **Ctrl+Left/Right Arrow:** Jump between words.
    
- **Ctrl+R:** Search history (reverse-i-search).
    
- **Tab:** Auto-completion.
    

### Vim Editor

Vim has three main modes:

1. **Command (Normal) Mode:** Navigate and issue commands.
    
2. **Insert Mode:** Edit text.
    
3. **Visual Mode:** Select text.
    

**Common Commands:**

- `vim file.txt`: Open file.
    
- `i`: Switch to Insert mode.
    
- `:wq`: Save and quit.
    
- `:q!`: Quit without saving.
    

## 3. File System Hierarchy & Management

### Directory Structure

Linux uses a single directory tree starting at `/`.

- `/bin` & `/usr/bin`: Essential user binaries.
    
- `/sbin` & `/usr/sbin`: System binaries.
    
- `/boot`: Boot loader files.
    
- `/dev`: Device files.
    
- `/etc`: System configuration files.
    
- `/home`: User home directories.
    
- `/root`: Root user's home directory.
    
- `/run`: Runtime data (processes started since boot).
    
- `/tmp`: Temporary files (deleted automatically after 10 days).
    
- `/var`: Variable data (logs, websites, databases).
    
- `/proc`: Kernel and process information (virtual filesystem).
    
- `/sys`: Kernel sysfs (device and driver info).
    

### Types of Files

- Regular files
    
- Directories
    
- Device files
    
- Symbolic links
    
- Sockets
    
- FIFOs (pipes)
    

### File Management Commands

|Command|Usage|
|---|---|
|`touch`|Create empty files or update timestamps|
|`mkdir`|Create directories|
|`cp`|Copy files or directories|
|`mv`|Move or rename files|
|`rm`|Remove files|
|`rmdir`|Remove empty directories|

### Paths

- **Absolute Path:** Starts from root `/` (e.g., `/home/user/Documents`).
    
- **Relative Path:** Starts from current location (e.g., `./file.txt`, `../dir/`).
    

### Links

- **Hard Link (`ln source target`):** Exact replica, shares Inode, valid only within the same filesystem.
    
- **Soft Link (`ln -s target linkname`):** Pointer/shortcut to original file, different Inode, can cross filesystems.
    

## 4. Searching & Redirection

### Pattern Matching (Globbing)

- `*`: Matches zero or more characters (e.g., `*.txt`).
    
- `?`: Matches exactly one character (e.g., `file?.log`).
    
- `[abc]`: Matches any one character in the set.
    
- `[!abc]`: Matches any character NOT in the set.
    

### Grep Command

Used to search text/patterns within files.

- `grep 'pattern' filename`: Basic search.
    
- `grep -i`: Case insensitive.
    
- `grep -v`: Invert match (show lines NOT matching).
    
- `grep -r`: Recursive search.
    
- `grep -n`: Show line numbers.
    
- `grep -A3` / `-B3`: Show 3 lines after/before match.
    

### I/O Redirection & Pipelines

- `>`: Redirect standard output to a file (overwrite).
    
- `>>`: Redirect standard output to a file (append).
    
- `2>`: Redirect standard error.
    
- `&>` or `2>&1`: Redirect both output and error.
    
- `|` (Pipe): Pass output of one command as input to the next (e.g., `ps aux | grep sshd`).
    

## 5. User & Group Management

### User Accounts

- **UID (User ID):** Unique identifier.
    
    - **Root:** UID 0.
        
    - **System Users:** Low UIDs (reserved).
        
    - **Regular Users:** Higher UIDs (defined in `/etc/login.defs`).
        
- **Configuration Files:**
    
    - `/etc/passwd`: User account info (username, UID, GID, home, shell).
        
    - `/etc/group`: Group definitions.
        

### Privilege Escalation

- **`su`:** Switch user. `su - username` switches to user with login shell. `su -` switches to root.
    
- **`sudo`:** Execute a command as another user (usually root) using your _own_ password.
    
    - Configured in `/etc/sudoers` (edit using `visudo`).
        

### User Creation

- `useradd [options] username`: Creates user and home directory.
    
- `passwd username`: Set the password.
    
- `usermod`: Modify existing user properties.
    

### Nologin Shell

Service accounts often use `/sbin/nologin` or `/usr/sbin/nologin` as their shell to prevent interactive login access for security.

## 6. Permissions

Permissions govern access to files and directories (Read `r`, Write `w`, Execute `x`).

### Methods

1. **Symbolic:** `u` (user), `g` (group), `o` (others).
    
    - Example: `chmod u+x script.sh` (Add execute for owner).
        
    - Example: `chmod g-w file.txt` (Remove write for group).
        
2. **Numeric:**
    
    - Read = 4, Write = 2, Execute = 1.
        
    - Example: `chmod 755 dir` (rwx for owner, rx for others).
        
    - Example: `chmod 644 file` (rw for owner, r for others).
        

### Ownership

- `chown owner:group filename`: Change user and group ownership.
    
- `chown -R`: Recursive change.
    

## 7. Process Management & Logging

### Process Monitoring

- **Process ID (PID):** Unique ID for every running process.
    
- `ps`: Snapshot of current processes.
    
    - `ps aux` or `ps -ef`: View all processes.
        
- `top` / `htop`: Real-time system monitoring.
    
- `pstree`: View processes as a tree structure.
    
- `pgrep`: Find process IDs by name.
    

### Job Control

- `jobs`: List background jobs.
    
- `fg`: Bring job to foreground.
    

### Killing Processes

- `kill [PID]`: Send TERM signal.
    
- `kill -9 [PID]`: Force kill (KILL signal).
    
- `pkill [name]`: Kill by process name.
    
- `killall [name]`: Kill all processes with specific name.
    

### System Logging

Logs are primarily in `/var/log` (e.g., `/var/log/messages`).

- **Priorities:** emerg, alert, crit, err, warning, notice, info, debug.
    
- **Viewing:**
    
    - `tail -f /var/log/messages`: Follow log in real-time.
        
    - `less +F`: Also allows following.
        

### Journalctl

Query the systemd journal:

- `journalctl -u nginx.service`: Logs for a specific unit.
    
- `journalctl -f`: Follow live logs.
    
- `journalctl --since "2025-06-01"`: Filter by time.
    

## 8. Service Management & Time Configuration

### Service Management (Systemctl)

Manage systemd services (start, stop, restart, enable).

- `systemctl status nginx`: Check status.
    
- `systemctl start nginx`: Start service.
    
- `systemctl stop nginx`: Stop service.
    
- `systemctl enable --now nginx`: Enable service at boot and start it immediately.
    
- **States:** active, inactive, failed.
    

### Time Configuration

Manage system time and timezone.

- `timedatectl status`: Check current settings.
    
- `timedatectl set-timezone Region/City`: Set timezone (e.g., `Africa/Cairo`).
    

## 9. Software Management

RHEL family uses `yum` (or `dnf`) and `rpm` for package management.

### Yum/DNF (High-level)

- `yum search package`: Search repositories.
    
- `yum install package`: Download and install.
    
- `yum update`: Update packages.
    

### RPM (Low-level)

- `rpm -ivh package.rpm`: Install a local RPM file with verbose output and hash progress.
    

## 10. References

- **Red Hat Documentation:** [docs.redhat.com](https://docs.redhat.com "null")
    
- **The Linux Documentation Project:** [tldp.org](http://tldp.org "null")
    
- **Local Help:** `/usr/share/doc`, `man` pages.