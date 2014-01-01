#为RHEL CentOS和Fedora安装HTOP（Linux进程监控）

我们在前面的一系列系统监控文章中，介绍了iotop的（监控linux的磁盘I/O）工具，今天给大家讲解的是，安装在CentOS6.3机器上的一个 系统进程监视工具，它叫HTOP;让我们来看看它是如何工作的吧。它可以正常的在RedHat/Fedora运行。可以这么说htop是Unix/Linux top命令的替代工具。我已经安装它了，非常高兴与大家分享，如果你有什么好使用经验，你可以通过留言与我们分享您的使用经验。现在开始安装使用htop。

##什么是htop?

HTOP是一个实时互动的监控工具，主要应用在通用的Linux版本下。它可以列出正在运行的进程的列表，而且易于使用。针对用惯了鼠标的小伙伴，我们可以用鼠标进行互动。您可以垂直滚动，来查看完整 的进程列表，以及水平滚动来查看进程的完整命令行。

#为RHEL，CentOS的和Fedora安装HTOP

让我们来配置yum源来安装吧，rpmforge的安装包库在RHEL6.3/6.2/6.1/6/5.8，CentOS的6.3/6.2/6.1/6/5.8和Fedora17,16,15,14,13,12是可以使用的.Linux下安装HTOP需要根据你系统版本来选中对应版 本。下面是针对32位或64位的安装方法。

For RHEL, CentOS & Fedora 32-bit OS

```Shell
##For RHEL 5, CentOS 5 & Fedora ##
#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm
#rpm -ihv rpmforge-release*.rf.i386.rpm
```
```Shell
## For RHEL 6 and CentOS 6
#wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm
#rpm -ihv rpmforge-release*.rf.i686.rpm
```

For RHEL, CentOS & Fedora 64-bit OS
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

一旦RPMForge软件库安装。现在开始安装使用yum命令。
```Shell
#yum install htop
```Shell

Now run the htop monitoring tool by executing following command on the terminal.
```Shell
#htop
```
##htop的三个主要部分:

* 顶部,在这里我们可以看到如CPU，内存，交换信息，也显示了任务，平均负载和正常运行时间。
* 进程的排序（根据CPU利用率）。
* 底部显示如帮助，设置，kill，nice，退出等不同的选项。

<img src='http://img01.21ops.com/images/2013/12/31/22b6b6ab8838681f54143eebc3bdea9c.jpeg'>
 
                   HTOP进程查看器

按F2或S设置菜单–>有四列，即设置，左栏，右栏和可用meters。

<img src='http://img01.21ops.com/images/2013/12/31/1bcf2a7b5a07a7cbb49ca02d2931cea7.jpeg'>
 
HTOP进程查看器仪表
键入tree或t显示进程树视图。

<img src='http://img01.21ops.com/images/2013/12/31/2fe21d6beed53afc2ef5acb594e861a2.jpeg'>
 
HTOP树进程查看器

大家可以参考页脚功能键使用漂亮的htop应用。然而，我们建议你使用的字符键，而不是功能键或快捷键，因为它可能会被其他程序占用了。
 
##HTOP快捷键和功能键

一些快捷键和功能键来实现互动。

<img src='http://img01.21ops.com/images/2013/12/31/b1167ecb6e20256c9c3c23a0fd29a9b9.png'>

HTOP命令快捷键和按键


英文原文:[tecmint](http://www.tecmint.com/install-htop-linux-process-monitoring-for-rhel-centos-fedora/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
