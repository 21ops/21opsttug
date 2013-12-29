#Centos6.4下如何安装配置OpenVPN

OpenVPN是一个开源的应用程序，它用来实现虚拟专用网（VPN）技术，主要用在路由或桥接配置上以及远程接入设施上，创造安全的点至点连接。它利用SSL/TLS密钥来定义安全认证协议。它能够穿越网络地址转换（NAT）和防火墙。

OpenVPN同级服务器之间可以预共享密钥、证书或用户名/密码进行身份验证对方。在多客户-服务器配置中使用，使用签名和证书颁发 机构，它允许服务器为每个客户端身份颁发验证证书。它使用流行的OpenSSL加密库，以及在SSLv3/TLSv1协议，并包含了许多安全性和控制功 能。关于OpenVPN的更多信息
在我们开始之前，你需要为你的服务器上启用企业版linux（EPEL）存储库中的额外的软件包。启用在CentOS5.x/6.x下的Epel源。
```Shell
# yum update
```
验证Tun/Tap是否安装:
```Shell
# cat /dev/net/tun
```
应该返回如下类似行:
```Shell
cat: /dev/net/tun: File descriptor in bad state
```
通过EPEL安装Openvpn软件包:
```Shell
# yum install openvpn -y
```
现在拷贝openvpn模板文件到 /etc/opnvpn下面:
```Shell
# cp /usr/share/doc/openvpn-2.3.2/sample/sample-config-files/server.conf
# /etc/openvpn/
```
编辑/etc/openvpn/server.conf配置文件:
```Shell
# vim /etc/openvpn/server.conf
```
取消“push”注释参数，让客户端请求通过路由
```Shell
push "redirect-gateway def1 bypass-dhcp"
```
还可以去掉如下参数注释:
```Shell
user nobody
group nobody
push "dhcp-option DNS 8.8.8.8"
push "dhcp-option DNS 8.8.4.4"
```
使用easy-rsa生成密钥和证书
现在，我们已经完成了修改配置文件，我们将生成所需的密钥和证书。创建所需的文件夹，然后复制文件。

```Shell
# mkdir -p /etc/openvpn/easy-rsa/keys
```

下载所需的脚本和证书:
```Shell
# cd /tmp
# wget
# https://github.com/downloads/OpenVPN/easy-rsa/easy-rsa-2.2.0_master.tar.gz
# tar -xvf easy-rsa-2.2.0_master.tar.gz
# cp /tmp/easy-rsa-2.2.0_master/easy-rsa/2.0/* /etc/openvpn/easy-rsa
```
找到所需配置，编辑“vars”文件，该文件主要提供的easy-rsa脚本与所需信息。
```Shell
# vim /etc/openvpn/easy-rsa/vars
```
我们需要在文件底部，填写合适的“KEY_”变量。变量名相当的描述，应填写合适的信息。一旦完成，你的“vars”文 件的底部应该出现类似于以下内容：
```Shell
export KEY_COUNTRY="US"
export KEY_PROVINCE="CA"
export KEY_CITY="SanFrancisco"
export KEY_ORG="Lin tut"
export KEY_EMAIL="info@lintut.com"
export KEY_EMAIL=info@lintut.com
export KEY_CN=changeme
export KEY_NAME=changeme
export KEY_OU=changeme
export PKCS11_MODULE_PATH=changeme
```
根据上面提供的信息，现在我们要改变到我们的工作目录，并建立我们的证书颁发机构，或CA。
```Shell
cd /etc/openvpn/easy-rsa
source ./vars
./clean-all
./build-ca
```

Build our Certificate Authority

现在，我们有我们的CA了，我们将创建我们的OpenVPN服务器证书。当集中密钥服务器询问的时候，回答是肯定的。
```Shell
./build-key-server server
```
我们也需要生成使用内建DH脚本，我们的Diffie Hellman密钥交换文件和所有的文件复制到/etc/openvpn下，如下所示：
```Shell
./build-dh
cd /etc/openvpn/easy-rsa/keys
cp dh1024.pem ca.crt server.crt server.key /etc/openvpn
```


run build-dh script

为了让客户端进行身份验证，我们需要创建客户端证书。您可以重复为每个客户端或设备产生一个唯一的证书和密钥。如果你规划超过一对以上的密钥对，一定要使用描述清楚文件的名字。
```
cd /etc/openvpn/easy-rsa
./build-key client
```
配置路由并启动OpenVPN服务器
在sysctl中启用IP转发
```Shell
nano -w /etc/sysctl.conf
```
# Controls IP packet forwarding
```Shell
net.ipv4.ip_forward = 1
```
应用新sysctl设置。
```Shell
# sysctl -p
# service openvpn start
# chkconfig openvpn on
```
创建一个iptables规则允许适当的VPN子网路由。
```Shell
# iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE
# service iptables save
```
配置OpenVPN客户

最后，让我们创建一个server.ovpn配置文件。为了方便，你可以简单地使用记事本（或任何其他简单的文本编辑工具）在你的本地计算机上创建它。输入该文件中如下内容：
```Shell
client
dev tun
proto udp
remote ip.add.re.ss 1194 # - Your server IP and OpenVPN Port
resolv-retry infinite
nobind
tun-mtu 1500
tun-mtu-extra 32
mssfix 1450
persist-key
persist-tun
ca ca.crt
auth-user-pass
comp-lzo
reneg-sec 0
verb 3
```
然后保存该文件到安装了OpenVPN客户端的config目录下。
类似文档：[http://www.21ops.com/linux/2250.html](http://www.21ops.com/linux/2250.html)

英文原文:[lintut](http://lintut.com/how-to-install-and-configure-openvpn-server-on-centos-6-4-linux/) 翻译者:[新世纪linux社区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)


