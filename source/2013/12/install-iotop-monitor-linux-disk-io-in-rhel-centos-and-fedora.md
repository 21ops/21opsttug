#Install Iotop (Monitor Linux Disk I/O) in RHEL, CentOS and Fedora

We are bringing you all a nice monitoring tool called Iotop, which is much similar to Linux familiar Top command that we used to monitor server processes and usage. In this article we will show how to install Iotop monitoring utility in RHEL 6.3/6.2/6.1/6/5.8, CentOS 6.3/6.2/6.1/6/5.8 and Fedora 17,16,15,14,13,12using yum command.

##What Is Iotop?
Iotop is an open source and free utility like Linux UI based Top command that used to monitor the Disk I/O and to trace the exact process or high used user disk read/writes. Iotop tool is based on Python programming requires Kernel accounting function to monitor and display processes. It can be very useful tool for system administrator to trace the specific process that may causing a disk I/O.

##Iotop Pre-requisites
* Kernel 2.6.18
* Python 2.4 with ctypes module

> Install Iotop (Monitor Linux Disk I/O) in RHEL 6.3/6.2/6.1/6/5.8, CentOS 6.3/6.2/6.1/6/5.8 and Fedora 17,16,15,14,13,12

##Installing Iotop in RHEL, CentOS and Fedora

##Step 1: Installing Iotop Pre-requisites
As I already said above that Iotop requires latest Kernel 2.6.18 and Python 2.4 with ctypes module, let’s first update Linux Kernel with the help of following command.

```Shell
#yum update kernel
```

Then you need to update Python with ctypes module for iotop package.
```Shell
#yum install python python-ctypes
```

##Step 2: Installing Iotop
To install iotop use the following yum command to install it on RHEL, CentOS and Fedora.
```Shell
#yum install iotop
```
##Step 3: Running Iotop
To run the iotop command, use the following command as root user.
```Shell
#iotop
Example Output

<img src='http://www.tecmint.com/wp-content/uploads/2012/07/iotop-Screen.jpg'>

Iotop Monitoring Command Preview

I recommend you all that start using iotop with -o or –only option to see all the running processes or threads actually doing I/O, instead of watching all processes or threads.
```Shell
#iotop --only
```
<img src='http://www.tecmint.com/wp-content/uploads/2012/07/iotop-Screen-1.jpg'>

Iotop Disk I/O Monitoring Preview

##Step 4: Iotop Usage
To list all the usage and options of iotop command, run the following command to check the man pages.
``Shell
#man iotop
```
Some important iotop usage and keyboard shortcuts.

* Move left or right arrow key to change the sorting.
* Use –version option to see version number and exit.
* Use -h option to see information of usage.
* Use -r option to reverse the sorting order.
* Use -o option to check processes or thread.
* Use -b option to Turn On non-interactive mode to enable logging I/O usage.
* Use -p PID to list all processes/threads to monitor.
* Use -u USER option to list all the users to monitor.
* Use -P option to list only processes. Normally iotop displays all threads.
* Use -a option to check accumulated I/O instead of bandwidth.

All the above iotop options are fairly straightforward. The interface almost looks and functions exactly same as Linux top command, So if you are a already familiar with its usage, then iotop will be a much simpler than top.

英文原文:[tecmint](http://www.tecmint.com/install-iotop-monitor-linux-disk-io-in-rhel-centos-and-fedora/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
