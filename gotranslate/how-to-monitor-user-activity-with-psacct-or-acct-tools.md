#How to Monitor User Activity with psacct or acct Tools

psacct or acct both are open source application for monitoring users activities on the system. These applications runs in the background and keeps track of each users activity on your system as well as what resources are being consumed.
I personally used this program in our company, we have development team where our developers continuously work on servers. So, this is one of best program to keep a eye on them. This program provides an excellent way to monitor what users are doing, what commands are they firing, how much resources are being consumed by them, how long users are active on the system. Another great feature of this program is it gives total resources consumed by services like Apache, MySQL, FTP,SSH etc.

I think this is one of the great and must needed application for every Linux/Unix System Administrators, who wanted to keep a track of user activities on their servers/systems.

The psacct or acct package provides several features for monitoring process activities.

* ac command prints the statistics of user logins/logouts (connect time) in hours.
* lastcomm command prints the information of previously executed commands of user.
* accton commands is used to turn on/off process for accounting.
* sa command summarizes information of previously executed commands.
* last and lastb commands show listing of last logged in users.

##Installing psacct or acct Packages
psacct or acct both are similar packages and there is not much difference between them, but the psacct package only available for rpm based distributions such as RHEL, CentOS and Fedora, whereas acct package available for distributions like Ubuntu, Debian and Linux Mint.

To install psacct package under rpm based distributions issue the following yum command.
```Shell
#yum install psacct
```
To install acct package using apt-get command under Ubuntu / Debian / Linux Mint.
```Shell
$sudo apt-get install acct
OR
# apt-get install acct
```

##Starting psacct or acct service
By default psacct service is in disabled mode and you need to start it manually under RHEL/CentOS/Fedora systems. Use the following command to check the status of service.
```Shell
#/etc/init.d/psacct status
Process accounting is disabled.
```

You see the status showing as disabled, so let’s start it manually using the following both commands. These two commands will create a /var/account/pacct file and start services.
```Shell
# chkconfig psacct on
# /etc/init.d/psacct start
Starting process accounting:                               [  OK  ]
```

After starting service, check the status again, you will get status as enabled as shown below.
```Shell
#/etc/init.d/psacct status
Process accounting is enabled.
```
Under Ubuntu, Debian and Mint service is started automatically, you don’t need to start it again.

##Display Statistics of Users Connect Time
ac command without specifying any argument will displays total statistics of connect time in hours based on the user logins/logouts from the current wtmp file.
```Shell
#ac
total     1814.03
```

##Display Statistics of Users Day-wise
Using command "ac -d" will prints out the total login time in hours by day-wise.
```Shell
# ac -d
Sep 17  total        5.23
Sep 18  total       15.20
Sep 24  total        3.21
Sep 25  total        2.27
Sep 26  total        2.64
Sep 27  total        6.19
Oct  1  total        6.41
Oct  3  total        2.42
Oct  4  total        2.52
Oct  5  total        6.11
Oct  8  total       12.98
Oct  9  total       22.65
Oct 11  total       16.18
```
##Display Time Totals for each User
Using command "ac -p" will print the total login time of each user in hours.

```Shell
#ac -p
        root                              1645.18
        tecmint                            168.96
        total     1814.14

Display Individual User Time
To get the total login statistics time of user “tecmint” in hours, use the command as.
```Shell
#ac tecmint
 total      168.96
```

##Display Day-Wise Logn Time of User
The following command will prints the day-wise total login time of user “tecmint” in hours.
```Shell
#ac -d tecmint
Oct 11  total        8.01
Oct 12  total       24.00
Oct 15  total       70.50
Oct 16  total       23.57
Oct 17  total       24.00
Oct 18  total       18.70
Nov 20  total        0.18

##Print All Account Activity Information
The “sa” command is used to print the summary of commands that were executed by users.

```Shell
#sa
       2       9.86re       0.00cp     2466k   sshd*
       8       1.05re       0.00cp     1064k   man
       2      10.08re       0.00cp     2562k   sshd
      12       0.00re       0.00cp     1298k   psacct
       2       0.00re       0.00cp     1575k   troff
      14       0.00re       0.00cp      503k   ac
      10       0.00re       0.00cp     1264k   psacct*
      10       0.00re       0.00cp      466k   consoletype
       9       0.00re       0.00cp      509k   sa
       8       0.02re       0.00cp      769k   udisks-helper-a
       6       0.00re       0.00cp     1057k   touch
       6       0.00re       0.00cp      592k   gzip
       6       0.00re       0.00cp      465k   accton
       4       1.05re       0.00cp     1264k   sh*
       4       0.00re       0.00cp     1264k   nroff*
       2       1.05re       0.00cp     1264k   sh
       2       1.05re       0.00cp     1120k   less
       2       0.00re       0.00cp     1346k   groff
       2       0.00re       0.00cp     1383k   grotty
       2       0.00re       0.00cp     1053k   mktemp
       2       0.00re       0.00cp     1030k   iconv
       2       0.00re       0.00cp     1023k   rm
       2       0.00re       0.00cp     1020k   cat
       2       0.00re       0.00cp     1018k   locale
       2       0.00re       0.00cp      802k   gtbl

##Where
* 9.86re is a “real time” as per wall clock minutes
* 0.01cp is a sum of system/user time in cpu minutes
* 2466k is a cpu-time averaged core usage, i.e. 1k units
* sshd command name

Print Individual User Information
To get the information of individual user, use the options -u.
```Shell
#sa -u
root       0.00 cpu      465k mem accton
root       0.00 cpu     1057k mem touch
root       0.00 cpu     1298k mem psacct
root       0.00 cpu      466k mem consoletype
root       0.00 cpu     1264k mem psacct           *
root       0.00 cpu     1298k mem psacct
root       0.00 cpu      466k mem consoletype
root       0.00 cpu     1264k mem psacct           *
root       0.00 cpu     1298k mem psacct
root       0.00 cpu      466k mem consoletype
root       0.00 cpu     1264k mem psacct           *
root       0.00 cpu      465k mem accton
root       0.00 cpu     1057k mem touch
```

##Print Number of Processes
This command prints the total number of processes and CPU minutes. If you see continue increase in these numbers, then its time to look into the system about what is happening.
```Shell
#sa -m
sshd                                    2       9.86re       0.00cp     2466k
root                                  127      14.29re       0.00cp      909k

##Print Sort by Percentage
The command “sa -c” displays the highest percentage of users.
```Shell
#sa -c
 132  100.00%      24.16re  100.00%       0.01cp  100.00%      923k
       2    1.52%       9.86re   40.83%       0.00cp   53.33%     2466k   sshd*
       8    6.06%       1.05re    4.34%       0.00cp   20.00%     1064k   man
       2    1.52%      10.08re   41.73%       0.00cp   13.33%     2562k   sshd
      12    9.09%       0.00re    0.01%       0.00cp    6.67%     1298k   psacct
       2    1.52%       0.00re    0.00%       0.00cp    6.67%     1575k   troff
      18   13.64%       0.00re    0.00%       0.00cp    0.00%      509k   sa
      14   10.61%       0.00re    0.00%       0.00cp    0.00%      503k   ac
      10    7.58%       0.00re    0.00%       0.00cp    0.00%     1264k   psacct*
      10    7.58%       0.00re    0.00%       0.00cp    0.00%      466k   consoletype
       8    6.06%       0.02re    0.07%       0.00cp    0.00%      769k   udisks-helper-a
       6    4.55%       0.00re    0.00%       0.00cp    0.00%     1057k   touch
       6    4.55%       0.00re    0.00%       0.00cp    0.00%      592k   gzip
       6    4.55%       0.00re    0.00%       0.00cp    0.00%      465k   accton
       4    3.03%       1.05re    4.34%       0.00cp    0.00%     1264k   sh*
       4    3.03%       0.00re    0.00%       0.00cp    0.00%     1264k   nroff*
       2    1.52%       1.05re    4.34%       0.00cp    0.00%     1264k   sh
       2    1.52%       1.05re    4.34%       0.00cp    0.00%     1120k   less
       2    1.52%       0.00re    0.00%       0.00cp    0.00%     1346k   groff
       2    1.52%       0.00re    0.00%       0.00cp    0.00%     1383k   grotty
       2    1.52%       0.00re    0.00%       0.00cp    0.00%     1053k   mktemp

##List Last Executed Commands of User
The "latcomm" command is used to search and display previously executed user commands information. You can also search commands of individual usernames. For example, we see commands of user (tecmint).
```Shell
#lastcomm tecmint
su                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
bash               F    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
id                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
grep                    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
grep                    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
bash               F    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
dircolors               tecmint  pts/0      0.00 secs Wed Feb 13 15:56
bash               F    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
tput                    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
tty                     tecmint  pts/0      0.00 secs Wed Feb 13 15:56
bash               F    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
id                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
bash               F    tecmint  pts/0      0.00 secs Wed Feb 13 15:56
id                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
```

Search Logs for Commands
With the help of the lastcomm command you will be able to view individual use of an each commands.
```Shell
#lastcomm ls
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
ls                      tecmint  pts/0      0.00 secs Wed Feb 13 15:56
```

英文原文:[tecmint](http://www.tecmint.com/how-to-monitor-user-activity-with-psacct-or-acct-tools/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
