# Linux and PASE AIX Commands

***touch*** - Create a new empty file.
```
touch filename.txt
```

***chmod*** - change file permissions.
```
Full permissions example: chmod 777 filename.txt
```

***find*** - find files

https://www.linode.com/docs/tools-reference/tools/find-files-in-linux-using-the-command-line/

```
Ex: find /home -name *.jpg	Find all .jpg files in the /home and sub-directories.
```

***dhclient*** - request a new IP address from DHCP

https://www.cyberciti.biz/faq/howto-linux-renew-dhcp-client-ip-address/

```
Renew IP address example: sudo dhclient -r
```

***ls*** - List files

https://techyaz.com/linux/11-examples-ls-command-list-files-linux/

```
List all files: ls *

List all PDF files: ls *.pdf

List all files wide foramt: ls -l

```

***cp*** - Copy files and directories

https://www.rapidtables.com/code/linux/cp.html

```
Copy file from one path to another: cp /dir1/file.txt  /dir2/file.txt
```

***mkdir*** - Make directory

https://www.computerhope.com/unix/umkdir.htm

```
Ex: mkdir /demo
```

***rmdir*** - Remove directory

https://www.computerhope.com/unix/urmdir.htm

```
ex: rmdir /dirname
```

***ifconfig*** - Check IP addresses

https://www.journaldev.com/30052/linux-ifconfig-command-examples

```
Ex: ifconfig
```

***ip*** - Newer Replacement for ifconfig - Check IP addresses

https://computingforgeeks.com/ifconfig-vs-ip-usage-guide-on-linux/#:~:text=%20ifconfig%20vs%20ip%20usage%20guide%20on%20Linux,ip%20and%20ifconfig%20commands.%20For%20this...%20More%20

```
Ex: ip address    (list ip addresses)
```

***systemctl*** - Linux Services

```
List all services active or not:
systemctl list-units --all --type=service --no-pager
```

# Additional samples links

https://www.journaldev.com/24613/linux-ps-command

crontab

awk

grep 

sudo 

cp 

export

nohup 

alias

zip

unzip




