#linux下限制shell:rssh和scponly

限制shell正如,[rsh](http://www.pizzashack.org/rssh/)和[scponly](https://github.com/scponly/scponly/wiki/)让系统管理员限制linux用户可以做哪些操作，例如，你可以创建用户，并允许通过[scp](http://en.wikipedia.org/wiki/Secure_copy)复制文件，但不会被允许登录到系统的命令行。这是非常重要的安全功能，应考虑每个系统管理员用户，以防止未经授权的活动，例如通过SSH。

如果你有一些在线存储，用于上传超过SCP/SSH或rsync从远程主机的备份数据，那么，强烈建议使用限制这些传入的连接，并确保即使攻击者得到了用户名/密码（或密钥），那么他（或她）也将无法打入您的系统。

scponly是极其简单的受限shell，用户帐户具有scponly的二进制的壳,将无法做任何事情（数据从远程主机通过scp协议或通过[rsync/ scp](http://troy.jdmz.net/rsync/index.html)的除外）。 RSSH提供多一点的功能：您可以限制用户使用选定的协议，如SCP，SFTP，rsync的，CVS或rdist的chroot环境。

安装：
我更喜欢使用yum或aptitude来安装这类软件像RSSH或scponly的，最快的方法就是尝试以下其中一项命令，根据您的需要：

```Shell
apt-get install rssh
apt-get install scponly
yum install rssh
yum install scponly
```
如果有问题，在你的Linux发行版的信息库中找到所需的受限shell，然后你应该下载源代码，并做一些操作。./configure时，和make install。这里是链接：latest rssh .tar.gz, latest scponly .tgz.

配置:
scponly的，不需要任何配置，所以你就应该将其设置为一个shell的用户帐户。下面是一些例子。
用scponly创建一个新的账号:
```Shell
useradd -s /usr/sbin/scponly user1
```
用该用户账号用rssh作为shell

```Shell
usermod -s /usr/sbin/rssh user2
```
/usr/sbin/scponly是scponly的二进制可执行文件。
 
RSSH文本配置文件通常存储在/etc/rssh.conf中的。您可以设置每个用户的设置或配置全局限制使用RSSH所有账目。默认rssh.conf文件有很好的注释，所以不应该有任何问题，你需要配置RSSH。在同一时间，在这里有一些例子。
 
如果你想限制所有用户scp和rsync，应该取消注释在rssh.conf行，想下面这样：
 
```Shell
allowscp
#allowsftp
#allowcvs
#allowrdist
allowrsync
```
现在看下每个用户的例子。允许用户得到的是仅使用scp协议，对以下符合在rssh.conf将做到这一点：
```Shell
user=sbk:022:00001:
```
允许用户ann只可以scp和rsync:
```Shell
user=sbk:022:10001:
```
正如你可以看到每个用户设置启用的协议指定为11000（SCP，SFTP），11111（SCP，SFTP，CVS，rdist的，rsync等）或00000（无协议启用）。在上面的例子中指定的umask022。

测试:
让我们假设你已经创建user1和只有scp和rsync的使用RSSH启用。尝试访问user1的帐号下的SSH服务器，看下下面的测试输出：

```Shell
artiomix$ ssh user1@1.2.3.4
user1@1.2.3.4's password: 
 
This account is restricted by rssh.
Allowed commands: scp rsync
 
If you believe this is in error, please contact your system administrator.
Connection to 1.2.3.4 closed.
```

与此同时SCP过户工作没有问题：
```Shell
artiomix$ scp -P 23451 /etc/test.file user1@1.2.3.4:/tmp
user1@1.2.3.4's password:
test.file                             100%  983     1.0KB/s   00:00
```
进一步阅读：
rssh支持chroot环境对于rsync、rsync和其他的传输协议。这意味着你不仅可以限制用户通过命令，他们也可以使用他们到达的文件系统。例如，user1可以可以chroot/chroot_user1，所以它不能被用来复制的东西从/etc目录的服务器或/var/www下面。这里有一个chroot在RSSH中文章，是不错的手册。

英文原文:[linuxscrew](http://www.linuxscrew.com/2012/07/05/linux-restricted-shells-rssh-and-scponly/) 翻译者:[新世纪linux社区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
