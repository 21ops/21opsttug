#给nagios添加地理位置功能


前段时间我发现Nagios的NagMap插件和世界各地的多台主机监测发现它非常有用。
例如，在欧洲，美国和其他国家在印度和新西兰也有一些生产服务器，它是更好地看到自己的国家在地图上，
而不是用无聊的Nagios主机状态列表。每个主机都有一个基于ping统计以下状态：绿色，黄色和红色。
绿色/白色（OK）状态相当于0-10％的丢包，黄色（警告）是10-20％的丢包和红色（严重）是指主机关机或丢包，它是20％以上。
所有这三个国家都显示在地图上用不同的标记。



Nagios的使用NagMap插件有可能基于谷歌地图中的主机和它们的状态创建一个地图，这里是我的地图的某些部分：

<img src="http://img01.21ops.com/images/2013/11/14/nagmap1.png">


以上截图显示OK状态（所需的图片）中的所有主机的情况下，当一些台主机出现故障或变得迟缓，那么你会看到这样的
一些红色标记<img src="http://img01.21ops.com/images/2013/11/14/server_red.png">或<img src="http://img01.21ops.com/images/2013/11/14/marker.png">(根据不同类型的主机)安装配置NagMap,所以首先你需要
从项目的下载部分下载nagmap压缩包并解压Nagios监控系统所在的服务器上的某个地方。下载的文件中包含PHP脚本访问Nagios
的状态文件，并显示相应的标记在地图上使用谷歌地图。我建议Nagios的文件目录中创建新的子目录： 

```Shell
    cd /usr/share/nagios/
    wget http://labs.shmu.org.uk/nagmap/nagmap-0.11.tar.gz
    tar -xvzf nagmap-0.11.tar.gz
    rm nagmap-0.11.tar.gz
```
一旦解压缩归档文件，它是必要的设置路径Nagios的状态文件在Nagmap文件status.php的。在我的情况下，Nagios的status.dat文件位于/ VAR /的nagios/ status.dat的中，所以我有以下行在nagmap status.php：

```Shell
    $fp = fopen("/var/nagios/status.dat","r");
```



这是自然的，Web服务器必须有足够的权限读取的/ var/的nagios/ status.dat的文件。下一步是建立地理位置的主机应该显示在Nagmap。应具体说明以下列方式：


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

其中“40.664167，-73.938611”（纽约市在这个例子中）的主机的经度和纬度。所以，你应该增加“音符经纬度"线到Nagios
在地图上所有的主机，这样才能看到他们。从这一点来说，你应该能够打开地图，例如https://your.server.com/nagios/nagmap
网址。如果打开的页面是空的，那么在读取或解析status.dat的文件有一些问题。不幸的是，nagmap不提供调试功能，所以你应该
打开marker.php 如https://your.server.com/nagios/nagmap/marker.php，并寻找到它的输出然后看哪里的问题。很有可能你会需
要一些基本的PHP知识。顺便说一句，文件marker.php包含标记图像的路径，所以你可以很容易地改变他们从默认。

英文原文:[linuxscrew](http://www.linuxscrew.com/2012/07/02/nagios-map-geolocation/) 
翻译者:[新世纪linux社区翻译组](https://github.com/21ops/21opsttug)
社区地址:[新世纪Linux社区](http://www.21ops.com)
