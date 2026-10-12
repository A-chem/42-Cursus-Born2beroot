# Virtualization

**Virtualization** is the process of creating a virtual version of something, like a computer, server, or storage, instead of using physical hardware. It allows one physical machine to act like multiple separate machines.
# What is a Virtual Machine

A **Virtual Machine (VM)** is a software-based computer that runs inside a real, physical computer. It acts like a separate computer, with its own operating system (OS), applications, and resources, but it is virtual instead of physical.
(VM) works by using a [[Hypervisor]]to create a simulated environment that behaves like a physical computer.
# How do Virtual Machines work?
A **Virtual Machine (VM)** works by using a software layer called a [[Hypervisor]], which allows your physical computer to create and run virtual computers. The [[Hypervisor]] divides the hardware resources, such as CPU, memory, and storage, into isolated parts, and assigns these resources to one or more VMs. Each VM acts like a separate computer, with its own [[Operating Oystem]] and applications, even though it’s running on the same physical machine.
# The basic differences between Rocky and Debian

- **Rocky Linux** is based on **Red Hat** and designed for **servers** and **businesses**. It’s stable, long-term, and works well in enterprise environments. It uses **RPM** packages and **YUM** for managing software.
    
- **Debian** is a **general-purpose** Linux that can be used on **desktops** and **servers**. It’s known for its stability and open-source nature. It uses **DEB** packages and **APT** for managing software.
# The purpose of virtual machines

- **Run Different Operating Systems**: For example, run Windows on a Mac or Linux on Windows.
- **Test Software**: Safely test new software or configurations without risking your main system.
- **Save Resources**: Use one physical machine to run many virtual computers, saving space and cost.
- **Isolation**: Keep each virtual machine separate so that problems in one don't affect others.
#  Apt vs Aptitude?

## Debian(package management system)

Is a Linux-based operating system built around packages. Nearly everything in Debian is delivered as a [[Package(.deb)]].
- The kernel (core of the OS) is a package.
- Applications like Firefox.... Player are packages.
- Even system utilities like bash (the shell)...are distributed as packages.

**Managing software manually can be messy :**

1. Find the software online.
2. Download it.
3. Ensure it’s compatible with your system.
4. Check for and install additional required software ([[Dependencies]]).

**Package Management :**

1. Finds the software you want from a [[Repository]].
2. Downloads the correct package version for your system.
3. Installs the package along with any required dependencies.
4. Keeps track of everything so you can easily upgrade or remove software.

### Tools 
#### DPKG (Debian Package)

The low-level tool that installs .deb files directly. It doesn’t resolve dependencies automatically. If the software needs another package to work, you must install that package manually.

**Command**: `sudo dpkg -i <package_name>.deb`
#### APT (Advanced Package Tool)

A higher-level tool that works with repositories. It automatically resolves and installs dependencies. It comes by default and doesn't offer a graphical interface to manage the tools that are installed and the ones that you can need in the future. Apt command offers a lot of sub-commands that help you to manage your system so that the packages can be added, updated, removed, or fixed if a problem occurs. 

**Command**: `sudo apt install <package_name>`

### Aptitude(Advanced Package Tool)
Is another popular tool that you can use over apt the possibility to manage your packages through command lines and also from a visual interface directly on your terminal. When facing a package conflict, `apt` will not fix the issue while `aptitude` will suggest a resolution that can do the job.

**Command**: `sudo aptitude install <package_name>
[[Aptitude.png]]

# APPArmor

Is a Linux security module that enhances system security by restricting what resources an application can access.Instead of relying solely on user and group permissions (Discretionary Access Control or DAC), AppArmor uses Mandatory Access Control (MAC), where system administrators can define what files, capabilities, and other resources an application is allowed to use, regardless of user permissions.

**Check if AppArmor is installed :** `sudo aa-status`

**If it’s not installed :** `sudo apt install apparmor apparmor-utils`

# Configure locals

1. We will choose the version without graphic interface.
2. Now language must be choosed for the machine.
3. It's time to select the country.
4. Time to select continent.
5. Now select the country.
6. Our keyboard follows the ANSI standard so `American English`.
# Configure the network

1. Now we must set a `Host Name` of the machine `achemlal42`
# Set up users and passwords

1. set a password for the root user `Rootuser12`
2. set up the user name, the name for that user have to be your student login `achemlal`
3. set our new user password `Abdilah123`
# Configure the clock

1. Select your time zone.

# BONUS: Partition Disks

**Partitioning a disk** refers to dividing a physical storage device, such as a hard drive (HDD) or solid-state drive (SSD), into multiple logical sections called **partitions**. Each partition acts as a separate unit of storage, allowing the system to manage different data independently.

1. When choosing disk partitioning, we will select manual.
[[image (1).png]]

2. it shows us a general description of our partitions and mount points. Currently, we do not have any partitions. To create a new partition table, we must choose the device where we want to create them. 
[[image(2).png]]

3. it shows us a general description of our partitions and mount points. Currently, we do not have any partitions. To create a new partition table.
[[image (9).png]]

## Types of Partitions:

- **Primary Partitions**: These are the main partitions where the OS and data can be stored. A disk can have up to four primary partitions. . There can only be 4 primary partitions per hard drive or 3 primary and one extended.

-  **Extended Partition**: A type of partition that acts as a container for multiple logical partitions, allowing more than four partitions on a disk.

- **Logical Partitions**: Created inside an extended partition, logical partitions allow you to have more than four partitions.

We will start by creating this:
[[image (4).png]]
# BONUS: primary partition

1. We will create a new partition.
2. he size of the partition must be `525m`
3. We choose primary because it will be the partition where the Operating System will be installed.
4. We will select beginning because we want the new partition to be created at the `beginning` of the available space.
5. We will modify the [[Mount Point]] as specified in the subject. We choose [[boot]] as the mount point for our partition.
[[image(5).png]]
# BONUS: logical partition

1. We will start creating this:
[[image (6).png]]
2. create a logical partition `(Physical volume)` with all the available space `max` on the disk, which has no mount point and is encrypted.
3. create the encrypted volumes `/dev/sda5` password `1234`
# BONUS: logical volume manager

**logical volume management([[LVM]]):**** is a system for managing disk storage in Linux. It allows you to combine multiple physical disks into one or more logical volumes (virtualized storage), which can then be used like a single partition.
  
1. We will create a new volume group.
2. We will enter the name we want to give it. `LVMGroup`
3. select the partition where we want to create the group  `/dev/mapper/sda5_crypt`.
4. Create logical volume.
[[image (8).png]]
5. start by choosing the group where we want them to be created.

| LVs     | Size   |
| ------- | ------ |
| root    | 10.7GB |
| swap    | 2.5GB  |
| home    | 5.4GB  |
| var     | 3.2GB  |
| srv     | 3.2GB  |
| tmp     | 3.2GB  |
| var-log | 4.3GB  |

# BONUS: [[filesystem]] of all logical volumes

1. select the [[filesystem]] (Ext4 journaling file system) that we want and the [[Mount Point]] indicated in the subject .
[[image (9).png]]

| LVs     | Mount Point |
| ------- | ----------- |
| root    | /           |
| swap    | swap        |
| home    | /home       |
| var     | /var        |
| srv     | /srv        |
| tmp     | /tmp        |
| var-log | /var/log    |

# Configure the package manager

1. `No` as is not required additional packages
2. choose `deb.debian.org` as is the recommended by debian itself.

# Install the [[GRUB (Grand Unified Bootloader)]] boot loader

1. install [[GRUB (Grand Unified Bootloader)]] boot in the hard disk
2. choose the device `/dev/sda (ata_VBOX_HARDDISK)` for the installation for boot loader.
3. finish installation

# Starting Your Virtual Machine

1. Press enter on `Debian GNU/Linux`.
2. Enter your encryption password you had created before.
3. Login in as the your_username you had created before.
4. Type `lsblk` in your Virtual Machine to see the partition.

# Configurating Your Virtual Machine
## Installing [[Sudo]]

1. First type `su -` to login in as the root user.
2. Then type `apt install sudo`
3. Verify whether _sudo_ was successfully installed via `dpkg -l | grep sudo`.
4. Add user to _sudo_ group via `adduser <username> sudo` or  `usermod -aG sudo <username>`
5. Verify whether user was successfully added to _sudo_ group via `getent group sudo`.
6. Type `sudo visudo` to open sudoers file
7. Lastly find - # User privilege specification, type `your_username ALL=(ALL) ALL`.
- `your_username`: The user to which you're granting sudo privileges.
- `ALL`: This means the user can run commands from any host (for network configurations).
- `(ALL)`: The user can run commands as any user, including root.
- `ALL`: The user can run any command as root.
9. We must reboot machine so the changes can be applied `sudo reboot`
##  Creating sudo.log

1. Limit Authentication Attempts to 3. Open the sudoers file using `sudo visudo` and Add or modify the following line `Defaults        passwd_tries=3`
2. Display a Custom Error Message for Wrong Password In the same `sudoers` file, add or modify `Defaults badpass_message="Your custom error message here"`
3. Archive sudo Actions in /var/log/sudo To log all sudo activities (both inputs and outputs) in a specific directory `sudo mkdir -p /var/log/sudo` and `sudo chmod 700 /var/log/sudo` In the `sudoers` file, add or modify : `Defaults log_input, log_output, iolog_dir=/var/log/sudo`
- `log_input`: Archives the commands run using `sudo`.
- `log_output`: Archives the output of those commands.
- `iolog_dir`: Specifies the directory where logs are saved.
4.  Enable [[TTY]] Mode for Security. Enabling TTY ensures sudo commands can only be run from a terminal session, adding an extra layer of security. Add or modify the following line in the `sudoers` file: `Defaults        requiretty`
5. Restrict Paths for sudo. Restricting paths ensures users can only execute commands located in approved directories, reducing potential misuse.Add or modify the following line in the `sudoers` file: - `Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"`
## Installing Git and Vim

1. Then type `apt-get install git -y` to install Git
2. Then type `git --version` to check the Git Version
1. Then type `apt-get install vim -y` to install Vim
2. Then type `vim --version` to check the Vim Version
## Installing & Configuring [[SSH (Secure Shell Host)]]

1. Type `sudo apt install openssh-server`
2. verify ssh installation `dpkg -l | grep openssh-server`
3. Type `sudo systemctl status ssh`  or  `sudo service ssh status` to check SSH Server Status
4. with the file [[sshd_config]] `sudo vim /etc/ssh/sshd_config`
5. Find this line `#Port22`
6. Change the line to `Port 4242` without the # (Hash) in front of it  and disable root login `PermitRootLogin no` if y want restrict SSH access to specific users(Optional, but recommended) `AllowUsers 
7. Now with the file  [[ssh_config]] `/etc/ssh/ssh_config`. (not `sshd_config`) :`nano /etc/ssh/ssh_config`
8. Restart the SSH service to apply changes `sudo systemctl restart sshd` or `sudo service ssh restart`
9. Check if SSH is running on the correct port: `sudo ss -tuln | grep 4242` You should see something like: `LISTEN 0 128 0.0.0.0:4242 0.0.0.0:*`
10. Use a second terminal or another machine to test `ssh your_username@your_vm_ip -p 4242` and You should not be able to connect as root `ssh root@your_vm_ip -p 4242`This should fail with a message like: - `Permission denied (publickey, password).`
##  Installing & Configuring [[UFW (Uncomplicated Firewall)]]

1. First type `apt-get install ufw` to install UFW
2. verify ssh installation  `dpkg -l | grep ufw`
3. Type `sudo ufw enable` to inable UFW
4. Type `sudo ufw status numbered`  or `sudo systemctl status ufw` to check the status of UFW
5. Type `sudo ufw allow ssh` to configure the Rules
6. Type `sudo ufw allow 4242` to configure the Port Rules
7. Lastly Type `sudo ufw status numbered` to check the status of UFW 4242 Port

## Connecting to SSH

0. Go to your Virtual Box Program
1. Click on your Virtual Machine and select `Settings`
2. Click `Network` then `Adapter 1` then `Advanced` and then click on `Port Forwarding`
3. Change the Host Port and Guest Port to `4242`
4. Type `sudo systemctl restart ssh` to restart your SSH Server
5. Type `sudo service sshd status` to check your SSH Status
6. Open an iTerm and type the following `ssh your_username@127.0.0.1 -p 4242`

## User Management

### Step 1: Modify the Hostname

 1. Change the hostname to your login followed by `42` use command `sudo hostnamectl set-hostname wil42`. Verify the change : `hostnamectl`
### Step 2: Implement the Strong Password Policy

To implement the password policy, you need to modify the `/etc/login.defs` file and set password aging rules, as well as configure `pam_pwquality.so` for password strength.

1. Set Password Aging Rules. Edit `/etc/login.defs` to configure password expiration and minimum password change settings: `sudo nano /etc/login.defs` and Add or modify the following lines:

- `PASS_MAX_DAYS   30       # Maximum days before password expires | sudo chage -M 30 username
` 
- `PASS_MIN_DAYS   2        # Minimum days before password can be changed | sudo chage -m 2 username`
- `PASS_WARN_AGE   7        # Number of days before expiry to warn user | sudo chage -W 7 username`

2. `sudo apt-get install libpam-pwquality` to install Password Quality Checking Library
3. Configure Password Complexity. Edit `/etc/pam.d/common-password`. Add the following line :`password requisite pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root`
4. Check the password expiration date using the `chage` command:`sudo chage -l testuser`

### Step 3:Create the User with Your Login as Username &Create group user42

To create a user with your login name (e.g., `wil42`) and make sure they belong to both the `user42` and `sudo` groups:
1. Create the user: `sudo useradd wil42`
2. Set a password for the user: `sudo passwd wil42`
3. Add the user to the `user42` and `sudo` groups: `sudo usermod -aG user42,sudo wil42`
4. Verify group membership: `groups wil42`
5. Create a new group  `sudo groupadd groupname`
##  Script
1. Edit the crontab file `sudo crontab -u` [[Cron]]
2. `*/10 * * * * sh /home/achemlal/monitoring.sh`.
`#!/bin/bash`

`wall "`
`Broadcast message from root@$(hostname) (tty1) ($(date)):`
`#Architecture: $(uname -a)`
`#CPU physical: $(nproc --all)`
`#vCPU: $(nproc)`
`#Memory Usage: $(free -m | awk 'NR==2 {print $3}')/$(free -m | awk 'NR==2 {print $2}')MB ($(free -m | awk 'NR==2 {print $3/$2*100}' | xargs printf "%.2f"))%`
`#Disk Usage: $(df -h / | awk 'NR==2 {print $3}')/$(df -h / | awk 'NR==2 {print $2}') ($(df -h / | awk 'NR==2 {print $5}'))`
`#CPU load: $(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')%`
`#Last boot: $(uptime -s | awk '{print $1 " " $2}')`
`#LVM use: $(lsblk -o NAME,TYPE | grep -q 'lvm' && echo yes || echo no)`
`#Connections TCP: $(ss -t | grep ESTAB | wc -l) ESTABLISHED`
`#User log: $(who | wc -l)`
`#Network: IP $(hostname -I | awk '{print $1}') ($(ip link show | grep 'ether' | awk '{print $2}'))`
`#Sudo: $(journalctl _COMM=sudo | grep COMMAND | wc -l) cmd`
`"`
`#!/bin/bash`
`while true`
	`do`
	`sleep 60`
	`wall "`
		`#Architecture: $(uname -a)`
		`#CPU physical: $(nproc --all)`
		`#vCPU: $(nproc)`
		`#Memory Usage: $(free --mega | awk 'NR==2 {print $3}')/$(free -mega | awk 'NR==2 {print $2}')MB ($(free --mega | awk 'NR==2 {print $3/$2*100}' | xargs printf "%.2f"))%`
		`#Disk Usage: $(df -h / | awk 'NR==2 {print $3}')/$(df -h / | awk 'NR==2 {print $2}') ($(df -h / | awk 'NR==2 {print $5}'))`
		`#CPU load: $(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')%`
		`#Last boot: $(uptime -s | awk '{print $1 " " $2}')`
		`#LVM use: $(lsblk -o NAME,TYPE | grep -q 'lvm' && echo yes || echo no)`
		`#Connections TCP: $(ss -t | grep ESTAB | wc -l) ESTABLISHED`
		`#User log: $(who | wc -l)`
		`#Network: IP $(hostname -I | awk '{print $1}') ($(ip link show | grep 'ether' | awk '{print $2}'))`
		`#Sudo: $(journalctl _COMM=sudo | grep COMMAND | wc -l) cmd"`
	`done`
`@reboot sh /home/achemlal/monitoring.sh`
1. **System Architecture** 
	`#Architecture: $(uname -a)`
	- **`uname -a`**: 
	This command shows details about the operating system, including the version of the kernel, the architecture (whether it's a 32-bit or 64-bit system), and other information.
2. **Number of Physical CPUs**  
	`#CPU physical: $(nproc --all)`
	- **`nproc --all`**:
	This tells you how many physical CPU cores your machine has. For example, if you have a 4-core processor, this will return `4`.
3. **Number of Virtual CPUs** 
	`#vCPU: $(nproc)`
	 - **`nproc`**:
	 This command shows how many virtual CPU cores your machine has. This is usually the same number or higher than the number of physical CPUs, especially if your system supports **hyperthreading** (a technology that lets each physical core act like two virtual cores).
4. **Memory Usage**
	`#Memory Usage: $(free -m | awk 'NR==2 {print $3}')/$(free -m | awk 'NR==2 {print 
	- **`free`** 
	command in Linux shows the system's memory usage, including the amount of free and used memory.
	- **`-m`** 
	flag is used to display the values in **megabytes (MB)**, rather than the default **kilobytes (KB)**.
	- **`awk`** 
	is a powerful scripting language used for manipulating data and generating reports, supporting variables, numeric and string functions, and logical operators without requiring compilation. It enables pattern scanning and processing, allowing users to define actions to take when specific text patterns are matched in files or lines of a document
	- **`NR==2`** 
	means "process the second line" (NR stands for "Number of Records", i.e., the line number in the input).
	- **`{print $3}`**
	means "print the third column" of the second line.
	- **`awk 'NR==2 {print $3}'`**
	Extracts the third column (used memory) from the second line of the `free -m` output.
5. **Disk Usage** 
	`$(df -h / | awk 'NR==2 {print $3}')/$(df -h / | awk 'NR==2 {print $2}') ($(df -h / | awk 'NR==2 {print $5}'))`
	- **`df -h /`** 
	This checks the disk usage of the root directory `/` and outputs the result in a human-readable format (e.g., KB, MB, GB).
	- **`awk 'NR==2 {print $3}'`** :
    This extracts the "Used" space from the second line of the `df` output (which corresponds to the `/` filesystem).
	- **`awk 'NR==2 {print $2}'`** 
	This extracts the "Size" (total space) from the second line.
	- **`awk 'NR==2 {print $5}'`** 
	This extracts the "Use%" (percentage used) from the second line.
6. **CPU Load** 
	`$(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')%`
	- **`s/`**:  
    This begins the **substitution** in `sed`. It tells `sed` to search for a specific pattern and replace it with something else.
	- **`.*, *`**:
    - `.*` matches any characters (zero or more) up until the first instance of the next part of the pattern.
    - `, *` matches a comma (`,`) followed by zero or more spaces.
    - Together, `.*, *` is used to skip over all the characters before the actual CPU usage information. In the case of the `top` command output, it would match everything before the CPU stats.
	- **`\([0-9.]*\)`**:
    - This is a **capture group**. The part inside `\(` and `\)` will be captured for later use in the substitution (replaced by `\1`).
    - `[0-9.]*` matches any number of digits (`0-9`) or decimal points (`.`). This part is intended to capture the **idle CPU percentage** (e.g., `75.2` for 75.2% idle).
	- **`%* id.*`**:
    - `%*` matches zero or more `%` symbols. This is used to match the percentage symbol that follows the number (in case there are extra spaces or symbols after the percentage).
    - `id.*` matches the word `id` followed by any number of characters after it. This part is included because `id` represents the idle CPU percentage in the `top` command output, and we want to capture everything up to that point to extract the number.
	- **`\1`**:
    - This refers to the first captured group, which is the number corresponding to the idle CPU percentage.
7. **Last Boot Time**
	`$(uptime -s | awk '{print $1 " " $2}')`
	 - **`uptime -s`** 
		 This gives you the system's uptime start time.
	- **`awk '{print $1 " " $2}'`**
		This is used to format the output from `uptime -s`
8. **LVM (Logical Volume Management)** 
	`$(lsblk -o NAME,TYPE | grep -q 'lvm' && echo yes || echo no)`
	- `lsblk -o NAME,TYPE`:
	    - `lsblk` lists information about all available block devices (like hard drives and partitions).
	    - The `-o NAME,TYPE` option specifies that only the `NAME` (device name, e.g., `/dev/sda1`) and `TYPE` (type of the device, e.g., `part` or `lvm`) will be shown.
	- `grep -q 'lvm'`:
	    This searches for the word `lvm` in the output of `lsblk`. The `-q` flag tells `grep` to operate quietly (i.e., it doesn't display any matches but only sets the exit status).
	- `&& echo yes || echo no`:
    - This is a conditional check.
    - If the `grep` command finds `lvm` in the `lsblk` output, the exit status will be `0` (success), and `echo yes` will be executed.
    - If `grep` does not find `lvm`, the exit status will be non-zero (failure), and `echo no` will be executed.
9. **TCP Connections** 
	`$(ss -t | grep ESTAB | wc -l) ESTABLISHED`
	- `ss -t`
		This lists all TCP sockets. The `-t` flag is used to show TCP connections.
	- `grep ESTAB`
		Filters the output of `ss` to show only the lines that contain "ESTAB", which indicates an established connection.
	- `wc -l`
		Counts the number of lines from the previous output, which corresponds to the number of established TCP connections.
10. **Logged-In Users**
	`$(who | wc -l)`
	- **`who`**:
		The `who` command is used to display information about users who are currently logged into the system. It shows details like the username, terminal, login time, etc.
	 - **`wc -l`** 
		 command counts the number of lines in the input it receives. In this case, it counts how many users are logged in because each user will appear on a separate line in the output of `who`.
11. **Network Information (IP and MAC addresses)**
	`IP $(hostname -I | awk '{print $1}') ($(ip link show | grep 'ether' | awk '{print $2}'))`
	- **`hostname -I`**
		This command returns all the IP addresses assigned to the host, and `awk '{print $1}'` will print the first one (in case there are multiple).
	- **`ip link show`**
		This command displays information about all network interfaces.
	- **`grep 'ether'`**
		Filters the output to show only lines with the MAC address.
	- **`awk '{print $2}'`**
		Extracts the MAC address from the second field of the output.
12. **Number of `sudo` Commands Executed**
	`$(journalctl _COMM=sudo | grep COMMAND | wc -l) cmd`
	- `journalctl _COMM=sudo`
		Filters journal logs for entries related to the `sudo` command. The `_COMM=sudo` filter ensures you're only looking at logs for commands run with `sudo`.
	- `grep COMMAND`
		Looks for lines containing the string `COMMAND`, which appears in the logs when a sudo command is executed.
	- `wc -l`
		Counts the number of matching lines.
# BONUS SERVICES
1. Install [[Lighttpd]]  `sudo apt install lighttpd`
2. 