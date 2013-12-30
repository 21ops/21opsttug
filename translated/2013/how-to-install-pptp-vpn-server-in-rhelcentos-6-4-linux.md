#Centos6.4下PPTP VPN server安装配置

在这篇文章中，我们将向您展示如何安装和正确的在RHEL/CentOS的linux上配置PPTP VPN服务器。
 
在你服务器IP地址以太网接口上，通过VPN能够针对你传输的数据进行加密。这种隧道技术与其他设备，如桌面操作系统，手机和平板电脑是兼容。
 
首先需要启用TUN模块（tunelling内核模块）：

```Shell
# echo 'modprobe tun' >> /etc/rc.modules
# chmod +x /etc/rc.modules
```
下一次启动的时候让tun模块加载到内核中

确认并删除以前安装的软件:
```Shell
yum remove -y pptpd ppp
iptables --flush POSTROUTING --table nat
iptables --flush FORWARD
rm -rf /etc/pptpd.conf
rm -rf /etc/ppp
```
安装步骤：

首先通过sourceforge安装poptop
```Shell
rpm -Uhv http://poptop.sourceforge.net/yum/stable/rhel6/pptp-release-current.noarch.rpm
yum -y install make libpcap iptables gcc-c++ logrotate tar cpio perl pam tcp_wrappers dkms kernel_ppp_mppe ppp pptpd
```
现在，我们需要启用系统转发功能，并设置内部IP地址，以及PPTP服务器的DNS：
```Shell
mknod /dev/ppp c 108 0
echo 1 > /proc/sys/net/ipv4/ip_forward
echo "mknod /dev/ppp c 108 0" >> /etc/rc.local
echo "echo 1 &gt; /proc/sys/net/ipv4/ip_forward" >> /etc/rc.local
echo "localip 172.16.36.1" >> /etc/pptpd.conf
echo "remoteip 172.16.36.2-254" >> /etc/pptpd.conf
echo "ms-dns 8.8.8.8" >> /etc/ppp/options.pptpd
echo "ms-dns 8.8.4.4" >> /etc/ppp/options.pptpd
```
然后，建立PPTP服务器的用户凭据。此证书将用于每一个客户端/设备登录并连接到PPTP服务器：
```Shell
nano /etc/ppp/chap-secrets
```
你的chap-secrets文件应该如下所示：
```Shell
# Secrets for authentication using CHAP
# client server secret IP addresses
yourusername pptpd yourpassword *
```
保存并关闭文件。
接下来，你需要打开正确的端口和数据包转发规则，添加下面的iptables规则：
```Shell
# VPN rules (pptpd)
iptables -A INPUT -i eth0 -p tcp --dport 1723 -j ACCEPT
iptables -A INPUT -i eth0 -p gre -j ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -p tcp -s 172.16.36.0/24 -j TCPMSS --syn --set-mss 1356
```
保持并重启你Iptables防火墙:
```Shell
service iptables save
service iptables restart
确保每次重启后自动加载:

```Shell
chkconfig iptables on
chkconfig pptpd on
```
最后重启iptables和pptp服务:
```Shell
service iptables start
service pptpd start
```
英文原文:[lintut](http://lintut.com/how-to-install-pptp-vpn-server-in-rhelcentos-6-4-linux/) 翻译者:[新世纪linux社区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
