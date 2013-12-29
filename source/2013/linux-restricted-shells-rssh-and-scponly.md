#Linux Restricted Shells: rssh and scponly

Restricted shells like [rssh](http://www.pizzashack.org/rssh/) and [scponly](https://github.com/scponly/scponly/wiki/) give sysadmin the possibility to limit the operations that Linux user can do, for example you can create user that will be allowed to copy files via [scp](http://en.wikipedia.org/wiki/Secure_copy) but won’t be permitted to login into system’s command line. This is quite important security feature that should be considered by every sysadmin to prevent unauthorized activity by users for example over SSH.

If you have some online storage that is used for uploading backup data over scp or rsync/ssh from remote hosts then it is highly recommended to use restricted shells for those incoming connections and make sure that even if the attacker has got username/password (or key) then he (or she!) won’t be able to break into your system.

scponly is extremely simple restricted shell, user account that has scponly binary as its shell won’t be able to do anything except transfer data from remote host via scp protocol or via [rsync/scp](http://troy.jdmz.net/rsync/index.html). rssh provides little bit more features: you can limit users to use selected protocols like scp, sftp, rsync, cvs or rdist either in chroot environment or not.

Installation

I prefer using yum or aptitude to install such kind of software like rssh or scponly so the fastest way is to try one of below commands depending on your needs:

```Shell
apt-get install rssh
apt-get install scponly
yum install rssh
yum install scponly
```

If there are problems to find desired restricted shell in your Linux distro’s repository then you should download sources and do some ./configure, make and make install. Here are the links: latest rssh .tar.gz, latest scponly .tgz.

Configuration

scponly doesn’t need any configuration and works out of the box so you just should set it as a shell for user account. Here are some examples.

Create new user account with scponly as shell:
```Shell
useradd -s /usr/sbin/scponly user1
```

Modify user account to set rssh as a shell:
```Shell
usermod -s /usr/sbin/rssh user2
```
Where /usr/sbin/scponly is binary executable of scponly.

rssh comes with text configuration file usually stored in /etc/rssh.conf. You can either setup per-user settings there or configure global restrictions for all accounts which are using rssh. Default rssh.conf file is well commented so there shouldn’t be any problems to configure rssh as you needs. At the same time, here are some examples.

If you wish to restrict all users to scp and rsync only then you should uncomment lines in rssh.conf like below:
```Shell
allowscp
#allowsftp
#allowcvs
#allowrdist
allowrsync
```

Now coming to per-user examples. User peter is allowed to use scp protocol only, the following line in rssh.conf will do that:
```Shell
user=sbk:022:00001:
```

User ann is allowed to scp, rsync only:
```Shell
user=sbk:022:10001:
```
As you can see enabled protocols in per-user setup are specified as 11000 (scp, sftp), 11111 (scp, sftp, cvs, rdist, rsync) or 00000 (no protocols enabled). 022 in above examples specifies umask.

Testing

Let’s assume you’ve created user1 and enabled only scp and rsync using rssh. An attempt to access the server via SSH under user1 account will end with the following output:
```Shell
artiomix$ ssh user1@1.2.3.4
user1@1.2.3.4's password: 
 
This account is restricted by rssh.
Allowed commands: scp rsync

If you believe this is in error, please contact your system administrator.
Connection to 1.2.3.4 closed.
```

At the same time scp transfers will work without problems:
```Shell
artiomix$ scp -P 23451 /etc/test.file user1@1.2.3.4:/tmp
user1@1.2.3.4's password:
test.file                             100%  983     1.0KB/s   00:00
Further Reading
```
rssh support chroot environments for scp, rsync and other transfer protocols. It means that you can restrict users not only by command they can use but also by filesystems they reach. For example, user1 can be chrooted to /chroot_user1 so it can’t be used to copy something from /etc or /var/www directories of the server. Here is nice manual about chroot in rssh.
