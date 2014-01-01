#RHEL CentOS and Fedora下安装iotop的（监控Linux的磁盘I/O）

我们正在给你介绍一个很好的监控工具，称为iotop，这个命令类似于linux下用来监控服务器进程和使用熟悉的top命令。在这篇文章中我们将介绍如何使用yum命令来安装在RHEL6.3/6.2/6.1/6/5.8，CentOS的6.3/6.2/6.1/6/5.8和Fedora17,16,15,14,13,12 iotop的监视工具。

##什么是Iotop?

iotop的是一个开源和免费的实用工具，用来监视磁盘I/O和追查准确的过程或高使用的用户的磁盘读/写Linux,用户界面基于top命令。 iotop的工具是基于Python编程需要内核计费功能，以监测和显示的过程。作为系统管理员能够跟踪，可能会导致磁盘I/O的具体过程，iotop则是非常有用的工具。

##Iotop环境要求:

* Kernel 2.6.18
* Python 2.4 with ctypes module

> 安装iotop的（监控Linux的磁盘I/O)的6.3/6.2/6.1/6/5.8 RHEL，CentOS的和Fedora6.3/6.2/6.1/6/5.817,16,15,14,13,12

##RHEL CentOS and Fedora下安装iotop

##步骤1：安装iotop的先决条件

正如我已经说过上面的iotop的需要最新的内核2.6.18和Python2.4与ctypes的模块，让我们第一次更新的Linux内核使用下面的命令的帮助。
```Shell
#yum update kernel
```
然后，你需要与iotop工具包的ctypes模块更新的Python。

```Shell
#yum install python python-ctypes
```

##步骤2：安装iotop的
```shell
#yum install iotop
```

##第3步：运行iotop的

要运行iotop的命令，请使用以下命令以root用户。
```Shell
# iotop
```
例子:

<img src='http://img01.21ops.com/images/2014/1/1/iotop-Screen1.jpg'>

iotop的监控命令预览

我建议大家，开始使用iotop的使用-o或-only选项来查看所有正在运行的进程或线程实，而不是看所有的进程或线程/O。

```Shell
#iotop --only
```
<img src='http://img01.21ops.com/images/2014/1/1/iotop-Screen-2.jpg'>


iotop的磁盘I/ O监控预览

##步骤4：iotop用法:

列出所有使用和iotop的命令选项，请运行以下命令来检查手册页。

```Shell
# man iotop
```

下面是一些重要的iotop的使用和键盘快捷键。
* 向左或向右箭头键来改变排序。
* 使用-version选项查看版本号并退出。
* 使用-h选项，看看使用情况的信息。
* 使用-r选项反向排序。
* 使用-o选项来检查进程或线程。
* 使用-b选项来开启非交互模式下启用日志I/O使用。
* 可使用-p PID来列出所有的进程/线程来监视。
* 使用-u用户选项列出所有的用户进行监控。
* 使用-P选项仅列出进程。通常iotop的显示所有线程。
* 使用-a选项来检查，而不是带宽积累的I/O。

上述所有iotop的选项是相当简单的。界面几乎和Linux top命令的外观和功能完全一样的，所以如果你是一个已经熟悉了它的用法，然后iotop的会比顶部要简单得多。

英文原文:[tecmint](http://www.tecmint.com/install-iotop-monitor-linux-disk-io-in-rhel-centos-and-fedora/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
