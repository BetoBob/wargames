# Bandit Training

https://overthewire.org/wargames/bandit/

I am going to use Powershell to run SSH commands because it saves command history accross sessions (so I don't need to re-type the SSH command repeatedly). ([source](https://superuser.com/questions/257855/keep-cmd-exe-command-history-between-sessions)) Sometime I should look up the differences between Powershell and Command Prompt lol. I think Powershell is meant more for IT professionals.

Below is a good set of solutions explaining how to approach these problems:

<iframe width="560" height="315" src="https://www.youtube.com/embed/ff2Au8BIy_A" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* potentially look into doing SSH keys if it's easy
  * might only need to set up SSH keys once if I am logging into the same sever over and over again, just with different credentials

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

