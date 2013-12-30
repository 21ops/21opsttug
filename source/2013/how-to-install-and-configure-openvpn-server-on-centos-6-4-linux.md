#How to install and configure openVPN server on CentOS 6.4 linux

OpenVPN is an open source software application that implements virtual private network (VPN) techniques for creating secure point-to-point connections in routed or bridged configurations and remote access facilities. It uses a custom security protocol that utilizes SSL/TLS for key exchange. It is capable of traversing network address translators (NATs) and firewalls.

OpenVPN allows peers to authenticate each other using a pre-shared secret key, certificates, or username/password. When used in a multiclient-server configuration, it allows the server to release an authentication certificate for every client, using signature and Certificate authority. It uses the OpenSSL encryption library extensively, as well as the SSLv3/TLSv1 protocol, and contains many security and control features. [More info about OpenVPN](http://en.wikipedia.org/wiki/Openvpn)

>
Before we begin, you’ll need to have the Extra Packages for Enterprise Linux (EPEL) Repository enabled on your server.
Enable Epel repository on CentOS 5.x/6.x

```Shell
# yum update
```
Verify Tun/Tap Is Installed:
```Shell
# cat /dev/net/tun
```
Should return a similar line:
```Shell
cat: /dev/net/tun: File descriptor in bad state
```
Install the OpenVPN package from EPEL:
```Shell
# yum install openvpn -y
```
Now, copy sample openVPN configuration file to /etc/opnvpn
```Shell
# cp /usr/share/doc/openvpn-2.3.2/sample/sample-config-files/server.conf /etc/openvpn/
```
Edit /etc/openvpn/server.conf file
```Shell
# nano /etc/openvpn/server.conf
```
Uncomment the “push” parameter which causes traffic on our client systems to be routed through OpenVPN.
```Shell
push "redirect-gateway def1 bypass-dhcp"
```
Also uncoment following line:
```Shell
user nobody
group nobody
push "dhcp-option DNS 8.8.8.8"
push "dhcp-option DNS 8.8.4.4"
```
##Generating Keys and Certificates Using easy-rsa

Now that we’ve finished modifying the configuration file, we’ll generate the required keys and certificates. Create the required folder and copy the files over.
```Shell 
# mkdir -p /etc/openvpn/easy-rsa/keys
```
Download required scripts and certificates:
```Shell
# cd /tmp
# wget https://github.com/downloads/OpenVPN/easy-rsa/easy-rsa-2.2.0_master.tar.gz
# tar -xvf easy-rsa-2.2.0_master.tar.gz
# cp /tmp/easy-rsa-2.2.0_master/easy-rsa/2.0/* /etc/openvpn/easy-rsa
```
With the files in the desired location, we’ll edit the “vars” file which provides the easy-rsa scripts with required information.
```Shell
# nano /etc/openvpn/easy-rsa/vars
```
We’re looking to modify the “KEY_” variables, located at the bottom of the file. The variable names are fairly descriptive and should be filled out with the applicable information.
Once completed, the bottom of your “vars” file should appear similar to the following:
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
We’ll now change into our working directory and build our Certificate Authority, or CA, based on the information provided above.
```Shell
cd /etc/openvpn/easy-rsa
source ./vars
./clean-all
./build-ca
```
<img src='http://lintut.com/wp-content/uploads/2013/09/Screenshot-from-2013-09-23-234109.png'>

 Build our Certificate Authority

Now that we have our CA, we’ll create our certificate for the OpenVPN server. When asked by build-key-server, answer yes to commit.
```Shell
./build-key-server server
```
We’re also going to need to generate our Diffie Hellman key exchange files using the build-dh script and copy all of our files into /etc/openvpn as follows:
```Shell
./build-dh
cd /etc/openvpn/easy-rsa/keys
cp dh1024.pem ca.crt server.crt server.key /etc/openvpn
```

<img src='http://lintut.com/wp-content/uploads/2013/09/Screenshot-from-2013-09-23-234558.png'>
run build-dh script

 
In order to allow clients to authenticate, we’ll need to create client certificates. You can repeat this as necessary to generate a unique certificate and key for each client or device. If you plan to have more than a couple certificate pairs be sure to use descriptive filenames.
```Shell
cd /etc/openvpn/easy-rsa
./build-key client
```
##Routing Configuration and Starting OpenVPN Server
Enable IP Forwarding in sysctl:
```Shell
nano -w /etc/sysctl.conf
# Controls IP packet forwarding
net.ipv4.ip_forward = 1
```
Apply our new sysctl settings.
```Shell
# sysctl -p
# service openvpn start
# chkconfig openvpn on
```

Create an iptables rule to allow proper routing of our VPN subnet.
```Shell
# iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE
# service iptables save
```
##Configuring OpenVPN Client

Finally lets create a server.ovpn config file. To make it easy, you can simply create it on your local computer using Notepad (or any other simple text editor tool). Enter following in that file:
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
Then save it with .ovpn extension. Save that file in the config directory of where you installed OpenVPN client in your computer.

英文原文地址:[how-to-install-and-configure-openvpn-server-on-centos-6-4-linux](http://lintut.com/how-to-install-and-configure-openvpn-server-on-centos-6-4-linux/)
