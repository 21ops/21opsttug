#Install Htop (Linux Process Monitoring) for RHEL, CentOS & Fedora

In our earlier series of system monitoring article where we explained about [Iotop (Monitor Linux Disk I/O)](http://www.tecmint.com/install-iotop-monitor-linux-disk-io-in-rhel-centos-and-fedora/) tool, now today we are so exciting to install another system process monitoring tool called Htop on our CentOS 6.3 box to see how it works. It should work on RedHat/Fedora as well. I had heard that htop is replacement of Unix/Linux Top command. I have installed it one of our box and became fond of it. You too can try it out and share your experience with us through comment.  Start installing htop and play with it.

##What is Htop?
Htop is an interactive and real time process monitoring application for Linux. It shows complete list of processes running and easy to use for normal tasks. We can interact with mouse those who love to play with mouse. You can scroll vertically to view the full process list, and scroll horizontally to view the full command line of the process.

##Install Htop for RHEL, CentOS & Fedora
Let us install Htop on RHEL 6.3/6.2/6.1/6/5.8, CentOS 6.3/6.2/6.1/6/5.8 and Fedora 17,16,15,14,13,12 Linux via the yum package manager, the rpmforge package repository must be installed on your system to retrieve and install. To do just install the following RPM for your architecture (32bit or 64bit).

> ##For RHEL, CentOS & Fedora 32-bit OS

```Shell
## For RHEL 5, CentOS 5 & Fedora ##

#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm
#rpm -ihv rpmforge-release*.rf.i386.rpm
```
```Shell
## For RHEL 6 and CentOS 6
#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm
#rpm -ihv rpmforge-release*.rf.i686.rpm
```

> ##For RHEL, CentOS & Fedora 64-bit OS

```Shell
## For RHEL 5, CentOS 5 & Fedora ##
#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm
#rpm -ihv rpmforge-release*.rf.x86_64.rpm 
```
```Shell
## For RHEL 6 and CentOS 6
#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
#rpm -ihv rpmforge-release*.rf.x86_64.rpm
```

Once RPMforge repository is installed. Now start installation with yum command.
```Shell
#yum install htop
```
Now run the htop monitoring tool by executing following command on the terminal.
```Shell
#htop
```

##Htop is having three sections mainly
* Header, where we can see info like CPU, Memory, Swap and also shows tasks, load average and Up-time.
* List of processes sorted by CPU utilization.
* Last footer shows different options like help, setup, kill, nice , quit etc.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/htop-3.jpg'>

Htop Process Viewer

Press F2 or S for setup menu > there are four columns i.e Setup, Left Column, Right Column and Available Meters.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/htop-4.jpg'>

Htop Process Viewer Meter

Type tree or t to display processes tree view.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/htop-5.jpg'>

Htop Tree Process Viewer

We can refer footer for function keys to use nifty htop application. However, we advise to use character keys or shortcut keys instead of function keys as it may have mapped with some other functions during secure connection.

##Htop Shortcut and Function Keys
Some of the shortcut and function keys and its functionality to interact with htop.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Htop-Shortcuts.png'>

Htop Command Shortcuts and Keys

英文原文:[tecmint](http://www.tecmint.com/install-htop-linux-process-monitoring-for-rhel-centos-fedora/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
