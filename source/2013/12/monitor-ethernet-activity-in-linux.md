#Arpwatch Tool to Monitor Ethernet Activity in Linux

Arpwatch is an open source computer software program that helps you to monitor Ethernet traffic activity (like Changing IP and MAC Addresses) on your network and maintains a database of ethernet/ip address pairings. It produces a log of noticed pairing of IP and MAC addresses information along with a timestamps, so you can carefully watch when the pairing activity appeared on the network. It also has the option to send reports via email to an network administrator when a pairing added or changed.

This tool is specially useful for Network administrators to keep a watch on ARP activity to detect ARP spoofing or unexpected IP/MAC addresses modifications.

##Installing Arpwatch in Linux
By default, Arpwatch tool is not installed on any Linux distributions. We must install it manually using ‘yum‘ command on RHEL, CentOS, Fedora and ‘apt-get‘ on Ubuntu, Linux Mint and Debian.
```Shell
#yum install arpwatch
```
```Shell
$sudo apt-get install arpwatch
```

Let’s focus on the some most important arpwatch files, the location of the files are slightly differ based on your operating system.
* /etc/rc.d/init.d/arpwatch : The arpwatch service for start or stop daemon.
* /etc/sysconfig/arpwatch : This is main configuration file…
* /usr/sbin/arpwatch : Binary command to starting and stopping tool via the terminal.
* /var/arpwatch/arp.dat : This is main database file where IP/MAC addresses are recorded.
* /var/log/messages : The log file, where arpwatch writes any changes or unusual activity to IP/MAC.

Type the following command to start the arpwatch service.
```Shell
#chkconfig --level 35 arpwatch on
#/etc/init.d/arpwatch start
```
```Shell
$sudo chkconfig --level 35 arpwatch on
$sudo /etc/init.d/arpwatch start
```
##Arpwatch Commands and Usage
To watch a specific interface, type the following command with ‘-i‘ and device name.
```Shell
#arpwatch -i eth0
```
So, whenever a new MAC is plugged or a particular IP is changing his MAC address on the network, you will notice syslog entries at ‘/var/log/syslog‘ or ‘/var/log/message‘ file.
```Shell
#tail -f /var/log/messages
```
##Sample Output
```Shell
Apr 15 12:45:17 tecmint arpwatch: new station 172.16.16.64 d0:67:e5:c:9:67
Apr 15 12:45:19 tecmint arpwatch: new station 172.16.25.86 0:d0:b7:23:72:45
Apr 15 12:45:19 tecmint arpwatch: new station 172.16.25.86 0:d0:b7:23:72:45
Apr 15 12:45:19 tecmint arpwatch: new station 172.16.25.86 0:d0:b7:23:72:45
Apr 15 12:45:19 tecmint arpwatch: new station 172.16.25.86 0:d0:b7:23:72:45
The above output displays new workstation. If any changes are made, you will get following output.
Apr 15 12:45:17 tecmint arpwatch: changed station 172.16.16.64 0:f0:b8:26:82:56 (d0:67:e5:c:9:67)
Apr 15 12:45:19 tecmint arpwatch: changed station 172.16.25.86 0:f0:b8:26:82:56 (0:d0:b7:23:72:45)
Apr 15 12:45:19 tecmint arpwatch: changed station 172.16.25.86 0:f0:b8:26:82:56 (0:d0:b7:23:72:45)
Apr 15 12:45:19 tecmint arpwatch: changed station 172.16.25.86 0:f0:b8:26:82:56 (0:d0:b7:23:72:45)
Apr 15 12:45:19 tecmint arpwatch: changed station 172.16.25.86 0:f0:b8:26:82:56 (0:d0:b7:23:72:45)
```

You can also check current ARP table, by using following command.
```Shell
#arp -a
```
##Sample Ouput
```Shell
tecmint.com (172.16.16.94) at 00:14:5e:67:26:1d [ether] on eth0
? (172.16.25.125) at b8:ac:6f:2e:57:b3 [ether] on eth0
```

If you want to send alerts to your custom email id, then open the main configuration file ‘/etc/sysconfig/arpwatch‘ and add the email as shown below.
```Shell
# -u <username> : defines with what user id arpwatch should run
# -e <email>    : the <email> where to send the reports
# -s <from>     : the <from>-address
OPTIONS="-u arpwatch -e tecmint@tecmint.com -s 'root (Arpwatch)'"
```

Here is an example of an email report, when a new MAC is connected on.
```Shell
        hostname: centos
      ip address: 172.16.16.25
       interface: eth0
ethernet address: 00:24:1d:76:e4:1d
 ethernet vendor: GIGA-BYTE TECHNOLOGY CO.,LTD.
       timestamp: Monday, April 15, 2012 15:32:29
```
Here is an example of an email report, when a IP changing his MAC address.
```Shell
            hostname: centos
          ip address: 172.16.16.25
           interface: eth0
    ethernet address: 00:56:1d:36:e6:fd
     ethernet vendor: GIGA-BYTE TECHNOLOGY CO.,LTD.
old ethernet address: 00:24:1d:76:e4:1d
           timestamp: Monday, April 15, 2012 15:43:45
  previous timestamp: Monday, April 15, 2012 15:32:29 
               delta: 9 minutes
```
As you can see above, it records, Hostname, IP address, MAC address, Vendor name and timestamps. For more information, see the arpwatch man page by hitting ‘man arpwatch’ on the terminal.

英文原文:[tecmint](http://www.tecmint.com/monitor-ethernet-activity-in-linux/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
