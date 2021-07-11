# [Bandit](https://overthewire.org/wargames/bandit/)

## Setup

Go to Bandit directory in PowerShell. Open the Github folder and type `powershell` in the address bar to start a session in the working directory.

PowerShell will be used because it has more features then command prompt. A big missing feature in command prompt is command history, which is especially helpful when commands are repeated, like the `ssh` command with the server address.

It also is optimal because it has less overhead than working in the Linux subsystem. If necessary, I can switch to a subsystem enviornment from PowerShell running the `bash` command. 

## Resources

Below is a good set of solutions explaining how to approach these problems:

<iframe width="560" height="315" src="https://www.youtube.com/embed/ff2Au8BIy_A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Level 0

* needed to take port number into account when using SSH
* https://superuser.com/questions/1536983/stuck-in-bandit-level-0-overthewire-org

```
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

## Level 0 -> Level 1

* loging to a new user for each level:

```
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

```
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

## Level 1 -> Level 2

* the filename was a special character (`-`), meaning I had do `cat ./-` in order to open up
* password for `bandit2`:

```
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

## Level 2 -> Level 3

* password for `bandit3`:

```
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

## Level 3 -> Level 4

* stored in a `.hidden` file
* password for `bandit4`:

```
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## Level 4 -> Level 5

* use `./-file00` to check files

```bash
bandit4@bandit:~/inhere$ file ./-file00
./-file00: data
bandit4@bandit:~/inhere$ file ./-file01
./-file01: data
bandit4@bandit:~/inhere$ file ./-file02
./-file02: data
bandit4@bandit:~/inhere$ file ./-file03
./-file03: data
bandit4@bandit:~/inhere$ file ./-file04
./-file04: data
bandit4@bandit:~/inhere$ file ./-file05
./-file05: data
bandit4@bandit:~/inhere$ file ./-file06
./-file06: data
bandit4@bandit:~/inhere$ file ./-file07
./-file07: ASCII text
```

* password for `bandit5`:

```
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## Level 5 -> Level 6

* **note:** remember to look for *all* files (including hidden files)
* **note:** in the future probably better to just use the `find` command (more proper and probably faster)
* I looked up the solution for this one

```bash
bandit5@bandit:~/inhere$ ls -alR | grep -F '1033' -B 10
-rw-r-----  1 root bandit5 4251 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 8065 May  7  2020 spaces file3

./maybehere07:
total 56
drwxr-x---  2 root bandit5 4096 May  7  2020 .
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
-rwxr-x---  1 root bandit5 3663 May  7  2020 -file1
-rwxr-x---  1 root bandit5 3065 May  7  2020 .file1
-rw-r-----  1 root bandit5 2488 May  7  2020 -file2
-rw-r-----  1 root bandit5 1033 May  7  2020 .file2
```

* https://stackoverflow.com/questions/4909751/how-do-i-list-all-the-files-in-a-directory-and-subdirectories-in-reverse-chronol

* https://stackoverflow.com/questions/11797730/how-to-find-lines-containing-a-string-in-linux

* [grep -B flag](https://stackoverflow.com/questions/9081/grep-a-file-but-show-several-surrounding-lines)

**Level 6 Password**

```
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

## [Level 6 -> Level 7](https://overthewire.org/wargames/bandit/bandit7.html)

* using the `find` command

```bash
bandit6@bandit:/home/bandit5$ find where-to-look criteria action 2>/dev/null
bandit6@bandit:/home/bandit5$ find / -type f -user bandit7 -group bandit6 -size 33c -print 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

* [remove 'Permission Denied' error messages](https://www.cyberciti.biz/faq/bash-find-exclude-all-permission-denied-messages/)

Using the previous `ls` command did not work well for this solution, so I ended up looking up how to use the `find` command.

**Level 7 Password**

```
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

## [Level 7 -> Level 8](https://overthewire.org/wargames/bandit/bandit8.html)

```bash
bandit7@bandit:~$ cat data.txt | grep -F 'millionth'
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

**Level 8 Password**

```
cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

## [Level 8 -> Level 9](https://overthewire.org/wargames/bandit/bandit9.html)

* [why sort before uniq command](https://askubuntu.com/questions/536775/uniq-command-not-working-properly)

```
bandit8@bandit:~$ sort data.txt | uniq -c | grep -F '1 '
      1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

**Level 9 Password**

```
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

## [Level 9 -> Level 10](https://overthewire.org/wargames/bandit/bandit10.html)

```bash
bandit9@bandit:~$ strings data.txt | grep -F "======"
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

**Level 10 Password**

```
truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

## [Level 10 -> Level 11](https://overthewire.org/wargames/bandit/bandit11.html)

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

**Level 11 Password**

```
IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

## [Level 11 -> Level 12](https://overthewire.org/wargames/bandit/bandit12.html)

* [how to rotate letters using `rt`](https://stackoverflow.com/questions/6441260/how-to-shift-each-letter-of-the-string-by-a-given-number-of-letters)

```bash
bandit11@bandit:~$ cat data.txt | tr '[a-z][A-Z]' '[n-za-m][N-ZA-M]'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

**Level 12 Password**

```
5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

## [Level 12 -> Level 13](https://overthewire.org/wargames/bandit/bandit13.html)

* storing files in directory `/tmp/beto/`
  * you can change to this directory to easily do work in it
* I used [this blog post](https://dynamicparallax.wordpress.com/2015/09/22/bandit-level-12-%E2%86%92-level-13/) to help me understand how to work backwards in the decompression
  * used it on the first decompression step, then used the `man` pages for future steps

**Steps**

1. Reverse Hex (only once; because this occurred after all the compression)
   * use `xxd -r` to achieve this
2. Reverse Compression several times

Reversing the hex is pretty easy. The trick is doing backwards compression on the files. In order to do this, you must know how the file is compressed because there are several compression algorithms. So here is the way to loop backwards through the compression:

1. do `file data` to check which tool was used to compress the file last
2. read the `man` page of the file to learn how to decompress a file
3. change the `data` file name if necessary for the compression tool
   * **example**: `gzip` requires the `.gz` file extension (use `mv` to rename the file appropriately)
4. run the correct decompress algorithm and continue to the next one

This involved several steps, so I am only going to show some sample commands I ran. The first snippet was using `file` command on the first data file I changed. This was after running `xxd -r` to reverse the hexdump of the file:

```bash
bandit12@bandit:~$ file /tmp/beto/data1.txt
/tmp/beto/data1.txt: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

So for this first set of de-compression, I had to rename `data1.txt` to `data1.gz`, then I ran the command `gzip -d data1.gz` to unzip the file.

I did this for several other compression types including `gzip`, `gzip2`, `tar` and `bzip`. After doing this several times and learning the proper decompression flags to run for these commands, I finally got the password:

```bash
bandit12@bandit:/tmp/beto$ file data8.gz
data8.gz: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/beto$ gzip -d data8.gz
bandit12@bandit:/tmp/beto$ cat data8
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

**Level 13 Password**

```
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

## [Level 13 -> Level 14](https://overthewire.org/wargames/bandit/bandit14.html)

```
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

I literally copied this to my local machine in a file text file and renamed it `sshkey.private` (stored in directory `14`). Then I ran this command to access the next server:

```bash
ssh -i 14/sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
```

* [Log in with an SSH private key](https://docs.rackspace.com/support/how-to/logging-in-with-an-ssh-private-key-on-linuxmac)

* I'm sure there could have been a way to download a copy of the SSH key, but I'm lazy
  * copying the text worked just fine

## [Level 14 -> Level 15](https://overthewire.org/wargames/bandit/bandit15.html)

Login with this command:

```bash
ssh -i 14/sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
```

