#How to Install and Setup Monit (Linux Process and Services Monitoring) Program

Monit is a free open source and very useful tool that automatically monitors and manages server process, files, directories, checksums, permissions, filesystems and services like Apache, Nginx, MySQL, FTP, SSH, Sendmail and so on in a UNIX/Linux based systems and provides an excellent and helpful monitoring functionality to system administrators.

The monit has user friendly web interface where you can directly view the system status and setup up processes using native HTTP(S) web server or via the command line interface. This means you must have web server like Apache or Nginx installed on your system to access and view monit web interface.

Read Also : [10 Linux Performance Monitoring Tools](http://www.tecmint.com/command-line-tools-to-monitor-linux-performance/)

##What Monit can do
Monit has a ability to start a process if it is not running, restart a process if not responding and stop a process if uses high resources. Additionally you can also use Monit to Monitor files, directories and filesystems for changes, checksum changes, file size changes or timestamp changes. With Monit you can able to monitor remote hosts TCP/IP port, server protocols and ping. Monit keeps its own log file and alerts about any critical error conditions and recovery status.

This article is written to describe a simple guide on Monit installation and configuration on a RHEL, CentOS, Fedora, Ubuntu, Linux Mint and Debian Linux Operating Systems, but it should be easily compatible to Scientific Linux as well.

##Step 1: Installing Monit
By default, Monit tool is not available from the system base repositories, you need to add and enable third party epel repository to install monit package under your RHEL/CentOS systems. Once you’ve added e[pel repository](http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/), install package by running the following yum command. For Ubuntu/Debian/Linux Mint user’s can easily install using apt-get command as shown.

######On RedHat/CentOS/Fedora/
```Shell
#yum install monit
```Shell
######On Ubuntu/Debian/Linux Mint
```Shell
$sudo apt-get install monit
```

##Step 2: Configuring Monit
Monit is very easy to configure, in fact the configuration files are created to be very easily readable and making them easier for users to understand. It is designed to monitor the running services in every 2 minutes and keeps the logs in “/var/log/monit“.

Monit has it’s web interface that runs on port 2812 using web server. To enable web interface you need to make changes in monit configuration file. The main configuration file of monit located at /etc/monit.conf under (RedHat/CentOS/Fedora) and /etc/monit/monitrc file for (Ubuntu/Debian/Linux Mint). Open this file using your choice of editor.
```Shell
# vi /etc/monit.conf
```
```Shell
$ sudo vi /etc/monit/monitrc
```

Next, uncomment the following section and add the IP address or domain name of your server, allow anyone to connect and change monit user and password or you can use default ones.
```Shell
 set httpd port 2812 and
     use address localhost  # only accept connection from localhost
     allow localhost        # allow localhost to connect to the server and
     allow admin:monit      # require user 'admin' with password 'monit'
     allow @monit           # allow users of group 'monit' to connect (rw)
     allow @users readonly  # allow users of group 'users' to connect readonly
```
Once you’ve configured it, you need to start the monit service to reload the new configuration settings.

```Shell
# /etc/init.d/monit start
```
```Shell
$ sudo /etc/init.d/monit start
```
Now, you will able to access the monit web interface by navigating to the “http://localhost:2812” or “http://example.com:2812“. Then enter user name as “admin” and password as “monit“. You should get screen similar to below.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monit-1.jpg'>

Monit Web Interface

##Step 3: Adding Monitoring Services
Once monit web interface correctly setup, start adding the programs that you want to monitor into the /etc/monit.conf under (RedHat/CentOS/Fedora) and /etc/monit/monitrc file for (Ubuntu/Debian/Linux Mint) at the bottom.

Following are some useful configuration examples for monit, that can be very helpful to see how a service is running, where it keeps its pidfile and how to start and stop a service etc.

######Apache
```Shell
check process httpd with pidfile /var/run/httpd.pid
group apache
start program = "/etc/init.d/httpd start"
stop program = "/etc/init.d/httpd stop"
if failed host 127.0.0.1 port 80
protocol http then restart
if 5 restarts within 5 cycles then timeout
```
######Apache2
```Shell
check process apache with pidfile /run/apache2.pid
start program = "/etc/init.d/apache2 start" with timeout 60 seconds
stop program  = "/etc/init.d/apache2 stop"
```
######Nginx
```Shell
check process nginx with pidfile /var/run/nginx.pid
start program = "/etc/init.d/nginx start"
stop program = "/etc/init.d/nginx stop"
```
######MySQL
```Shell
check process mysqld with pidfile /var/run/mysqld/mysqld.pid
group mysql
start program = "/etc/init.d/mysqld start"
stop program = "/etc/init.d/mysqld stop"
if failed host 127.0.0.1 port 3306 then restart
if 5 restarts within 5 cycles then timeout
```
######SSHD
```Shell
check process sshd with pidfile /var/run/sshd.pid
start program "/etc/init.d/sshd start"
stop program "/etc/init.d/sshd stop"
if failed host 127.0.0.1 port 22 protocol ssh then restart
if 5 restarts within 5 cycles then timeout
```
Once you’ve configured all programs for monitoring, check monit syntax for errors. If found any errors fix them, it’s not so tough to figure out what’s went wrong. When you get message like “Control file syntax OK“, or if you see no errors, you can proceed ahead.
```Shell
#monit -t
```
```Shell
$ sudo monit -t
```
After fixing all possible errors, you can type the following command to stat the monit service.
```Shell
#/etc/init.d/monit restart
```
```Shell
$ sudo /etc/init.d/monit restart
```
You can verify that monit service is started by checking log file.
```Shell
# tail -f /var/log/monit
```
```Shell
$ sudo tail -f /var/log/monit.log
```

######Sample Output
```Shell
[BDT Apr  3 03:06:04] info     : Starting monit HTTP server at [localhost:2812]
[BDT Apr  3 03:06:04] info     : monit HTTP server started
[BDT Apr  3 03:06:04] info     : 'tecmint.com' Monit started
[BDT Apr  3 03:06:04] error    : 'nginx' process is not running
[BDT Apr  3 03:06:04] info     : 'nginx' trying to restart
[BDT Apr  3 03:06:04] info     : 'nginx' start: /etc/init.d/nginx
```

######Monit Screenshot
This is how looks monit after adding all process for monitoring.

<img src='http://www.tecmint.com/wp-content/uploads/2013/04/Monit-2.jpg'>

Monit Monitoring All Process


英文原文:[tecmint](http://www.tecmint.com/how-to-install-and-setup-monit-linux-process-and-services-monitoring-program/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
