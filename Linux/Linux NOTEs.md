# Linux for DevOps – Complete Beginner's Guide (With Commands & Examples)

 **Who is this for?**  
> This guide is for anyone starting their DevOps journey who wants to learn Linux from scratch .

* * *

## Table of Contents

1.  What is Linux?
    
2.  Why Linux for DevOps?
    
3.  Linux vs Windows
    
4.  How to Set Up Linux
    
5.  Architecture of Linux
    
6.  Linux Directory Structure
    
7.  Basic Linux Commands
    
8.  File Viewing & Editing Commands
    
9.  File Permissions
    
10.  User & Group Management
     
11.  Package Management (APT)
     
12.  Process Management
     
13.  Systemctl – Managing Services
     
14.  Disk & Storage Commands
     
15.  Networking Commands
     
16.  SSH – Connecting to Remote Servers
     
17.  Text Processing – grep, sed, awk
     
18.  Compression & File Transfer
     

* * *

## 1\. What is Linux?

Linux was created by **Linus Torvalds** in 1991. It is an **open-source operating system**, which means anyone can use it, modify it, and distribute it for free.

Think of it this way:

*   Windows is like a locked house — you can live in it but can't change the walls.
    
*   Linux is like your own land — you can build, modify, and do whatever you want.
    

**Key points about Linux:**

*   Open source and free to use
    
*   No need for antivirus (unlike Windows)
    
*   Supports multiple users at the same time (multi-user)
    
*   Can do multiple tasks at the same time (multi-tasking)
    
*   Shell-based (you control it through commands)
    
*   Enterprise-level, based on Unix
    

**Popular Linux flavors (distributions):**

| Flavor | Used For |
| --- | --- |
| Ubuntu | Beginners, developers |
| Red Hat (RHEL) | Enterprise companies |
| CentOS / Rocky Linux / AlmaLinux | Free version of Red Hat |
| Amazon Linux | AWS cloud servers |
| Fedora / Arch | Advanced users |

* * *

## 2\. Why Linux for DevOps?

In DevOps, you work with servers every day. Almost **90% of servers in the world run Linux**. Tools like Docker, Kubernetes, Ansible, Jenkins — they all run on Linux.

As a DevOps engineer, you will:

*   SSH into Linux servers
    
*   Deploy applications on Linux
    
*   Write shell scripts
    
*   Monitor logs on Linux systems
    
*   Manage users and permissions
    

* * *

## 3\. Linux vs Windows

| Feature | Windows | Linux |
| --- | --- | --- |
| Type | Client OS | Server OS |
| License | Commercial (paid) | Open Source (free) |
| Users | Single user | Multiple users |
| Examples | Windows 11 | Ubuntu, RHEL, CentOS |
| Antivirus needed? | Yes | No |
| Use case | General purpose | Networking, security, DevOps |
| Shell | PowerShell | Bash |

* * *

## 4\. How to Set Up Linux

There are multiple ways to run Linux on your machine:

**Option 1 — WSL (Windows Subsystem for Linux)**  
Run Linux inside Windows. Best for beginners on Windows.

**Option 2 — Virtual Box**  
Install Linux as a virtual machine. Good for learning locally but slightly slow.

**Option 3 — Vagrant Docker**  
Automates creating virtual machines. Used with Virtual Box.

**Option 4 — Cloud (AWS / Azure / GCP)**  
Launch a Linux server on cloud (EC2 on AWS). This is what you'll actually use in DevOps jobs.

**Option 5 — Dual Boot** *(not recommended for beginners)*  
Install Linux alongside Windows on the same machine.

> **Recommendation for beginners:** Start with WSL or a free AWS EC2 instance with Ubuntu.

* * *

## 5\. Architecture of Linux

Linux is made of three layers. Think of it like an onion:

![](https://cdn.hashnode.com/uploads/covers/6a16afe718745e9b1d7d91ba/496da424-7629-4a5b-bcd0-bcc5eaf28f4d.png align="center")

**Kernel:**

*   The kernel is a program written in C
    
*   It talks directly with the hardware (RAM, CPU, hard disk)
    
*   You can't talk to kernel directly
    

**Shell:**

*   You write commands in the shell (like Bash)
    
*   Shell translates your commands and sends them to the kernel
    
*   Kernel runs the command and does the task
    

**Application:**

*   Programs you use like vim, notepad, browser, etc.
    
*   Applications talk to the shell, shell talks to the kernel
    

**Flow:** Application → Shell → Kernel → Hardware

**Bootloader (GRUB):**

*   GRUB is the program on Linux that loads and manages the boot process
    
*   It's what runs first when you turn on your computer
    

* * *

## 6\. Linux Directory Structure

In Linux, everything is a file — even folders. The top-most folder is called **root (**`/`**)**.

```plaintext
/  (root — top of everything)
├── bin       — Basic commands (ls, cp, mv...) And Contain binary executables
├── sbin      — System-level binary files (used by root user)
├── etc       — Configuration files
├── home      — User home directories (/home/akash)
├── root      — Home folder of the root user only
├── var       — Variable files (logs, cache, backups)
├── tmp       — Temporary files (anyone can access and make changes)
├── opt       — Third-party software installations
├── mnt       — Mount point for external storage
├── dev       — Device files (represents hardware)
├── media     — Removable media (USB, CD)
├── boot      — Boot files (needed to start the OS)
├── usr       — User binaries, all Linux commands live here
│   └── man   — Manual pages (use 'man' command to read docs)
└── lost+found — Recovered files after crash
```

**Remember these key directories:**

| Directory | Purpose |
| --- | --- |
| `/etc` | All configuration files |
| `/var` | Logs, cache, backups — things that change over time |
| `/tmp` | Temporary files — anyone can access and modify |
| `/home` | Where user personal files are stored |
| `/root` | Only root (admin) user can access |
| `/opt` | Install third-party apps here |
| `/bin` | Contains all Linux commands |
| `/mnt` | Mount external drives temporarily here |

* * *

## 7\. Basic Linux Commands

### Navigation

| Command | What it does | Example |
| --- | --- | --- |
| `pwd` | Shows your current location (Present Working Directory) | `pwd` |
| `ls` | List files and folders | `ls` |
| `ls -l` | Detailed list with permissions | `ls -l` |
| `ls -a` | Show hidden files too | `ls -a` |
| `cd` | Change directory | `cd /home/akash` |
| `cd ..` | Go one level up | `cd ..` |
| `cd ~` | Go to your home directory | `cd ~` |

### File and Folder Operations

| Command | What it does | Example |
| --- | --- | --- |
| `mkdir` | Create a new folder | `mkdir devops` |
| `touch` | Create a new empty file | `touch demo.txt` |
| `cp` | Copy a file | `cp demo.txt devops/` |
| `mv` | Move or rename a file | `mv demo.txt devops/` |
| `rm` | Remove/delete a file | `rm demo.txt` |
| `rmdir` | Remove an empty folder | `rmdir devops` |
| `rm -r` | Remove folder and all its contents (recursive) | `rm -r devops` |
| `rm -f` | Force remove (no confirmation) — use carefully! | `rm -f demo.txt` |
| `rm -rv` | Remove and print each item being deleted | `rm -rv devops` |

> **Warning:** `rm -f` removes without asking. Always double check before using it.

### Viewing File Contents

| Command | What it does | Example |
| --- | --- | --- |
| `cat` | Read/display file content | `cat demo.txt` |
| `head` | Show first 10 lines | `head demo.txt` |
| `tail` | Show last 10 lines | `tail demo.txt` |
| `tail -f` | Live tail — keep watching file updates | `tail -f /var/log/syslog` |
| `less` | View file page by page | `less demo.txt` |
| `more` | Similar to less | `more demo.txt` |
| `wc` | Word count in a file | `wc demo.txt` |
| `diff` | Compare two files | `diff file1.txt file2.txt` |
| `sort` | Sort file contents | `sort demo.txt` |
| `clear` | Clear the terminal screen | `clear` |

### Links

| Command | What it does | Example |
| --- | --- | --- |
| `ln -s` | Create a soft link (shortcut) — if original deleted, link also breaks | `ln -s /filepath linkname` |
| `ln` | Create a hard link — even if original deleted, link still works | `ln /filepath linkname` |

* * *

## 8\. File Viewing & Editing Commands

### vim — Text Editor

Vim is a powerful text editor in the terminal. It has two modes:

*   **Command mode** (default) — for navigation
    
*   **Insert mode** — for typing text
    

**How to use vim:**

```bash
vim demo.txt        # Open or create a file
```

Once inside vim:

*   Press `i` → Enter insert mode (now you can type)
    
*   Press `Esc` → Go back to command mode
    
*   Type `:wq` → Save and exit
    
*   Type `:q!` → Exit without saving
    

### cat — Read a file

```bash
cat demo.txt
```

### zcat — Read compressed file

```bash
zcat file.gz
```

* * *

## 9\. File Permissions

### Understanding Permissions

Every file and folder in Linux has permissions for 3 types of users:

*   **Owner (user)** — the person who created the file
    
*   **Group** — a group of users
    
*   **Others** — everyone else
    

Permissions are shown like this when you run `ls -l`:

```plaintext
drwxr-xr--
```

Let's break it down:

```plaintext
d  rwx  r-x  r--
  |   |    |    |
  |   |    |    └── Others: read only (r--)
  |   |    └─────── Group: read and execute (r-x)
  |   └──────────── Owner: read, write, and execute (rwx)
  └──────────────── d = Directory, - = Regular File, l = Link
```

**Permission meanings:**

*   `r` = Read (value: 4)
    
*   `w` = Write (value: 2)
    
*   `x` = Execute (value: 1)
    
*   `-` = No permission (value: 0)
    

**Numeric permission chart:**

| Number | Permission | Meaning |
| --- | --- | --- |
| 0 | \--- | No permission |
| 1 | \--x | Execute only |
| 2 | \-w- | Write only |
| 3 | \-wx | Write + Execute |
| 4 | r-- | Read only |
| 5 | r-x | Read + Execute |
| 6 | rw- | Read + Write |
| 7 | rwx | Read + Write + Execute |

### chmod — Change Permissions

```bash
chmod 777 filename       # Give all permissions to everyone
chmod 755 filename       # Owner: all, Group & Others: read+execute
chmod 600 filename       # Owner: read+write, others: nothing
```

### chown — Change File Owner

```bash
chown akash filename             # Change owner to akash
sudo chown akash filename        # With sudo if needed
chown akash:devops filename      # Change owner and group
```

### chgrp — Change Group

```bash
sudo chgrp devops filename       # Change group ownership
```

## 10\. User & Group Management

### Check Current User

```bash
whoami                  # Shows your username
who                     # Shows all logged-in users
id                      # Shows user ID, group IDs
echo $SHELL             # Check which shell you're using (bash/sh)
```

### Create a New User

```bash
sudo useradd -m akash          # Create user 'akash' with home directory
sudo passwd akash              # Set password for akash
```

### Switch User

```bash
su akash                # Switch to user akash
```

### Delete a User

```bash
sudo userdel akash             # Delete user akash
```

### Create User with Bash Shell

```bash
sudo useradd -m om -s /bin/bash     # Create user with bash shell
sudo passwd om                       # Set password
```

### Sudo Access

`sudo` is a group that has **all permissions** in the system. When you add a user to the sudo group, they can run admin commands.

```bash
sudo usermod -aG sudo akash          # Add akash to sudo group
```

You can also manually edit the sudoers file:

```plaintext
/etc/sudoers                         # File that controls sudo access
```

### Check All Users

```bash
cat /etc/passwd                      # See all users in the system
```

### Group Management

```bash
sudo groupadd devops                 # Create a new group
sudo groupdel devops                 # Delete a group

# Add users to group — Method 1: gpasswd
sudo gpasswd -M om,Prajod devops     # Add multiple users to group

# Add users to group — Method 2: usermod
sudo usermod -aG devops Prajod       # Add Prajod to devops group
                                      # -aG means append to group

# Check groups
cat /etc/group                        # See all groups
```

### df -h — Check Disk Usage

```bash
df -h                               # See storage usage in human-readable format
```

* * *

## 11\. Package Management (APT)

APT is the package manager for Ubuntu/Debian-based Linux systems.

```bash
sudo apt update             # Download the latest list of available packages
sudo apt upgrade            # Upgrade all installed packages to latest version
sudo apt install nginx      # Install a package (e.g., nginx)
sudo apt remove nginx       # Uninstall a package
```

**Other package managers for different Linux distributions:**

| Tool | Distribution |
| --- | --- |
| apt | Ubuntu, Debian |
| yum | CentOS (older) |
| dnf | Fedora, newer CentOS |
| pacman | Arch Linux |
| rpm | Red Hat |

* * *

## 12\. Process Management

A process is any program that is currently running.

```bash
ps                          # Show your current running processes
ps aux                      # Show ALL processes on the system
top                         # Live view of all processes (like Task Manager)
kill -9 <process_id>        # Force kill a process
free -h                     # Check RAM usage
nohup <command>             # Run command that keeps running even after logout
vmstat                      # Show memory and storage stats
```

**System information commands:**

```bash
uname -a                    # Show OS and platform info
uptime                      # How long the system has been running
date                        # Current date and time
reboot                      # Restart the system
shutdown                    # Shut down the system
```

* * *

## 13\. Systemctl – Managing Services

`systemctl` is a tool to **control and manage services** (like nginx, apache) running on Linux.

```bash
systemctl status nginx        # Check if nginx is running
sudo systemctl stop nginx     # Stop nginx
sudo systemctl start nginx    # Start nginx
sudo systemctl restart nginx  # Restart nginx (stop + start)
sudo systemctl reload nginx   # Reload config without stopping
```

**Full command breakdown:**

```plaintext
sudo  systemctl  stop    nginx
 |        |        |       |
 |        |        |       └── Service name
 |        |        └────────── Action (start/stop/restart/status)
 |        └─────────────────── Tool to control services
 └──────────────────────────── Run as super user
```

**Real-world example — Host a webpage on nginx:**

```bash
cd /var/www/html              # Go to nginx web folder
# Create index.html file here
# Then map port 80 to your IP address
```

* * *

## 14\. Disk & Storage Commands

```bash
lsblk                         # List all block devices (disks and partitions)
df -h                         # Show all mount points and disk usage
du -sh /var/log               # Show size of a specific folder
```

* * *

## 15\. Networking Commands

| Command | Purpose | Example |
| --- | --- | --- |
| `ping` | Check if a server is reachable | `ping google.com` |
| `nslookup` | Find IP address of a domain | `nslookup google.com` |
| `dig` | Detailed DNS info about a domain | `dig google.com` |
| `traceroute` | Show path packets take to reach a server | `traceroute youtube.com` |
| `ifconfig` | Check your IP address and network interfaces | `ifconfig` |
| `ip` | Modern replacement for ifconfig | `ip a` |
| `netstat` | Network statistics | `netstat` |
| `ss` | Same as netstat (faster) | `ss -tuln` |
| `wget` | Download files from internet | `wget https://example.com/file.zip` |
| `curl` | Upload or download data (supports GET, POST, PUT) | `curl -X GET https://api.example.com` |
| `hostname` | Show machine hostname | `hostname` |
| `whois` | See domain owner and registration info | `whois google.com` |
| `arp` | Find MAC address of a device | `arp -a` |
| `mtr` | Trace route continuously | `mtr google.com` |
| `watch` | Continuously watch a command | `watch -n 1 mtr google.com` |
| `route` | Show/edit routing table | `route` |
| `iwconfig` | Check wireless network info | `iwconfig` |
| `nmap` | Scan ports and details of websites | `nmap google.com` |
| `iptable` | Firewall rules | `sudo iptables -L` |
| `telnet` | Like nslookup but with port | `telnet www.google.com 80` |

**curl vs wget:**

*   `wget` → just download files
    
*   `curl` → download AND upload, supports APIs (GET, POST, PUT, DELETE)
    

* * *

## 16\. SSH – Connecting to Remote Servers

SSH stands for **Secure Shell**. It is a protocol (rule) that lets you connect from one machine to another in a **secure and encrypted way**. SSH uses **port 22**.

### How SSH Works

SSH uses a **key pair** system:

*   **Public Key** → You put this on the server (like a lock)
    
*   **Private Key** → You keep this on your local machine (like a key)
    

When you connect, the server checks if your private key matches the public key. If yes — you're in.

![](https://cdn.hashnode.com/uploads/covers/6a16afe718745e9b1d7d91ba/40771a02-76e2-4a1b-81ee-6e567e9f6b31.png align="center")

### SSH from Local to EC2

```bash
# Step 1: Generate SSH key pair on your local machine
ssh-keygen

# This creates two files:
# id_rsa        → private key (keep this safe, never share)
# id_rsa.pub    → public key (put this on the server)

# Step 2: Connect to remote server
ssh -i "keyname.pem" ubuntu@<public-ip-or-dns>

# Step 3: Exit the server
exit
```

### Connect EC2 to Another EC2 (Bastion Host)

Sometimes you need to connect servers to each other (for example, a demo server needs to reach a testing server). You use a **Bastion Host** as a middle server.

```plaintext
Local → Bastion Host (EC2-A) → EC2-B
```

### View Hidden Folders

```bash
ls -a                         # Show hidden files (starts with .)
cd .ssh                       # Go to SSH folder
cat authorized_keys           # See public keys that are allowed to connect
```

* * *

## 17\. Text Processing – grep, sed, awk

### grep – Search for text in files

```bash
grep "hello" filename             # Find "hello" in file
grep -i "hello" filename          # Case-insensitive search
grep -i "hello" filename | head   # Show first few results
grep -i -c "info" applog          # Count occurrences (case-insensitive)
```

### awk – Extract specific columns/data from files

awk is a powerful tool to extract and process data from files. Think of it like a mini programming language.

```bash
# Print a specific column
awk '{print $3}' filename           # Print column 3

# Print specific text from a file
awk '/Auth failure/ {print}' filename    # Print lines containing "Auth failure"

# Print column 2 from matching lines
awk '/Auth failure/ {print $2}' filename
```

**awk example — reading a log file:**

```plaintext
STD    None      mobilze
357    Prajod    96431109
308    Om        98348711
```

```bash
awk '{print $2}' applog         # Output: None, Prajod, Om
```

### sed – Edit file content (find and replace)

`sed` is a stream editor — it edits files without opening them.

```bash
# Replace text globally in a file
sed 's/user/username/g' auth_failure_file

# Replace text in place (modify the actual file)
sed -i 's/user/username/g' auth_failure_file
```

### head / tail

```bash
head filename                   # Show first 10 lines
tail filename                   # Show last 10 lines
tail -f /var/log/syslog         # Follow live logs (great for debugging)
```

### find – Find files and directories

```bash
find /home -name "demo.txt"     # Find file by name
find /var/log -type f           # Find all files in a directory
```

* * *

## 18\. Compression & File Transfer

### zip / unzip

```bash
zip -r archive.zip foldername       # Zip a folder
zip archive.zip file.txt            # Zip a single file
unzip archive.zip                   # Unzip a file
```

### SCP – Secure Copy

SCP is used to copy files between two Linux machines securely over SSH.

```bash
scp <file> ubuntu@<ip>:/destination     # Copy file to remote server
```

### rsync – Remote Sync

rsync syncs files between two machines. It only copies what has changed (efficient).

```bash
rsync -avz localfile ubuntu@ip:/remote/path
```

* * *
