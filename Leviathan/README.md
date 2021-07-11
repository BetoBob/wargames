# [Leviathan](https://overthewire.org/wargames/leviathan/)

**Note:** Pretty much all of the Level chapters are left intentionally blank. So I guess it's up to the player to figure out how to progress.

## Level 0

```bash
ssh -p 2223 leviathan0@leviathan.labs.overthewire.org
```

**Level 0 Password**

```
leviathan0
```

## Level 0 -> Level 1

Lets explore the `/home/` directory:

```bash
leviathan0@leviathan:/home$ ls -lR
.:
total 32
drwxr-xr-x 3 root root 4096 Aug 26  2019 leviathan0
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan1
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan2
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan3
drwxr-xr-x 3 root root 4096 Aug 26  2019 leviathan4
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan5
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan6
drwxr-xr-x 2 root root 4096 Aug 26  2019 leviathan7

./leviathan0:
total 0

./leviathan1:
total 8
-r-sr-x--- 1 leviathan2 leviathan1 7452 Aug 26  2019 check

./leviathan2:
total 8
-r-sr-x--- 1 leviathan3 leviathan2 7436 Aug 26  2019 printfile

./leviathan3:
total 12
-r-sr-x--- 1 leviathan4 leviathan3 10288 Aug 26  2019 level3

./leviathan4:
total 0

./leviathan5:
total 8
-r-sr-x--- 1 leviathan6 leviathan5 7560 Aug 26  2019 leviathan5

./leviathan6:
total 8
-r-sr-x--- 1 leviathan7 leviathan6 7452 Aug 26  2019 leviathan6

./leviathan7:
total 4
-r--r----- 1 leviathan7 leviathan7 178 Aug 26  2019 CONGRATULATIONS
```

So there is nothing in the `/home/` directory for `leviathan0` to access.

So lets explore the root directory I guess:

```bash
leviathan0@leviathan:/$ ls -l
total 308
drwxr-xr-x   2 root root   4096 Oct 16  2018 bin
drwxr-xr-x   4 root root   4096 Oct 16  2018 boot
dr-xr-xr-x   3 root root      0 May  6  2020 cgroup2
drwxr-xr-x  14 root root   4500 May 12 16:13 dev
drwxr-xr-x  88 root root   4096 Aug 26  2019 etc
drwxr-xr-x  10 root root   4096 Aug 26  2019 home
lrwxrwxrwx   1 root root     29 Oct 16  2018 initrd.img -> boot/initrd.img-4.9.0-6-amd64
lrwxrwxrwx   1 root root     29 Oct 16  2018 initrd.img.old -> boot/initrd.img-4.9.0-6-amd64
drwxr-xr-x  16 root root   4096 Aug 26  2019 lib
drwxr-xr-x   2 root root   4096 Aug 26  2019 lib32
drwxr-xr-x   2 root root   4096 Oct 16  2018 lib64
drwxr-xr-x   2 root root   4096 Aug 26  2019 libx32
drwx------   2 root root  16384 Oct 16  2018 lost+found
drwxr-xr-x   3 root root   4096 Oct 16  2018 media
drwxr-xr-x   2 root root   4096 Oct 16  2018 mnt
drwxr-xr-x   2 root root   4096 Oct 16  2018 opt
dr-xr-xr-x 169 root root      0 May  4  2020 proc
lrwxrwxrwx   1 root root      9 Aug 26  2019 README.txt -> /etc/motd
drwx------   7 root root   4096 Aug 31  2020 root
drwxr-xr-x  15 root root    580 Jul 11 21:56 run
drwxr-xr-x   2 root root   4096 Aug 26  2019 sbin
drwxr-xr-x   3 root root   4096 Aug 26  2019 share
drwxr-xr-x   2 root root   4096 Oct 16  2018 srv
dr-xr-xr-x  12 root root      0 May  5  2020 sys
drwxrws-wt 182 root root 225280 Jul 11 21:58 tmp
drwxr-xr-x  12 root root   4096 Aug 26  2019 usr
drwxr-xr-x  11 root root   4096 Aug 26  2019 var
lrwxrwxrwx   1 root root     26 Oct 16  2018 vmlinuz -> boot/vmlinuz-4.9.0-6-amd64
lrwxrwxrwx   1 root root     26 Oct 16  2018 vmlinuz.old -> boot/vmlinuz-4.9.0-6-amd64
```

Nothing too promising here either. 