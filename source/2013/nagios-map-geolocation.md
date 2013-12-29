#Geolocation for Nagios

Some time ago I came across NagMap addon for Nagios and found it pretty helpful for monitoring multiple hosts around the world.

For example, there are some production servers in Europe, US and others in India and New Zealand and it’s much better see their states on the map rather than using boring Nagios host status list. Every host can have one of the following states based on ping statistics: green, yellow and red. Green/white (ok) status corresponds to 0-10% packet loss, yellow (warning) is 10-20% packet loss and red (critical) means the host is down or packet loss to it is more than 20%. All three states are shown on the map using different markers.

Using NagMap addon for Nagios it’s possible to create a map of the hosts and their states based on Google Maps, here is some part of my map:
<img src="http://www.linuxscrew.com/wp-content/uploads/2012/07/nagmap1.png">

Above screenshot shows all hosts in OK state (desired picture) so in case when some host goes down or becomes sluggish then you’ll see some red markers like this<img src="http://www.linuxscrew.com/wp-content/uploads/2012/07/server_red.png">  or <img src="http://www.linuxscrew.com/wp-content/uploads/2012/07/marker.png">  (depending on type of the host).

Setup and configure NagMap

So first of all you need to download nagmap tarball from project’s download section and unpack it somewhere on the server that hosts Nagios monitoring system. Downloaded tarball contains PHP scripts which will access Nagios’s status file and show corresponding markers on the map using Google Maps. I suggest to create new subdir in directory where Nagios files are located:

```Shell
cd /usr/share/nagios/
wget http://labs.shmu.org.uk/nagmap/nagmap-0.11.tar.gz
tar -xvzf nagmap-0.11.tar.gz
rm nagmap-0.11.tar.gz
```
Once unpacked the archive it’s necessary to set path to Nagios status file in Nagmap’s file status.php. In my case Nagios’s status.dat file is located at /var/nagios/status.dat so I have the following line in nagmap’s status.php:

```Shell
$fp = fopen("/var/nagios/status.dat","r");
```
It’s natural that web server must have enough rights to read /var/nagios/status.dat file.

The next step is to set up geographical location for the hosts which should be shown at Nagmap. It should be specified in the following way:

```Shell
define host {
        use generic-host
        host_name HostName1
        address 11.22.33.44
        notes latlng: 40.664167, -73.938611
        check_command check-host-alive
        register 1
}
```

Where “40.664167, -73.938611″ is longitude and latitude of the host (New York city in this example). So you should add ‘notes latlng:’ lines to all host in Nagios to see them on the map.

From this point you should be able to open the map, e.g. https://your.server.com/nagios/nagmap/ URL. If opened page is empty then there is some problem in reading or parsing status.dat file. Unfortunately nagmap doesn’t provide debug feature so you should open marker.php e.g. https://your.server.com/nagios/nagmap/marker.php  and look into its output to see where’s the problem. Most probably you’ll need some basic PHP knowledge. Btw, file marker.php contains paths to marker images so you can easily change them from default there.

英文原文:[nagios-map-geolocation](http://www.linuxscrew.com/2012/07/02/nagios-map-geolocation/) 
