#NetHogs – Monitor Per Process Network Bandwidth Usage in Real Time

Linux operating systems have tons of open source network monitoring tools on the web. Say, you can use iftop command to check bandwidth usage, netstat command to see reports on interface statistics or top command to watch running process on your system. But if you are really looking for something that can give you a real time statistics of your network bandwidth of per process usage, then NetHogs is the only utility you should look for.

<img src='http://www.tecmint.com/wp-content/uploads/2013/03/nethogs-3.jpg'>

NetHogs – Network Bandwidth Monitoring

##What is NetHogs?
NetHogs is an open source command line program (similar to Linux top command) that is used for monitor real time network traffic bandwidth used by each process or application.

From NetHogs Project Page

> NetHogs is a small ‘net top’ tool. Instead of breaking the traffic down per protocol or per subnet, like most tools do, it groups bandwidth by process. NetHogs does not rely on a special kernel module to be loaded. If there’s suddenly a lot of network traffic, you can fire up NetHogs and immediately see which PID is causing this. This makes it easy to identify programs that have gone wild and are suddenly taking up your bandwidth.

This article explains you on how to install and find out real time per process network bandwidth usage with nethogs utility under Unix/Linux operating systems.

##Install NetHogs in RHEL, CentOS and Fedora
To install nethogs, you must turn on EPEL repository under your Linux systems and then run the following yum command to download and install nethogs package.
```Shell
#yum install nethogs
######Sample Output
```Shell
[root@tecmint ~]# yum -y install nethogs

Loaded plugins: fastestmirror, refresh-packagekit
Loading mirror speeds from cached hostfile
 * base: mirrors.hns.net.in
 * epel: mirror.nus.edu.sg
 * extras: mirrors.hns.net.in
 * rpmfusion-free-updates: mirrors.ustc.edu.cn
 * rpmfusion-nonfree-updates: mirror.de.leaseweb.net
 * updates: mirrors.hns.net.in
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package nethogs.i686 0:0.8.0-1.el6 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

===========================================================================================================
 Package				Arch				Version					Repository					Size
===========================================================================================================
Installing:
 nethogs				i686				0.8.0-1.el6				epel						28 k

Transaction Summary
===========================================================================================================
Install       1 Package(s)

Total download size: 28 k
Installed size: 50 k
Downloading Packages:
nethogs-0.8.0-1.el6.i686.rpm														|  28 kB     00:00
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : nethogs-0.8.0-1.el6.i686                                                          1/1
  Verifying  : nethogs-0.8.0-1.el6.i686                                                          1/1

Installed:
  nethogs.i686 0:0.8.0-1.el6

Complete!

##Install NetHogs in Ubuntu, Linux Mint and Debian
To install nethogs, type the following apt-get command to install nethogs package.
```Shell
$sudo apt-get install nethogs

######Sample Output
tecmint@tecmint:~$ sudo apt-get install nethogs
[sudo] password for tecmint: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  nethogs
0 upgraded, 1 newly installed, 0 to remove and 318 not upgraded.
Need to get 27.1 kB of archives.
After this operation, 100 kB of additional disk space will be used.
Get:1 http://in.archive.ubuntu.com/ubuntu/ quantal/universe nethogs i386 0.8.0-1 [27.1 kB]
Fetched 27.1 kB in 1s (19.8 kB/s)  
Selecting previously unselected package nethogs.
(Reading database ... 216058 files and directories currently installed.)
Unpacking nethogs (from .../nethogs_0.8.0-1_i386.deb) ...
Processing triggers for man-db ...
Setting up nethogs (0.8.0-1) ...

##Using NetHogs Utility
To run the nethogs utility, type the following command under red-hat based systems.
```Shell
#nethogs
```
To execute it, you will must have root permissions, so run with sudo command as shown.
```Shell
$sudo nethogs
######Sample Previews:

<img src='http://www.tecmint.com/wp-content/uploads/2013/03/NetHogs1.png'>

NetHogs Preview on CentOS 6.3


<img src='http://www.tecmint.com/wp-content/uploads/2013/03/nethogs-2.jpg'>

NetHogs Preview on Ubuntu 12.10

As you see above the send and received lines show the amount of traffic being used by per process. The total sent and received usage of bandwidth calculated at the bottom. You can sort and change the order by using the interactive controls discussed below.

##NetHogs Command Line Options
Following are the nethogs command line options. Using ‘-d‘ to add a refresh rate and ‘device name‘ to monitor specific given device or devices bandwidth (default is eth0). For example, to set 5 seconds as your refresh rate, then type the command as.
```Shell
#nethogs -d 5
```
```Shell
$sudo nethogs -d 5
```
To monitor specific device (eth0) network bandwidth only, use the command as.
```Shell
#nethogs eth0
```
```Shell
$sudo nethogs eth0
```

To monitor network bandwidth of both eth0 and eth1 interfaces, type the following command.
```Shell
#nethogs eth0 eth1
```
```Shell
$sudo nethogs eth0 eth1
```
##Other Options and Usage
```Shell
-d : delay for refresh rate.
-h : display available commands usage.
-p : sniff in promiscious mode (not recommended).
-t : tracemode.
-V : prints Version info.
```
##NetHogs Interactive Controls
Following are some useful interactive controls (Keyboard Shortcuts) of nethogs program.
```Shell
-m : Change the units displayed for the bandwidth in units like KB/sec -> KB -> B-> MB.
-r : Sort by magnitude of respectively traffic.
-s : Sort by magnitude of sent traffic.
-q : Hit quit to the shell prompt.
```
For a full list of nethogs utility command line options, please check out the nethogs man pages by using command as ‘man nethogs‘ or ‘sudo man nethogs‘ from the terminal. For more information visit the Ne [Nethogs project](http://nethogs.sourceforge.net/) home page.

英文原文:[tecmint](http://www.tecmint.com/nethogs-monitor-per-process-network-bandwidth-usage-in-real-time/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)

