#Install IfTop (Bandwidth Monitoring) Tool in RHEL / CentOS / Fedora

In our earlier article, we reviewed the usage of TOP Command and it’s parameters. In this article we have came up with another excellent program called Interface TOP (IFTOP) is a real time network bandwidth monitoring tool through Command line. It will show a quick overview of network activities. In a TOP command you can see percentage usage of CPU, Memory and SWAP in real time. But IFTOP shows a real time updated list of network connections based on their network usage ordered on every 2, 10 and 40 seconds average. In this post we are going to see the installation and how to use IFTOP with examples.

##FTOP Pre-requisite
* libpcap : module provides a user-level network packet capture information and statistics.
* libncurses : is a API programming library that enables programmers to provide text-based interfaces in a terminal.

##Install libpcap and libncurses
Installation of the libpcap and libncurses library with YUM command as shown below for error-free iftop installation.
```Shell
#yum -y install libpcap libpcap-devel ncurses ncurses-devel
```
##Download and Install IFTOP
Download iftop from it’s website with Wget command as shown below.

```Shell
#wget http://www.ex-parrot.com/pdw/iftop/download/iftop-0.17.tar.gz
```

Follow the below all commands to install iftop.
```Shell
#tar -zxvf iftop-0.17.tar.gz
#cd iftop-0.17
#./configure
#make
#make install
```
##Basic usage of Iftop
Once installation done, go to your console and type iftop command.
```Shell
#iftop
```
Sample output of iftop command which shows bandwidth of default interface as shown below.

<img src='http://www.tecmint.com/wp-content/uploads/2012/10/iftop.png'>

iftop screenshot

##Monitoring Specific Interface
You can give a specific interface to monitor with -i option.
```Shell
#iftop -i eth0
```
<img src='http://www.tecmint.com/wp-content/uploads/2012/10/iftop-eth0.png'>

iftop eth0 command Screenshot

##Iftop Options and Usage

While running iftop you can use the keys like S, D to see more information like source, destination etc. Please do man iftop if you want to explore more options and tricks. Press ‘q‘ to quit from running windows.

In this article we have seen how to install and usage of iftop. if you want to know more about it please visit [iftop website](http://www.ex-parrot.com/pdw/iftop/download/). Kindly share it and send your comment through our comment box below.

英文原文:[tecmint](http://www.tecmint.com/install-iftop-bandwidth-monitoring-tool-in-rhel-centos-fedora/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
