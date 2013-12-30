#12 TOP Command Examples in Linux

This is the part of our on-going series of commands in Linux. We have covered basic ls command and cat command. In this article, we are trying to explore top command which is one of the most frequently used commands in our daily system administrative jobs. top command displays processor activity of your Linux box and also displays tasks managed by kernel in real-time. It’ll show processor and memory are being used and other information like running processes. This may help you to take correct action. top command found in UNIX-like operating systems.

You might also be interested in following tutorials :

*[Htop (Linux Process Monitoring) tool for RHEL, CentOS & Fedora](http://www.tecmint.com/install-htop-linux-process-monitoring-for-rhel-centos-fedora/)

*[Iotop (Monitor Linux Disk I/O) in RHEL, CentOS and Fedora](http://www.tecmint.com/install-iotop-monitor-linux-disk-io-in-rhel-centos-and-fedora/)

##1. Display of Top Command
In this example, it will show information like tasks, memory, cpu and swap. Press 'q' to quit window.
```Shell
# top
```
<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Command.jpg'>

Linux Top Command

##2. Sorting with -O (Uppercase Letter 'O').
Press (Shift+O) to Sort field via field letter, for example press 'a' letter to sort process with PID (Process ID).

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Sort.jpg'>

Sorting Process ID’s with Top

Type any key to return to main top window with sorted PID order as shown in below screen. Press 'q' to quit exit the window.
<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Sort.jpg'>

Sorting Process ID's

##3. Display Specific User Process
Use top command with 'u' option will display specific User process details.
```Shell
# top -u tecmint
```
<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-User-Process.jpg'>

Top with Specific User Processes

##4. Highlight Running Process in Top
Press 'z' option in running top command will display running process in color which may help you to identified running process easily.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Colorful.png'>

Top Process with Colorful

##5. Shows Absolute Path of Processes
Press'c' option in running top command, it will display absolute path of running process.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-command-with-Path.jpg'>

Top with Specific Process Path

##6. Change Delay or Set 'Screen Refresh Interval' in Top
By default screen refresh interval is 3.0 seconds, same can be change pressing ‘d‘ option in running top command and change it as desired as shown below.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Set-Refresh-Time.jpg'>

Top – Set Refresh Time

##7. Kill running process with argument 'k'.
You can kill a process after finding PID of process by pressing ‘k‘ option in running top command without exiting from top window as shown below.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Kill-Process.jpg'>

Top-Kill Process ID

##8. Sort by CPU Utilisation
Press (Shift+P) to sort processes as per CPU utilization. See screenshot below.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-With-CPU-Utilization.jpg'>

Top - High CPU Utilization

##9. Renice a Process
You can use 'r' option to change the priority of the process also called Renice.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-Renice-Process.jpg'>

Top – Renice Process

##10. Save Top Command Results
Press (Shift+W) to save the running top command results under /root/.toprc.
Top Command Save Results
Top Command Save Results

##11. Getting Top Command Help
Press 'h' option to obtain the top command help.

<img src='http://www.tecmint.com/wp-content/uploads/2012/08/Top-command-help.jpg'>

Top Command Help

##12. Exit Top Command After Specific repetition
Top output keep refreshing until you press 'q'. With below command top command will automatically exit after 10 number of repetition.
```Shell
#top -n 10
```
There are number of arguments to know more about top command you may refer man page of top command. Please share it if you find this article useful through our comment box below.

