# File Nevigation in Linux commands 

1. **pwd** - Print Working Directory
```
pwd
```
2. **cd** - change directory 

```
cd /path/to/directory
```
3. **ls** - list directory contents

```
ls
```
4. **mkdir** [folder name] - make directory
```
mkdir [folder_name]
```
5. **rmdir** [folder name] - remove directory
```
rmdir [folder_name]
```

6. **touch** [file name] - create a file
```
touch [file_name.txt]
```

7. **ls -la** - list all files including hidden files
```
ls -la

total 116
drwx------ 15 chimi chimi  4096 Oct 24 14:59 .
drwxr-xr-x  3 root  root   4096 Oct 10 23:56 ..
-rw-r--r--  1 chimi chimi   220 Oct 10 23:56 .bash_logout
-rw-r--r--  1 chimi chimi  5551 Oct 10 23:56 .bashrc
-rw-r--r--  1 chimi chimi  3526 Oct 10 23:56 .bashrc.original
drwx------ 10 chimi chimi  4096 Oct 11 00:05 .cache
drwxr-xr-x 15 chimi chimi  4096 Oct 11 10:27 .config
-rw-r--r--  1 chimi chimi 11759 Oct 10 23:56 .face
lrwxrwxrwx  1 chimi chimi     5 Oct 10 23:56 .face.icon -> .face
drwxr-xr-x  4 chimi chimi  4096 Oct 15 10:30 .java
drwxr-xr-x  4 chimi chimi  4096 Oct 10 23:58 .local
drwx------  4 chimi chimi  4096 Oct 11 00:01 .mozilla
-rw-r--r--  1 chimi chimi   807 Oct 10 23:56 .profile
-rw-r--r--  1 chimi chimi     0 Oct 12 21:12 .sudo_as_admin_successful
-rw-------  1 chimi chimi  9572 Oct 21 14:51 .zsh_history
-rw-r--r--  1 chimi chimi 10868 Oct 10 23:56 .zshrc
drwxr-xr-x  2 chimi chimi  4096 Oct 21 10:14 Desktop
drwxr-xr-x  2 chimi chimi  4096 Oct 10 23:58 Documents
drwxr-xr-x  3 chimi chimi  4096 Oct 24 14:09 Downloads
drwxr-xr-x  2 chimi chimi  4096 Oct 10 23:58 Music
drwxr-xr-x  3 chimi chimi  4096 Oct 21 13:37 Pictures
drwxr-xr-x  2 chimi chimi  4096 Oct 10 23:58 Public
drwxr-xr-x  2 chimi chimi  4096 Oct 10 23:58 Templates
drwxr-xr-x  2 chimi chimi  4096 Oct 10 23:58 Videos
-rw-rw-r--  1 chimi chimi     0 Oct 24 14:59 new.txt

```
* Everything starting with **d**  [from drwxr-xr-x] are directory.
* Everything starting with **-** [from -rw-r--r--] are files.

8. Copy a file and past to new location

```
cp [file_name.extension] [new_location]

cp new.txt /home/user/new.txt
```

9. Move a file to new location

```
mv [file_name.extension] [new_location]

mv new.txt /Desktop/new.txt
```

10. locate a file in sysytem

```
locate file_name.extension
```

11. **cat** - concatenate and display the content of file

```
cat file_name.extension
```

# Network Commands

* **ifconfig** - display network interface configuration like IP address, MAC address etc.

```
ifconfig
```

* **ping** - check the network connectivity between two devices

```
ping [IP address]
```
**ping once**

```
ping -c 1 [IP address]
```

* **arp -a** - associating ip address with MAC address

* **netstat** - display network connections, ports, routing tables, interface statistics, masquerade connections, and multicast memberships

* **history** - display the history of commands

* Save the ping results to ping.txt file

```
ping -c 5 10.10.10.180 > ping.txt
```
result will be saved in ping.txt file

* view the content of ping.txt file

```
cat ping.txt

PING 192.168.56.129 (192.168.56.129) 56(84) bytes of data.
64 bytes from 192.168.56.129: icmp_seq=1 ttl=64 time=0.050 ms
64 bytes from 192.168.56.129: icmp_seq=2 ttl=64 time=0.062 ms
64 bytes from 192.168.56.129: icmp_seq=3 ttl=64 time=0.075 ms
64 bytes from 192.168.56.129: icmp_seq=4 ttl=64 time=0.122 ms
64 bytes from 192.168.56.129: icmp_seq=5 ttl=64 time=0.064 ms

--- 192.168.56.129 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4104ms
rtt min/avg/max/mdev = 0.050/0.074/0.122/0.025 ms
                                                    
```

* grap a specific line from the file like ip **icmp_seq=1**

``` 
cat ping.txt | grep icmp_seq=1   

64 bytes from 192.168.56.129: icmp_seq=1 ttl=64 time=0.050 ms
```








