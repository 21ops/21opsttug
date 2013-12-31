#Real Time Interactive IP LAN Monitoring with IPTraf Tool

There are number of monitoring tools available. Moreover, i came across a IPTraf monitoring tool which i find very useful and it’s a simple tool to monitor Inbound and Outbound network traffic passing through interface.

IPTraf is an ncurses-based IP LAN monitoring tool (text-based) wherein we can monitor various connections like TCP, UDP, ICMP, non-IP counts and also Ethernet load information etc.

This article guides you on how to install IPTraf monitoring tool using YUM command.

##Installing IPTraf
IPTraf is part of the Linux distribution and can be installed on RHEL, CentOS and Fedora server’s using yum command from terminal.
```Shell
#yum install iptraf
```
Under Ubuntu, iptraf can be installed using Ubuntu Software Center or ‘apt-get’ method. For example, use the ‘apt-get‘ command to install it.
```Shell
$sudo apt-get install iptraf
```

##IPTraf Usage
Once IPTraf installed, run the following command from the terminal to launch an ascii based menu interface that will allow you to view current IP traffic monitoring, General interface statistics, Detailed interface statistics, Statistical breakdowns, Filters and also provide some configure options where you can configure as per your need.
```Shell
[root@tecmint ~]# iptraf
```
<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf.png'>

IPTraf Startup Screen

The iptraf interactive screen, displays a menu system with different options to choose from. Here are the some screenshots that shows real time IP traffic counts and interface statistics etc.

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf1.png'>

IPTraf System Menu

##IP traffic monitor

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf2.png'>

IP Traffic Monitor

##General interface statistics

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf3.png'>

IPTraf General interface statistics

##Detailed interface statistics

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf5.png'>

IPTraf Detailed interface statistics

##Statistical breakdowns

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf51.png'>

IPTraf Statistical breakdowns

##LAN station monitor

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf6.png'>

IPTraf LAN station monitor

##Configure

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf7.png'>

IPTraf Configure

##IPTraf Options

Using "iptraf -i" will immediately start the IP traffic monitor on a particular interface. For example, the following command will start the IP traffic on interface eth0. This is the primary interface card that attached to your system. Else you can also monitor all your network interface traffic using argument as “iptraf -i all“.
```Shell
#iptraf -i eth0
```

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf8.png'>

IPTraf Eth0 Monitoring

Similarly, you can also monitor TCP/UDP traffic on a specific interface, using the following command.
```Shell
#iptraf -s eth0
```

<img src='http://www.tecmint.com/wp-content/uploads/2013/02/IPTraf9.png'>

IPTraf TCP/UDP Monitoring

If you want to know more options and how to use them, check iptraf ‘man page‘ or use the command as ‘iptraf -help‘ for more parameters. Fore more information visit the official project page.

英文原文:[tecmint](http://www.tecmint.com/real-time-interactive-ip-lan-monitoring-with-iptraf-tool/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
