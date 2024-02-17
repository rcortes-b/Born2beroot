# Born2beroot - A short introduction to System Administration and Virtual Machine

⚠️ This is not a 'how to' guide about Born2beroot 42 School Project ⚠️

✅ This is a summary of what I've learned doing this interesting project ✅

## _What Software did I use?_

➡️ Virtual Machine → VMware

➡️ Linux Distribution → Debian (12.4 Version)

➡️ FireWall → UFW

➡️ SSH → OpenSSH

➡️ Web Server → Lighttpd && OpenLiteSpeed

➡️ Database → MariaDB

➡️ WordPress

➡️ PHP 


# Index

1. [💻 What is a Virtual Machine and What is it Used for? ⌨️](#1--what-is-a-virtual-machine-and-what-is-it-used-for-)
2. [💿 Disk Partitions and Logical Volume Management 📀](#2--disk-partitions-and-logical-volume-management-)
3. [🛡️ AppArmor 🔰](#3--apparmor-%EF%B8%8F)
4. [⚙️ Sudo ⛔](#4--sudo-)
5. [📚 Apt and Aptitude 📖](#5--apt-and-aptitude-)
6. [🔒 How to Set a Strong Password Policy 🔑](#6--how-to-set-a-strong-password-policy-)
7. [🌐 SSH 📶](#7--ssh-)
8. [🔥 FireWall 🧱](#8--firewall-)
9. [👾 Scripts && Commads 🤖](#9--script-&&-commands-)
10. [⏱️ Crontab ⏰](#10--crontab-)
12. [⭐ Bonus - WordPress ⭐](#10--bonus-%EF%B8%8F)

## 1- _What is a Virtual Machine and What is it Used for?_ 💻


➤ A Virtual Machine is a simulation of an environment which uses software instead of physical computer hardware to run programs or a different operating system.

➤ It is useful, for example, in the cybersecurity field to do tests without a real risk of infecting your computer with malware or something else.

➤ A Virtual Machine can be useful too for testing a different operative system without the need of disk partitioning.


## 2- _Disk Partitions and Logical Volume Management_ 💿


There is three types of disk partitions: Primaries, Secondaries and Logicals.

➤ Primaries → Limited to 4 primaries partitions. In this partitions is where the operative system is allocated. If you have 1 secondary partition your limit is 3 primaries.

➤ Secondaries → Limited to 1 secondary partition. In this partition is where the logical partitions are allocated.

➤ Logicals → The logical partitions can be part of the secondary or the total amount of it. This partitions allows us to separate different types of data and allocates different amounts of space for different purposes.

### What is a Swap Partition?
➤ A swap partition is for managing the RAM overflow. It's a space for give memory when the operative system decides that needs memory for active processes and the amount of available memory is insufficient.

### What is the Logical Volume Management or LVM?
➤ Logical Volume Management is a system of managing logical volumes or filesystems that is much more flexible than the traditional method of partitioning a disk into one or more segments and formatting it with a single filesystem.


## 3- _AppArmor_ 🛡️


➤ AppArmor is a Linux kernel security module which allows the system administrator to restrict the capabilities of a program.

➤ AppArmor applies a set of rules (like a ‘profile’) to each program. The kernel queries AppArmor before each system call to find out if a process is authorized to perform such an operation.


## 4- _Sudo_ ⚙️


➤ The meaning of 'sudo' is 'super userdo

➤ Sudo is used to grant temporary access to a no root user and elevate the privileges to do some tasks, as it could be adding users or groups.

➤ To establish sudo policies, I have created a file in the directory: "/etc/sudoers.d/" which file will be named 'sudo_config' and it has to contain the following rules:

	Defaults  passwd_tries=3
	Defaults  badpass_message="Custom Error Message"
	Defaults  logfile="/var/log/sudo/[file_name]"  , in this case sudo_log
	Defaults  log_input, log_output
 	Defaults  iolog_dir="/var/log/sudo"
 	Defaults  requiretty
	Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"


## 5 - _APT and Aptitude_ 📚


➤ APT (Advanced Packaging Tool) is a free software user interface, under the conception of software package management.

➤ APT use to be enough for a common use but aptitude is an improved version of APT.

➤ Some differences between APT and Aptitude are:
	
   ↔️ APT offers a command-line interface and aptitude a visual interface.
	
   ↔️ Aptitude offers an interactive mode displaying a list of the software packages and allows to choose which packages you want to install or uninstall.
	
   ↔️ When facing a package conflict, APT will not fix the issue but aptitude will suggest a resolution that can do the job.


## 6 - _How to Set a Strong Password Policy_ 🔒

First of all, I had gone to the file: "/etc/login.defs" file then edited PASS_MAX, PASS_MIN, PASS_WARN which means:
		
↔️ Maximum of days that password will last

↔️ Minimum of days to change password since last password change

↔️ Number of days in which you’ll be warned before your password expires

After these rules, I edited the file: "etc/pam.d/common-password" that I got after downloading a package named libpam-pwquality. In this file, I looked for the line ‘password requisite’ next to ‘retry = 3’ then I typed:

	-minlen = 10 [minimum length of password]
	-ucredit = -1 [minimum 1 Uppercase]
	-dcredit = -1 [minimum 1 Digit]
	-lcredit = -1 [minimum 1 Lowercase]
	-maxrepeat = 3 [Password cannot have a character repeated three continuously times]
	-reject_username [Password cannot contain the username]
	-difok = 7 [At least seven different characters from last password]
	-enforce_for_root [To apply the policy to the root user]


## 7 _SSH_ 📶


SSH is a protocol that grants remote access to a server through a secure channel in which all information is encrypted.

➤Main SSH Commands
			
↔️ sudo ssh service status

↔️ sudo service ssh

↔️ sudo service ssh restart / start / stop

➤ SSH Files

↔️ /etc/ssh/ssh_config

↔️ /etc/ssh/sshd_config

➤ To connect via SSH I allowed a port using the UFW Firewall then I typed in the terminal:
	
 ↔️ ssh -p [port_name] [user]@[ip_address]

After this command I could connect to my Virtual Machine from my original environment.


## 8 _FireWall_ 🧱


➤ A firewall is a network security device that monitors incoming and outgoing traffic and decides whether to allow or block traffic based on a set of predefined security restrictions.

➤ Main Commands

↔️sudo ufw status enable

↔️ sudo ufw status numbered

↔️ sudo ufw allow ‘port_name’

↔️ sudo ufw delete rule_name [using ufw status numbered]

↔️ sudo ufw deny ‘port_name’


## 9 _Scripts && Commands_ 👾


➤ In this part, I did a script which every time is executed displays some data of the environment.
➤ I will summarize the commands but the expected result would be something like this:

***INSERTAR LA IMAGEN DE MI PERFIL --- USO TEMPORAL DE LA IMAGEN DE GEMARTIN :D 
<img width="796" alt="182506484-f5a095b8-4751-461e-a114-f8e36b4cfa9a" src="https://github.com/rcortes-b/Born2beroot/assets/150854181/9155565e-13e8-4914-9bc0-2ae29d02c9dc">

➤ Commands

↔️ wc -l → Count number of lines

↔️ grep → Search for a string of characters in a specified file

↔️ awk →  Text processing language which allows you to make comparisons. 
For  example, awk ‘$1 == “Mem:” will search in the first line ($1) of a  specified file or command output for an occurrence with the ‘Mem:’ string.

↔️ tail → Writes the specified file to standard output beginning at a specified point.

↔️ free --mega → The ‘free’ command displays the total amount of RAM and how much you spent. The flag --mega is used to display it in megabytes.

↔️ uname -a → Displays the SO architecture and the kernel version.

↔️ vmstat → The 'vmstat' command displays system statistics, allowing you to get a general overview of processes, memory usage, CPU activity, system status, etc.

↔️ ss → Used to dump socket statistics and for monitoring network connections.

↔️ hostname → Used to obtain DNS and set the NIS or the name of the host.
This name is given to the computer and attached to the network. Using the -I flag gives the IP address.


## 10 _Crontab_ ⏰


➤ Crontab is a daemon used for automating tasks. We can set the time in the file: "sudo crontab -e"

↔️ m → Minute [Every 10 minutes → */10, every minute *]

↔️ h → Hour

↔️ dom → Day of the month

↔️ mon → Month of the year

↔️ dow → Day of the week

↔️ command → Where the command will be typed


## 11- _Bonus - WordPress_ ⭐

➤ I also did the bonus parte which was about creating a wordpress using the following software: Lighttpd (Web Server), MariaDB (Database), PHP (programming language used to develop dynamic web apps and interactive websites).

➤ There was also a second bonus which was about adding an additional service.
I’ve chosen LiteSpeed which is a web server software (like Lighttpd).

➤ Here are all the steps that I followed: 

### 11-2 Lighttpd

➤ Lighttpd is a web server designed to be fast, secure, flexible, and standards compliant. 
➤ It is optimized for environments where speed is very important. 
➤ This is because it consumes less CPU and RAM than other servers.

#### Installation

➤ First of all we install the Lighttpd packages.

	sudo apt install lighttpd

➤ We allow connections via UFW to a new port.

	sudo ufw allow port_id


### 11-3 MariaDB

➤ MariaDB is a database. It is used for a variety of purposes, such as data warehousing, e-commerce, enterprise-level functions and logging applications.

➤ Install the MariaDB packages.

	sudo apt install mariadb-server

➤ Because the default configuration is not very secure we use a script that restricts access to the server and removes unused accounts.

➤ The script:

	sudo mysql_secure_installationReply
	
 And the replies are:
  	
   	Switch to unix_socket autentication? → N
	Change the root password? → N
	Remove anonymous users? → Y
	Disallow root login remotely? → Y
	Remove test database and acces to it? → Y
	Reaload privilege tables now? → Y
 
➤ Once the installation is finished we will create the database and the user for wordpress
➤ To enter mariadb we put → mariadb
➤ We create a database for the WordPress

	CREATE DATABASE databasename;
	SHOW DATABASE to see the databases;
➤ We create a user inside the database.

	CREATE USER 'username'@'localhost' IDENTIFIED BY '12345';

➤ Bind the user to the database to give him the necessary permissions to work

	GRANT ALL PRIVILEGES ON databasename.* TO 'username'@'localhost';
➤ We update the permissions to take effect

	FLUSH PRIVILEGES;


### 11-4 PHP

➤ PHP is a programming language. It is used to develop dynamic web applications and interactive websites.

➤ PHP runs on the server side.

#### Installation

➤ We install the PHP packages

	sudo apt install php-cgi php-mysql


### 11-5 WordPress

➤ WordPress is a content management system focused on the creation of any type of web page.

#### Installation

➤ We install 'wget' and 'zip'

	sudo apt install wget zip

↔️ wget → Used to download files from the web.
↔️ zip → Used to compress and decompress zip compressed files.

➤ We go to the "/var/www" folder and download the latest version of wordpress and unzip it

	sudo wget https://es.wordpress.org/latest-es_ES.zip
	sudo unzip latest-es_EN.zip

➤ Rename the folders from html to html_old and from wordpress to html.

➤ We change permissions to the new html folder

	chmod -R 755 html

### 11-6 WordPress Configuration

➤ Access the "/var/www/html" directory.

➤ Copy the file 'wp-config-sample.php' and rename it wp-config.php and in that file modify:

	DATABASE NAME
	USERNAME
	PASSWORD

➤ Enable the fastcgi-php module in Lighttpd to improve the performance and speed of web applications.

	sudo lighty-enable-mod fastcgi

➤ We enable the same module but for PHP.

	sudo lighty-enable-mod fastcgi-php

➤ We update and apply the changes in the configuration.

	sudo service lighttpd force-reload

➤ We go to the browser and enter our IP in the search engine.

✅ With this we will have the website ready ✅


### 11-7 OpenLiteSpeed

#### What is OpenLiteSpeed?
➤ LiteSpeed Web Server is the leading high-performance, high-scalability web server

#### Installation
➤ We install LiteSpeed from the repository.

	wget -O - https://repo.litespeed.sh | sudo bash

➤ Run the following commands to make sure.

	sudo apt update

➤ Install LiteSpeed.

	sudo apt install openlitespeed

➤ Change the password to a more secure one. In this file: sudo /usr/local/lsws/admin/misc/admpass.sh

➤ Configure the firewall to allow connections on ports 8088/tcp and 7080/tcp.

	sudo ufw allow 8088/tcp
	sudo ufw allow 7080/tcp
	sudo ufw reload

➤To access LiteSpeed we put in the browser 'IP:port'

==========================================================================================

✅ Well, that's all ✅

➤ At first, i though this project was going to be boring and tedious but contrary to what I thought it has been quite an interesting project.

➤This is what I've learnt in this beautiful project :)

***Most part of the theorical content has been obtained from the next guide: [https://github.com/gemartin99/Born2beroot-Tutorial/tree/main]


### - Check my profile on the intra of 42 school ↙️
[HERE]([https://profile.intra.42.fr/users/rcortes-])
