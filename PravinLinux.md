#### Which two columns do you really want to be removed. Your output has INFO_NAM & PROCID deleted 
>awk '{$(NF-1)=$(NF-2)=""};1' <file | column -t can format it nicely. 
#### Don't print 6th and 8th column
- awk '{$6=$8=""; print $0}' file
- awk '{print $1,$2,$3,$4,$5,$7}' file

### I would like to delete the 3rd column(in-place editing)
>awk '!($3="")' file		

### diff between rsync and scp


#### Linux code
- pwd		---print working or present directory path
- touch xyz	---create xyz file in present directory
- ls		---shows all contain form the present directory
- date		---shows the today date

### How to delete history parmanantly in linux??
- ls -l
- ls -ld
- chown <user name> <file name>		----change file ownership
- useradd <user name>				----create user in linux
- id <user name>					----how to check user created or not
- pidof proces_name
- free								----Free command used to check the used and available space of physical memory and swap memory in KB.
- fstab								----/etc/fstab all mounted partition mount here permanantly
- fdisk	-l						
- axel https://releases.ubuntu.com/20.04.2.0/ubuntu-20.04.2.0-desktop-amd64.iso
- links www.tecmint.com
- elinks www.tecmint.com
- lsb_release -a		
- ln -l 

---
### tar,gzip,bzip,bzip2 command flags and syntax
- tar -zcvf name_of_tar.tar /path/to/folder
- tar -zxvf Name_of_tar_file.tar
- gzip -cvzf name_of_archive.tar.gz /path/to/folder
- gunzip file_name.tar.gz

- A: Append tar files to existing archives.
- c: Create a new archive file.
- d: Compare archive with Specified filesystem.
- j: bzip the archive
- r: append files to existing archives.
- t: list contents of existing archives.
- u: Update archive
- x: Extract file from existing archive.
- z: gzip the archive
– delete: Delete files from existing archive.

---

### Grep command - grep or Global Regular Expression Print is the main search program on Unix-like systems which can search for any type of string on any file or list of files or even output of any command.
---
What is the flag for grep?
>The four most commonly used flags to grep are 
- c: This prints only a count of the lines that match a pattern
- h: Display the matched lines, but do not display the filenames.
- i: Ignores, case for matching
- l: Displays list of a filenames only.
- n: Display the matched lines and their line numbers.
- v: This prints out all the lines that do not matches the pattern
- e exp: Specifies expression with this option. Can use multiple times.
- f file: Takes patterns from file, one per line.
- E: Treats pattern as an extended regular expression (ERE)
- w: Match whole word
- o: Print only the matched parts of a matching line
 
### Another less well-known flag that is rather useful is -e.
- dpkg -l | grep -i python
- cat file_name |grep -i error
- ps -ef |grep jvm_name

---

### Total Runlevel’s in Linux is 7 which is 0 to 6 
1. init0 - shutdown or poweroff 
2. init1 - Boot with single user mode and no Network, no GUI, no Login credential, only “/” mounted, only minimal drivers and services. 
3. Init2 - Multiuser Mode without Network and No NFS and No GUI 
4. init3 - Multiuser Mode with all possibility but only No GUI and when No GUI there No Processor Load. 
5. Init4 - same as runlevel 3 but reserved for developer to development.
6. Init5 - Bydefault runlevel all possibility and GUI also present. 
7. Init6 - Reboot or Restart again again

---

### How to find Machine Hardware and motherboard information. 
- uname -a 		(view linux system information and architechture details) 
- lshw -short 		(information all system hw related with short table) 
- dmesg | grep -i pci 
- dmidecode 
- biosdecode

---

### Top command used for collect and display all information from proc which loaded in ram 
- 1st row contain 	-–uptime	—how  many user login	—load average with 1min 5min 15min 
- 2nd row contain 	--total task	—running task	—sleeping task—stopped task—zombie task 
- 3rd row contain 	--how many % CPU used by User process, System process—nice value	—CPU ideal Status value 
- 4th row contain 	--RAM total Memory Size	—free size—	used size—cache and buffer memory 
- 5th row contain		--swap total memory siz	-free size	—used size	—available memory
- 6th row contain 	--process ID	—user name	—nice value	-%cpu	-%memory	—time --command name 

---

### File System Hierarchy 
- / - Primary hierarchy root and root directory of the entire file system hierarchy
- /bin - This stands for binaries and contains the fundamental utilities that are needed by all users also for Essential command  example: ps, ls, ping, grep, cp.
- /sbin - This stands for System Binaries, and contains the fundamental utilities needed to start, maintain and recover the system and also system binaries used typically by system aministrator, for system maintenance purpose eg.iptables, reboot, fdisk, ifconfig, swapon
- /root - This is the home location for the system administrator root.
- /srv - This one is server data which is data for services provided by the system.
- /sys - This contains a sysfs virtual filesystem which holds information related to the hardware.
- /etc - This contains configuration files for the system and system databases. For example: /etc/resolv.conf, /etc/logrotate.conf
- /opt - Contains add-on software, larger programs may install here rather than in /opt stands for optional and contain third party application files.
- /boot - This contains all the files needed for the booting process like GRUB boot loader’s files and Linux kernels eg.  /boot/initrd.img-2.6.32-24-generic, /boot/vmlinuz-2.6.32-24-generic, /boot/grub/grub.conf
- /dev - This stands for devices, which contains files for peripheral devices and pseudo devices. Eg - /dev/sda, /dev/sr0
- /lib - This is the system libraries and has files like the kernel modules and device drivers for 64bit systems.
- /media- This is default mount point for removable devices like USB drives and media players, etc.
- /proc - This contains virtual filesystems describing the processes information as files. eg-/proc/uptime
- /tmp - This is a place for temporary files. tmpfs mounted on it or scripts on start up usually clear this at boot.
- /mnt - This stands for mount, and contains filesystem mount points. Used for multiple hard drives, multiple partitions, network filesystems and CD ROMs.
- /home - This holds all the home directories for the users.
- /usr - This holds the executables and shared resources that are not system critical and Secondary hierarchy for read-only user data.
- /var - This stands for variable and is a place for files that are in a changeable state. Such as size going up and down and var stands for variable files. 

---

### Netstat command (network statistics) 
>This a command-line tool for monitoring network connections both incoming and outgoing as well as viewing routing tables, interface statistics,etc
- netstat -a | more			------Listing all the LISTENING Ports of TCP and UDP Connections
- netstat -at				------Listing TCP Ports connections
- netstat -au				------Listing UDP Ports connections
- netstat -l				------Listing all LISTENING Connections
- netstat -lt				------Listing all TCP LISTENING Connections
- netstat -lu				------Listing all UDP LISTENING Connections
- netstat -lx				------Listing all UNIX LISTENING Connections

---

### ls command
- r for read access.
- w for write access.
- u for read and write access.
- TYPE – of files and it’s identification.
- DIR – Directory
- REG – Regular file
- CHR – Character special file.
- FIFO – First In First Out

- ls						-----List Files and Directories in Linux
- ls -l						-----Long Listing of Files in Linux
- ls -a						-----View Hidden Files in Linux	
- ls -lh					-----List Files with Human Readable Format
- ls -ltr					-----List Files and Directories in Reverse Order in Linux
- ls -i						-----Display Inode number of File or Directory

---
### fdisk commad
> fdisk stands (for “fixed disk or format disk“) is an most commonly used command-line based disk manipulation utility for a Linux/Unix systems.
- fdisk -l					----View all Disk Partitions in Linux
- fdisk -l /dev/sda			----View Specific Disk Partition in Linux
---
### df commad
>The ‘df‘ command stands for “disk filesystem“, it is used to get a full summary of available and used disk space usage of the file system on the Linux system.
>df -a						----Display Information of all File System Disk Space Usage
>df -h						----Show Disk Space Usage in Human Readable Format
>df -i						---- Display File System Inodes

---
### scp (secure copy) command in Linux system is used to copy file(s) between servers in a secure way. 
>The SCP command or secure copy allows secure transferring of files in between the local host and the remote host or between two remote hosts.
- scp -v Label.pdf mrarianto@IP_address
---
### crontab commad
- * * * * * /bin/ls >/ls.txt
- *	Minute (hold values between 0-59)
- Hour (hold values between 0-23)
-	Day of Month (hold values between 1-31)
-	The month of the year (hold values between 1-12 or Jan-Dec)
-	Day of week (hold values between 0-6 or Sun-Sat)
>Command – The /path/to/command or script you want to schedule.
>crontab -l
>crontab -e			----Edit Crontab Entries
>crontab -r			----Remove Crontab Entry
>30 0 * * *   root   find /tmp -type f -empty -delete			----delete empty files and directory from /tmp at 12:30 am daily.	

---
### chkconfig commad
>The Chkconfig command tool allows to configure services start and stop automatically in the /etc/rd.d/init.d 
- chkconfig -l							----List All Services
- chkconfig -l | grep httpd				----Check Status of Specific Service
- chkconfig --level 2345 httpd off	----turned Off a service called httpd for 2345 run level. 	
---

---
### Find Command 
- find . -type f -name pravin 			(find file in current directory which name is pravin) 
- find . -iname pravin  					(find all in current directory with ignore case  pravin) 
- find  /  -type d -iname pravin 			(find only directory in “/ “ which name is pravin) 
- find  / -type f -name “*.txt”   		(find all .txt file in  ‘ / ’) ->   find . -type f -perm 777   (find all file in current directory with permission 777) 
- find . -type f ! -perm 777  			(find all file in current directory without permission 777) 
- find / -type f -perm 777 -print -exec rm -f {} \; 	(find and delete file with permission 777) 
- find / -type f -name “pravin” -exec rm -f {} \; 		(find and delete file with name pravin) 
- find /tmp -type f -empty Find Empty file in /tmp directory 
- find /tmp -type f -name “.*” 						Find Hidden file in /tmp directory 
- ffind / -mtime 50		 		(find all the files which are modified 50 days back) 
- find / -atime 50 				(find all the files which are accessed 50 days back) 
- find / -mtime 50 -mtime -100 	(To find all the files which are modified more than50days back and less than100days) 
- find / -mmin 60 				(find all the files which are modified in last1 hour back) 
- find / -amin 60 				(find all the files which are accessed in last1 hour back) 
- find / -cmin 60 				(find all the files which are changed in last 1 hour back) 
- fins / -size +50M -size -100M (find all the files with size between 50MB to 100MB ) 
- find / -type f -name “*.mp3” -size +10M -exec rm -f {} \; (find and delete all .mp3 file which having size more than 10MB

