# Linux Cheat Sheet – DevOps Quick Reference

---

## Navigation
```bash
pwd                    # Where am I? (Present Working Directory)
ls                     # List files
ls -l                  # Detailed list
ls -a                  # Show hidden files
ls -la                 # Detailed + hidden
cd /path               # Go to a directory
cd ..                  # Go up one level
cd ~                   # Go to home directory
```

---

## File & Folder Operations
```bash
mkdir foldername       # Create folder
touch filename         # Create empty file
cp source dest         # Copy file
mv source dest         # Move / rename file
rm filename            # Delete file
rm -r foldername       # Delete folder and contents
rm -rf foldername      # Force delete (no prompt) — be careful!
```

---

## View File Contents
```bash
cat file               # View full file
head file              # First 10 lines
tail file              # Last 10 lines
tail -f file           # Live follow (great for logs)
less file              # Scroll through file
wc file                # Word count
diff file1 file2       # Compare two files
sort file              # Sort content
```

---

## Editing Files
```bash
vim file               # Open vim editor
  i                    # Enter insert mode
  Esc                  # Back to command mode
  :wq                  # Save and exit
  :q!                  # Exit without saving
```

---

## File Permissions
```bash
ls -l                  # See permissions
chmod 777 file         # Give all permissions to everyone
chmod 755 file         # Owner: all | Group+Others: read+execute
chmod 600 file         # Owner: read+write | Others: none
chown user file        # Change owner
chown user:group file  # Change owner and group
chgrp group file       # Change group only
getfacl file           # Check ACL permissions
setfacl -m u:user:rwx file   # Set ACL for user
setfacl -m g:group:rwx file  # Set ACL for group
setfacl -b file        # Remove all ACL
```

**Permission Numbers:**
```
4 = read (r)
2 = write (w)
1 = execute (x)
0 = no permission (-)

7 = rwx | 6 = rw- | 5 = r-x | 4 = r-- | 0 = ---
```

---

## User Management
```bash
whoami                         # Current user
who                            # All logged-in users
id                             # User ID and group info
su username                    # Switch user
sudo useradd -m username       # Create new user
sudo passwd username           # Set password
sudo userdel username          # Delete user
sudo usermod -aG sudo user     # Add user to sudo group
cat /etc/passwd                # List all users
cat /etc/group                 # List all groups
```

---

## Group Management
```bash
sudo groupadd groupname                    # Create group
sudo groupdel groupname                    # Delete group
sudo gpasswd -M user1,user2 groupname      # Add multiple users to group
sudo usermod -aG groupname username        # Add single user to group
sudo gpasswd -a username groupname         # Add user to group
```

---

## Package Management (Ubuntu/Debian)
```bash
sudo apt update             # Refresh package list
sudo apt upgrade            # Upgrade all packages
sudo apt install nginx      # Install a package
sudo apt remove nginx       # Remove a package
```

---

## Process Management
```bash
ps                     # Your processes
ps aux                 # All system processes
top                    # Live process monitor
kill -9 <PID>          # Kill a process
free -h                # RAM usage
vmstat                 # Memory + storage stats
nohup command &        # Run in background, survives logout
```

---

## System Info
```bash
uname -a               # OS and kernel info
uptime                 # System uptime
date                   # Current date/time
df -h                  # Disk usage
du -sh /path           # Size of a folder
lsblk                  # List block devices
```

---

## Service Management (systemctl)
```bash
systemctl status nginx        # Check service status
sudo systemctl start nginx    # Start service
sudo systemctl stop nginx     # Stop service
sudo systemctl restart nginx  # Restart service
sudo systemctl reload nginx   # Reload config
```

---

## SSH
```bash
ssh-keygen                             # Generate key pair
ssh -i keyfile.pem ubuntu@<ip>         # Connect to server
chmod 400 keyfile.pem                  # Fix key permission
exit                                   # Disconnect from server
ls -a                                  # See hidden .ssh folder
cat ~/.ssh/authorized_keys             # View allowed public keys
```

---

## Text Processing
```bash
grep "word" file               # Find word in file
grep -i "word" file            # Case-insensitive
grep -c "word" file            # Count matches
grep -i -c "info" applog       # Count case-insensitive

awk '{print $2}' file          # Print column 2
awk '/error/ {print $3}' file  # Print col 3 of lines with "error"

sed 's/old/new/g' file         # Replace text (view only)
sed -i 's/old/new/g' file      # Replace text (modify file)

find /path -name "*.txt"       # Find files by name
find /path -type f             # Find all files
```

---

## Networking
```bash
ping google.com                # Check connectivity
nslookup google.com            # Find IP of domain
dig google.com                 # Detailed DNS info
traceroute google.com          # Path to server
ifconfig                       # Network interfaces + IP
ip a                           # Modern ifconfig
netstat                        # Network stats
wget https://url.com/file      # Download file
curl -X GET https://api.com    # API call (GET)
curl -X POST https://api.com   # API call (POST)
hostname                       # Machine name
```

---

## Compression & File Transfer
```bash
zip archive.zip file           # Zip a file
zip -r archive.zip folder      # Zip a folder
unzip archive.zip              # Unzip

scp file ubuntu@ip:/path       # Copy file to remote
rsync -avz src ubuntu@ip:/dst  # Sync files to remote
```

---

## LVM (Logical Volume Manager)
```bash
lsblk                                  # See all disks
lvm                                    # Enter LVM shell

# Physical Volume
pvcreate /dev/xvdf /dev/xvdg           # Create PV
pvs                                    # List PVs
pvdisplay                              # PV details

# Volume Group
vgcreate devops /dev/xvdf /dev/xvdg   # Create VG
vgs                                    # List VGs
vgdisplay                              # VG details

# Logical Volume
lvcreate -L 10G -n devops             # Create LV (10GB)
lvs                                    # List LVs
lvdisplay                              # LV details
lvextend -L +5G /dev/devops/devops-lv  # Extend LV by 5GB

# Mount Volume
mkfs.ext4 /dev/devops/devops-lv       # Format volume
mkdir /mnt/myvolume                    # Create mount point
mount /dev/devops/devops-lv /mnt/myvolume  # Mount it
umount /mnt/myvolume                   # Unmount
```

---

## Important Directories
```
/etc          → Config files
/var          → Logs, cache (changes over time)
/tmp          → Temp files (anyone can access)
/home         → User files (/home/username)
/root         → Root user's home
/bin          → Basic commands
/sbin         → System commands (for root)
/opt          → Third-party apps
/mnt          → Mount point for drives
/dev          → Device files
/boot         → Boot files
```

---

## Quick Reminders
- `sudo` = Run as admin
- `~` = Your home directory
- `.` = Current directory
- `..` = Parent directory
- `Ctrl + C` = Stop a running command
- `Ctrl + D` = Exit terminal / logout
- `Tab` = Auto-complete command or path
- `↑ arrow` = Previous command
- `man command` = Read manual for any command (e.g., `man ls`)
