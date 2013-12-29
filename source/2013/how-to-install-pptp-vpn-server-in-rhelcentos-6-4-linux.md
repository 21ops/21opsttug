#How to install PPTP VPN server in RHEL/Centos 6.4 Linux

In this article we show you how to install and properly configure a PPTP VPN server in RHEL/CentOS linux. With this VPN you’ll have access to transfering your data encrypted and using a ethernet interface that uses your Server IP address. This tunneling technology is compatible with several devices like desktop operating systems, mobile phones and tablets.
First need enable tun module (tunelling kernel module):

```Shell
echo 'modprobe tun' >> /etc/rc.modules
chmod +x /etc/rc.modules
```

At next boot will be loaded tun module in kernel
Make sure you begin with a clean install by removing any previously installed packages:
```Shell
yum remove -y pptpd ppp
iptables --flush POSTROUTING --table nat
iptables --flush FORWARD
rm -rf /etc/pptpd.conf
rm -rf /etc/ppp
```
Installation procedure
First, install the poptop package from sourceforge:
```Shell
rpm -Uhv http://poptop.sourceforge.net/yum/stable/rhel6/pptp-release-current.noarch.rpm
yum -y install make libpcap iptables gcc-c++ logrotate tar cpio perl pam tcp_wrappers dkms kernel_ppp_mppe ppp pptpd
```

Now, we need to enable IP forwading, set internal IP addresses and point the DNS Servers that will be used by the pptp server:
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

Then, create your users credentials for the PPTP server. This credentials will be used to log in to the PPTP server on every client/device you connect from:

```Shell
nano /etc/ppp/chap-secrets
```

Your chap-secrets file should look like this:
```Shell
# Secrets for authentication using CHAP
# client server secret IP addresses
yourusername pptpd yourpassword *
```
Save and close the file.
Next, you need to add the following iptables rules in order to open the correct ports and properly forward the data packets:

```Shell
# VPN rules (pptpd)
iptables -A INPUT -i eth0 -p tcp --dport 1723 -j ACCEPT
iptables -A INPUT -i eth0 -p gre -j ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -p tcp -s 172.16.36.0/24 -j TCPMSS --syn --set-mss 1356
Save and restart your iptables firewall:
service iptables save
service iptables restart
```

Make sure you load your iptables after every reboot:
```Shell
chkconfig iptables on
chkconfig pptpd on
```
And finally, restart iptables and pptpd services:
service iptables start
service pptpd start
That is it.
Also check out How to install and configure openVPN server on CentOS 6.4 linux

英文原文:[how-to-install-pptp-vpn-server-in-rhelcentos-6-4-linux](http://lintut.com/how-to-install-pptp-vpn-server-in-rhelcentos-6-4-linux/)
