#Suricata 1.4.4 Released – A Network Intrusion Detection, Prevention and Security Monitoring System

Suricata is an open source high performance modern Network Intrusion Detection, Prevention and Security Monitoring System for Unix/Linux, FreeBSD and Windows based systems. It was developed and owned by a non-profit foundation the OISF (Open Information Security Foundation).

Recently, the OISF project team announced the release of Suricata 1.4.4 with minor but crucial updates and fixed some essential bugs over the previous release.

##Suricata Features

######IDS / IPS
Suricata is a rule-based Intrusion Detection and Prevention engine that make use of externally developed rules sets to monitor network traffic, as well as able to handle multiple gigabyte traffic and gives email alerts to the System/Network administrators.

######Multi-threading
Suricata provides speed and importance in network traffic determination. The engine is developed to apply the increased processing power offered by modern multi-core hardware chip sets.

######Automatic Protocol Detection
The engine not only provides keywords for TCP, UDP, ICMP and IP, but also has an built-in support for HTTP, FTP, TLS and SMB. A system administrator can able to create its own rule to detect a match within an HTTP stream. This is going to become different Malware detection and control.

######Fast IP Matching
The engine will certainly take rules that are IP matches based on the RBN and compromised IP lists at Emerging Threats and keep them into a specific fast matching preprocessor.

Read Also : [Install LMD – Linux Malware Detect in  Linux](http://www.tecmint.com/install-linux-malware-detect-lmd-in-rhel-centos-and-fedora/)

##Step :1 Installing Suricata in RHEL, CentOS and Fedora
You must use the Fedora’s EPEL repository to install some needed packages for i386 and x86_64 systems.

* Enable Fedora’s EPEL repository

Before you can compile and build Suricata for your system, install the following dependency packages that are required for further installation. The process may take a while to complete, depending on the internet speed.
```Shell
#yum -y install libpcap libpcap-devel libnet libnet-devel pcre \
pcre-devel gcc gcc-c++ automake autoconf libtool make libyaml \
libyaml-devel zlib zlib-devel libcap-ng libcap-ng-devel magic magic-devel file file-devel
```

######IPS Support
Next, build Suricata with IPS support. For this, we to need “libnfnetlink” and “libnetfilter_queue” packages, but these pre-built packages not available in the EPEL or CentOS Base repositories. So, we need to download and install rpms from the Emerging Threats CentOS repository.

######For 32-Bit
```Shell
#rpm -Uvh http://rules.emergingthreatspro.com/projects/emergingrepo/i386/libnetfilter_queue-0.0.15-1.i386.rpm \
http://rules.emergingthreatspro.com/projects/emergingrepo/i386/libnetfilter_queue-devel-0.0.15-1.i386.rpm \
http://rules.emergingthreatspro.com/projects/emergingrepo/i386/libnfnetlink-0.0.30-1.i386.rpm \ 
http://rules.emergingthreatspro.com/projects/emergingrepo/i386/libnfnetlink-devel-0.0.30-1.i386.rpm
```
######For 64-Bit
```Shell
#rpm -Uvh http://rules.emergingthreatspro.com/projects/emergingrepo/x86_64/libnetfilter_queue-0.0.15-1.x86_64.rpm \
http://rules.emergingthreatspro.com/projects/emergingrepo/x86_64/libnetfilter_queue-devel-0.0.15-1.x86_64.rpm \
http://rules.emergingthreatspro.com/projects/emergingrepo/x86_64/libnfnetlink-0.0.30-1.x86_64.rpm \ 
http://rules.emergingthreatspro.com/projects/emergingrepo/x86_64/libnfnetlink-devel-0.0.30-1.x86_64.rpm

######Download Suricata
Download latest Suricata source files and build it using the following commands.
```Shell
#cd /tmp
#wget http://www.openinfosecfoundation.org/download/suricata-1.4.4.tar.gz
#tar -xvzf suricata-1.4.4.tar.gz
#cd suricata-1.4.4
```

Now we use Suricata Auto Setup feature to automatically create all necessary directories, configuration files and latest rulesets.
```Shell
#./configure && make && make install-conf
#./configure && make && make install-rules
#./configure && make && make install-full
```Shell

##Step 2: Installing Suricata in Debian and Ubuntu
Before, beginning installation, you must have the following pre-requisites packages installed on the system to proceed further. Make sure you must be root user to run the following command. This installation process may take some time, depending on the current speed of your internet.
```Shell
#apt-get -y install libpcre3 libpcre3-dbg libpcre3-dev \
build-essential autoconf automake libtool libpcap-dev libnet1-dev \
libyaml-0-2 libyaml-dev zlib1g zlib1g-dev libmagic-dev libcap-ng-dev \
pkg-config magic file libhtp-dev
```

######IPS Support
By default, works as an IDS. If you want to add IDS support, install some needed packages as follows.
```Shell
#apt-get -y install libnetfilter-queue-dev libnetfilter-queue1 libnfnetlink-dev libnfnetlink0
```
######Download Suricata
Download latest Suricata tar-ball and build it using the following commands.
```Shell
#cd /tmp
#wget http://www.openinfosecfoundation.org/download/suricata-1.4.4.tar.gz
#tar -xvzf suricata-1.4.4.tar.gz
#cd suricata-1.4.4
```
Use Suricata Auto Setup option to create all needed directories, configuration files and rulesets automatically as shown below.
```Shell
#./configure && make && make install-conf
#./configure && make && make install-rules
#./configure && make && make install-full
```

##Step 3: Suricata Basic Setup
After downloading and installing Suricata, now its time to proceed to Basic Setup. Create following directorates.
```Shell
#mkdir /var/log/suricata
#mkdir /etc/suricata
```

The next part is to copy configuration files such as “classification.config“, “reference.config” and “suricata.yaml” from the base build installation directory.
```Shell
#cd /tmp/suricata-1.4.4
#cp classification.config /etc/suricata
#cp reference.config /etc/suricata
#cp suricata.yaml /etc/suricata
```
Finally, start the “Suricata Engine” first time and specify the interface device name of your preference. Instead of eth0, you can include the network card of your preference.
```Shell
#suricata -c /etc/suricata/suricata.yaml -i eth0
23/7/2013 -- 12:22:45 -  - This is Suricata version 1.4.4 RELEASE
23/7/2013 -- 12:22:45 -  - CPUs/cores online: 2
23/7/2013 -- 12:22:45 -  - Found an MTU of 1500 for 'eth0'
23/7/2013 -- 12:22:45 -  - allocated 2097152 bytes of memory for the defrag hash... 65536 buckets of size 32
23/7/2013 -- 12:22:45 -  - preallocated 65535 defrag trackers of size 104
23/7/2013 -- 12:22:45 -  - defrag memory usage: 8912792 bytes, maximum: 33554432
23/7/2013 -- 12:22:45 -  - AutoFP mode using default "Active Packets" flow load balancer
23/7/2013 -- 12:22:45 -  - preallocated 1024 packets. Total memory 3170304
23/7/2013 -- 12:22:45 -  - allocated 131072 bytes of memory for the host hash... 4096 buckets of size 32
23/7/2013 -- 12:22:45 -  - preallocated 1000 hosts of size 76
23/7/2013 -- 12:22:45 -  - host memory usage: 207072 bytes, maximum: 16777216
23/7/2013 -- 12:22:45 -  - allocated 2097152 bytes of memory for the flow hash... 65536 buckets of size 32
23/7/2013 -- 12:22:45 -  - preallocated 10000 flows of size 176
23/7/2013 -- 12:22:45 -  - flow memory usage: 3857152 bytes, maximum: 33554432
23/7/2013 -- 12:22:45 -  - IP reputation disabled
23/7/2013 -- 12:22:45 -  - using magic-file /usr/share/file/magic
```
After several minutes later, check the engine is correctly working and receives and inspects traffic.
```Shell
#cd /usr/local/var/log/suricata/
#ls -l
-rw-r--r-- 1 root root  25331 Jul 23 12:27 fast.log
drwxr-xr-x 2 root root   4096 Jul 23 11:34 files
-rw-r--r-- 1 root root  12345 Jul 23 11:37 http.log
-rw-r--r-- 1 root root 650978 Jul 23 12:27 stats.log
-rw-r--r-- 1 root root  22853 Jul 23 11:53 unified2.alert.1374557837
-rw-r--r-- 1 root root   2691 Jul 23 12:09 unified2.alert.1374559711
-rw-r--r-- 1 root root   2143 Jul 23 12:13 unified2.alert.1374559939
-rw-r--r-- 1 root root   6262 Jul 23 12:27 unified2.alert.1374560613
```
Watch “stats.log” file and make sure the displayed information is up-dated in real time.
```Shell
#tail -f stats.log
tcp.reassembly_memuse     | Detect                    | 0
tcp.reassembly_gap        | Detect                    | 0
detect.alert              | Detect                    | 27
flow_mgr.closed_pruned    | FlowManagerThread         | 3
flow_mgr.new_pruned       | FlowManagerThread         | 277
flow_mgr.est_pruned       | FlowManagerThread         | 0
flow.memuse               | FlowManagerThread         | 3870000
flow.spare                | FlowManagerThread         | 10000
flow.emerg_mode_entered   | FlowManagerThread         | 0
flow.emerg_mode_over      | FlowManagerThread         | 0
```

##Reference Links
[Suricata Homepage](http://suricata-ids.org/)
[Suricata User Guide](https://redmine.openinfosecfoundation.org/projects/suricata/wiki/Suricata_User_Guide)


英文原文:[tecmint](http://www.tecmint.com/suricata-a-network-intrusion-detection-prevention-system/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
