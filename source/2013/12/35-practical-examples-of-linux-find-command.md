#35 Practical Examples of Linux Find Command

this article we are sharing our day-to-day Linux find command experience and its usage in the form of examples. In this article we will show you the most used 35 Find Commands examples in Linux. We have divided the section into Five parts from basic to advance usage of find command.

Through this article we are sharing our day-to-day Linux find command experience and its usage in the form of examples. In this article we will show you the most used 35 Find Commands examples in Linux. We have divided the section into Five parts from basic to advance usage of find command.

* Part I: Basic Find Commands for Finding Files with Names
* Part II: Find Files Based on their Permissions
* Part III: Search Files Based On Owners and Groups
* Part IV: Find Files and Directories Based on Date and Time
* Part V: Find Files and Directories Based on Size

> #Part I – Basic Find Commands for Finding Files with Names

##1. Find Files Using Name in Current Directory
Find all the files whose name is tecmint.txt in a current working directory.
```Shell
#find . -name tecmint.txt
./tecmint.txt
```

##2. Find Files Under Home Directory
Find all the files under /home directory with name tecmint.txt.
```Shell
#find /home -name tecmint.txt
/home/tecmint.txt
```

##3. Find Files Using Name and Ignoring Case
Find all the files whose name is tecmint.txt and contains both capital and small letters in /home directory.
```Shell
#find /home -iname tecmint.txt
./tecmint.txt
./Tecmint.txt
```

##4. Find Directories Using Name
Find all directories whose name is Tecmint in / directory.
```Shell
#find / -type d -name Tecmint
/Tecmint
```

##5. Find PHP Files Using Name
Find all php files whose name is tecmint.php in a current working directory.
```Shell
#find . -type f -name tecmint.php
./tecmint.php
```

##6. Find all PHP Files in Directory
Find all php files in a directory.
```Shell
#find . -type f -name "*.php"
./tecmint.php
./login.php
./index.php
```

> #Part II – Find Files Based on their Permissions

##7. Find Files With 777 Permissions
Find all the files whose permissions are 777.
```Shell
#find . -type f -perm 0777 -print
```

##8. Find Files Without 777 Permissions
Find all the files without permission 777.
```Shell
#find / -type f ! -perm 777
```

##9. Find SGID Files with 644 Permissions
Find all the SGID bit files whose permissions set to 644.
```Shell
#find / -perm 2644
```

##10. Find Sticky Bit Files with 551 Permissions
Find all the Sticky Bit set files whose permission are 551.
```Shell
#find / -perm 1551
```

##11. Find SUID Files
Find all SUID set files.
```Shell
#find / -perm /u=s
```

##12. Find SGID Files
Find all SGID set files.
```Shell
#find / -perm /g+s
```

##13. Find Read Only Files
Find all Read Only files.
```Shell
#find / -perm /u=r
```

##14. Find Executable Files
Find all Executable files.
# find / -perm /a=x

##15. Find Files with 777 Permissions and Chmod to 644
Find all 777 permission files and use chmod command to set permissions to 644.
```Shell
#find / -type f -perm 0777 -print -exec chmod 644 {} \;
```

##16. Find Directories with 777 Permissions and Chmod to 755
Find all 777 permission directories and use chmod command to set permissions to 755.
```Shell
#find / -type d -perm 777 -print -exec chmod 755 {} \;
```

##17. Find and remove single File
To find a single file called tecmint.txt and remove it.
```Shell
#find . -type f -name "tecmint.txt" -exec rm -f {} \;
```

##18. Find and remove Multiple File
To find and remove multiple files such as .mp3 or .txt, then use.
```Shell
#find . -type f -name "*.txt" -exec rm -f {} \;
OR
#find . -type f -name "*.mp3" -exec rm -f {} \;
```

##19. Find all Empty Files
To file all empty files under certain path.
```Shell
#find /tmp -type f -empty
```

##20. Find all Empty Directories
To file all empty directories under certain path.
```Shell
#find /tmp -type d -empty
```
##21. File all Hidden Files
To find all hidden files, use below command.
```Shell
#find /tmp -type f -name ".*"
```

> #Part III – Search Files Based On Owners and Groups

##22. Find Single File Based on User
To find all or single file called tecmint.txt under / root directory of owner root.
```Shell
#find / -user root -name tecmint.txt
```

##23. Find all Files Based on User
To find all files that belongs to user Tecmint under /home directory.
```Shell
#find /home -user tecmint

##24. Find all Files Based on Group
To find all files that belongs to group Developer under /home directory.
```Shell
#find /home -group developer
```
##25. Find Particular Files of User
To find all .txt files of user Tecmint under /home directory.
```Shell
#find /home -user tecmint -iname "*.txt"
```


> #Part IV – Find Files and Directories Based on Date and Time

##26. Find Last 50 Days Modified Files
To find all the files which are modified 50 days back.
```Shell
#find / -mtime 50
```

##27. Find Last 50 Days Accessed Files
To find all the files which are accessed 50 days back.
```Shell
#find / -atime 50
```

##28. Find Last 50-100 Days Modified Files
To find all the files which are modified more than 50 days back and less than 100 days.
```Shell
#find / -mtime +50 –mtime -100
```

##29. Find Changed Files in Last 1 Hour
To find all the files which are changed in last 1 hour.
```Shell
#find / -cmin -60
```
##30. Find Modified Files in Last 1 Hour
To find all the files which are modified in last 1 hour.
```Shell
#find / -mmin -60
```
##31. Find Accessed Files in Last 1 Hour
To find all the files which are accessed in last 1 hour.
```Shell
#find / -amin -60
```

> #Part V – Find Files and Directories Based on Size

##32. Find 50MB Files
To find all 50MB files, use.
```Shell
#find / -size 50M
```

##33. Find Size between 50MB – 100MB
To find all the files which are greater than 50MB and less than 100MB.
```Shell
#find / -size +50M -size -100M
```

##34. Find and Delete 100MB Files
To find all 100MB files and delete them using one single command.
```Shell
#find / -size +100M -exec rm -rf {} \;
```

##35. Find Specific Files and Delete
Find all .mp3 files with more than 10MB and delete them using one single command.
```Shell
#find / -type f -name *.mp3 -size +10M -exec rm {} \;
```

That’s it, We are ending this post here, In our next article we will discuss more about other Linux commands in depth with practical examples. Let us know your opinions on this article using our comment section.


英文原文:[tecmint](http://www.tecmint.com/35-practical-examples-of-linux-find-command/) 翻译者:[新世纪linux区翻译组](https://github.com/21ops/21opsttug) 社区地址:[新世纪Linux社区](http://www.21ops.com)
