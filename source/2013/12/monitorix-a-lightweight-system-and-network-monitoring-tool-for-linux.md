#Monitorix 3.4.0 Released – A Lightweight System and Network Monitoring Tool for Linux

Monitorix is an open source, free and most powerful lightweight tool designed to monitor system and network resources in Linux. It regularly collects system and network data and display the information in graphs using its own web interface. Monitorix allows to monitor overall system performance and also help in detecting bottlenecks, failures, unwanted long response times and other abnormal activities.

It is written in Perl language and licensed under the terms of GNU (General Public License) as published by the FSP (Free Software Foundation). It uses RRDtool to generate graphs and display them using web interface.

This tool is specifically created for monitoring Red Hat, CentOS, Fedora based Linux systems, but today it runs on many different flavors of GNU/Linux distributions and even it runs on UNIX systems like OpenBSD, NetBSD and FreeBSD.

The development of Monitorix is currently in active state and adding new features, new graphs, new updates and fixing bugs to offer a great tool for Linux system/network administration.

##Monitorix Features

* System load average, active processes, per-processor kernel usage, global kernel usage and memory allocation.
* Monitors Disk drive temperatures and health.
* Filesystem usage and I/O activity of filesystems.
* Network traffic usage up to 10 network devices.
* System services including SSH, FTP, Vsftpd, ProFTP, SMTP, POP3, IMAP, POP3, VirusMail and Spam.
* MTA Mail statistics including input and output connections.
* Network port traffic including TCP, UDP, etc.
* FTP statistics with log file formats of FTP servers.
* Apache statistics of local or remote servers.
* MySQL statistics of local or remote servers.
* Squid Proxy Web Cache statistics.
* Fail2ban statistics.
* Monitor remote servers (Multihost).
* Ability to view statistics in graphs or in plain text tables per day, week, month or year.
* Ability to zoom graphs for better view.
* Ability to define the number of graphs per row.
* Built-in HTTP server.

For a full list of new features and updates, please check out the official [feature page](http://www.monitorix.org/features.html).

##Installing Monitorix on a RHEL/CentOS/Fedora Linux
First, install following required packages.
```Shell
#yum install rrdtool rrdtool-perl perl-libwww-perl perl-MailTools perl-MIME-Lite perl-CGI perl-DBI perl-XML-Simple perl-Config-General perl-HTTP-Server-Simple wget
```
If in case yum fails to installing one or more of above packages, then you could enable following additional repositories to install them.

* [Enable EPEL repository](http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/)
* [Enable RPMforge repository](http://www.tecmint.com/install-and-enable-rpmforge-repository-in-rhel-centos-6-5-4/)

Next, download the latest version of 'Monitorix' package using wget command.
```Shell
#wget http://www.monitorix.org/monitorix-3.4.0-1.noarch.rpm
```

Once successfully downloaded, install it using the rpm command.
```Shell
#rpm -ivh monitorix-3.4.0-1.noarch.rpm
Preparing...                ########################################### [100%]
   1:monitorix              ########################################### [100%]
```
Once successfully installed, please have a look at the main configuration file ‘/etc/monitorix.conf‘ to add some extra settings according to your system and enable or disable graphs.

Finally, add Monitorix service to system start-up and start the service with following commands.
```Shell
#chkconfig --level 35 monitorix on
#service monitorix start
```
Once, you’ve started service, the program will start collecting system information according to configuration set in ‘/etc/monitorix.conf‘ file, and after few minutes you will start seeing system graphs from your browser at.
```Shell
http://localhost:8080/monitorix/
```

If you have SELinux in enabled state, then graphs are not visible and you will get tons of error messages in ‘/var/log/messages‘ or ‘/var/log/audit/audit.log‘ file about access denied to RRD database files. To get rid of such errors messages and visible graphs, you need to disable SELinux.
To Turn Off SELinux, simple changing the line “enforcing” to “disabled” in ‘/etc/selinux/config’ file.
```Shell
SELINUX=disabled
```
The above will disable SELinux temporarily, until you reboot the machine. If you want the system to start in always disable mode, you need to reboot the system.

##Installing Monitorix on a Ubuntu/Debian/Linux Mint
The Monitorix installation can be done in two-ways, using Izzy repository for automatic installation/updates and another using manually download and install .deb package.

The Izzy repository is an experimental repository but the packages from this repository should work on all versions of Ubuntu, Debian, etc. However, no warranties are given – So, the risk is all yours. If you still want to add this repository for automatic updates via apt-get, simply follow the steps provided below for automatic installation.

######Automatic Installation Using Izzy Repository

Add the following line to your ‘/etc/apt/sources.list’ file.
```Shell
deb http://apt.izzysoft.de/ubuntu generic universe
```
Get GPG key for this repository, you can get it using wget command.
```Shell
#wget http://apt.izzysoft.de/izzysoft.asc
```
Once downloaded, add this GPG key to apt configuration by using the command ‘apt-key‘ as shown below.
```Shell
#apt-key add izzysoft.asc
```
Finally, install the package via the repository.
```Shell
#apt-get update
#apt-get install monitorix
```

######Manual Installation Using .Deb Package
Manually, downloading latest version of .deb package and install it with taking care of required dependencies as shown below.
```Shell
#apt-get update
#apt-get install rrdtool perl libwww-perl libmailtools-perl libmime-lite-perl librrds-perl libdbi-perl libxml-simple-perl
#wget http://www.monitorix.org/monitorix_3.4.0-izzy1_all.deb
#dpkg -i monitorix_3.4.0-izzy1_all.deb
```
During installation, a web server configuration takes place. So, you need to reload the Apache web server to reflect new configuration.
```Shell
#service apache2 reload
```
Monitorix comes with a default configuration, if you wish to change or adjust some settings take a look at the configuration file at ‘/etc/monitorix.conf‘. Once you’ve done changes reload the service for new configuration to take effect.
```Shell
#service monitorix restart
```

Now point your browser to ‘http://localhost/monitorix/‘ and start watching graphs of your system. It can be accessed from localhost only, if you wish to allow access to remote IP’s. Simply open the ‘/etc/apache2/conf.d/monitorix.conf‘ file and add IP’s to the ‘Allow from‘ clause. For example see below.
```Shell
<Directory /usr/share/monitorix/cgi-bin/>
        DirectoryIndex monitorix.cgi
        Options ExecCGI
        Order Deny,Allow
        Deny from all
        Allow from 172.16.16.25
</Directory>
```
After you made changes to above configuration, do not forget to restart Apache.
```Shell
# service apache2 reload
```

##Monitorix Screenshots
Please check out the following are some screenshots.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-1.png'>

Monitorix Web Interface

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-2-620x223.png'>

System load average, active processes and memory allocation.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-3-620x249.png'>

Global kernel usage

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-4-592x450.png'>

Per-processor kernel usage.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-5-620x240.png'>

Disk drive temperatures and health.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-6-620x275.png'>

Filesystem usage and I/O activity.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-7-620x223.png'>

eth0 interface traffic

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-8-620x240.png'>

System services demand

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-9.png'>

Network Port Traffic

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-10-620x222.png'>

Apache Statistics

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monitorix-11.png'>

MySQL Statistics

##Reference Links:
[Monitorix Homepage](http://www.monitorix.org/)
[Monitorix Documentation](http://www.monitorix.org/documentation.html)

英文原文:[tecmint](http://www.tecmint.com/monitorix-a-lightweight-system-and-network-monitoring-tool-for-linux/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
