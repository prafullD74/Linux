# Linux

[Open source](https://www.redhat.com/en/topics/open-source) generally refers to a type of software released through a specific kind of license that makes its source code legally available to end-users. 
A [Linux distro](https://www.redhat.com/en/topics/linux/whats-the-best-linux-distro-for-you) is an installable operating system (OS) that’s built from the Linux kernel and supports user programs, repositories, and libraries. 
Because [Linux is open source](https://www.redhat.com/en/topics/linux/what-is-linux) and released under the [GNU General Public License (GPL)](https://www.gnu.org/licenses/licenses.html), anyone can run, study, modify, and redistribute the source code, or even sell copies of their modified code.
 
choose a Linux distro?
    1. CentOS (CentOS Linux, CentOS Streams)
    2. Debian
    3. Red Hat® Enterprise Linux(Enterprise—or commercial—Linux distros)
    4. Ubuntu 
    5. Fedora Linux
    6. Kali Linux
    7. openSUSE
 
Community—or upstream—distros are free Linux versions primarily supported and maintained by an open source software-development community.  if you’re trying to run a [server](https://www.redhat.com/en/topics/linux/linux-server) for a long period of time, community distros might not be the best choice.
Red Hat Enterprise Linux offers 10 years of lifecycle support (as opposed to Fedora Linux’s 2 years), so you can better maintain long-term applications.
Enterprise distros sometimes include package managers, which are programs that help with the installation and management of Linux software packages. 
A package manager is a command-line or graphical tool used to automate the process of installing, updating, and removing software packages on a Linux system.
Package managers facilitate the installation of software packages from repositories or local files. They automatically handle dependencies, ensuring that all required components are installed.
 
APT (Advanced Package Tool) is a powerful and widely used package manager in the Linux world. It's the default package manager for Debian-based distributions, including Debian itself, Ubuntu, and Linux Mint.
Installing a package : sudo apt-get install package-name
Updating the package list : sudo apt-get update
Upgrading packages: sudo apt-get upgrade
Removing a package: sudo apt-get remove package-name
Searching for packages:  apt-cache search package-name
 
YUM (Yellowdog Updater, Modified) is a package manager primarily used in Red Hat-based Linux distributions such as CentOS, Fedora, and RHEL (Red Hat Enterprise Linux). 
The main configuration file for YUM is at /etc/yum.conf, and all the repos are at /etc/yum.repos.d.
[adding repositories to your system](https://www.redhat.com/sysadmin/add-yum-repository)
The history option gives you an overview of what happened in past transactions. This provides some useful information, like the date when the transaction happened and what command was run.
???? How to configure these repositories to obtain software from both official sources and trusted third-party repositories. ???
 
Installing a package: sudo yum install package-name
Updating the package list: sudo yum makecache
Upgrading packages: sudo yum update
Removing a package:  sudo yum remove package-name
undoing a transaction: yum history undo <id>
 
dnf is the successor to YUM and is now the recommended package manager for Fedora-based distributions.
Installing a package: sudo dnf install package-name
Updating packages: sudo dnf upgrade
 
Package file format: .rpm, RPM is a popular package management tool in Red Hat Enterprise Linux-based distros. An RPM package consists of an archive of files and metadata. Metadata includes helper scripts, file attributes, and information about packages. RPM maintains a database of installed packages, which enables powerful and fast queries. The RPM database is inside /var/lib, and the file is named __db*. The flag -i is for install, U is for upgrade, v for verbose, h for hash (this option displays the # as a progress bar for the operation).
To erase a package : rpm -e erase-options package-name
To query for a package : rpm -q query-options package
 
Zypper is the default package manager used in openSUSE and its derivatives.
 
DPKG (Debian Package Manager) is a fundamental package management tool for Debian-based Linux distributions, including Debian itself, Ubuntu, and their derivatives. DPKG is responsible for installing software packages on a Debian-based system. Users can install packages from local .deb files or by specifying package names if the packages are already present on the system.
Installing a package from a .deb file: sudo dpkg -i package.deb
Removing a package: sudo dpkg -r package-name
Querying package information: dpkg -l | grep package-name
 
Systemd is a system and service manager for Linux operating systems. It is designed to replace traditional init systems like SysV init and Upstart and is responsible for initializing the system, starting services, managing daemons, and monitoring system state. Its approach to managing processes is both efficient and powerful.
 
systemctl is the primary command-line interface for interacting with systemd. It provides a wide range of functions for managing services, viewing their status, and controlling the system's behavior.
To start a service : sudo systemctl start apache2
To stop a service : sudo systemctl stop apache2
To ensure a service starts at boot : sudo systemctl enable apache2
To disable a service from starting at boot: sudo systemctl disable apache2
To restart a service: sudo systemctl restart apache2
To reload configuration files without stopping the service: sudo systemctl reload apache2
To view the status of a service: systemctl status apache2
list all currently active units (services, sockets, targets, etc.) : systemctl list-units --type=service
 
systemd and systemctl play a crucial role in managing processes and services, improving system startup times and ensuring efficient service management. 
