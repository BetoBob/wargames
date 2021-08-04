# [Bandit](https://overthewire.org/wargames/bandit/)

## Setup

Go to Bandit directory in PowerShell. Open the Github folder and type `powershell` in the address bar to start a session in the working directory.

PowerShell will be used because it has more features then command prompt. A big missing feature in command prompt is command history, which is especially helpful when commands are repeated, like the `ssh` command with the server address.

It also is optimal because it has less overhead than working in the Linux subsystem. If necessary, I can switch to a subsystem environment from PowerShell running the `bash` command. 

## Resources

Below is a good set of solutions explaining how to approach these problems:

<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLBf0hzazHTGOIn_vuuuCzRFVhYiDBnJID" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Even if I find a solution, it might be good to look up solutions occasionally to see if there was a more intuitive way to approach my problem.

## Level 0

* needed to take port number into account when using SSH
* https://superuser.com/questions/1536983/stuck-in-bandit-level-0-overthewire-org

```
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

* solution used for this problem

## Level 0 -> Level 1

* logging to a new user for each level:

```bash
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

```bash
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

* changing the `-p` flag to `30000` does not resolve this issue

First, I need to find the password of the current server I am in. I currently only have the SSH key for the server I am in, not the actual password itself.

I had to look up how to find the password for each level. Initially I thought I had to use a `sudo` command to check my user's password info. However in the README of the servers, it states that each game's password is stored in `/etc/bandit_pass`:

```
--[ Playing the games ]--

  This machine might hold several wargames.
  If you are playing "somegame", then:

    * USERNAMES are somegame0, somegame1, ...
    * Most LEVELS are stored in /somegame/.
    * PASSWORDS for each level are stored in /etc/somegame_pass/.
```

```bash
bandit14@bandit:~$ ls -l /etc/bandit_pass/
total 136
-r-------- 1 bandit0  bandit0   8 May  7  2020 bandit0
-r-------- 1 bandit1  bandit1  33 May  7  2020 bandit1
-r-------- 1 bandit10 bandit10 33 May  7  2020 bandit10
-r-------- 1 bandit11 bandit11 33 May  7  2020 bandit11
-r-------- 1 bandit12 bandit12 33 May  7  2020 bandit12
-r-------- 1 bandit13 bandit13 33 May  7  2020 bandit13
-r-------- 1 bandit14 bandit14 33 May  7  2020 bandit14
-r-------- 1 bandit15 bandit15 33 May  7  2020 bandit15
...
```

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

So now that I have that password, I just need to submit it to 30000 from the localhost of `bandit14`:

```bash
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

The tool [`nc` (short for `netcat`)](https://en.wikipedia.org/wiki/Netcat) is used to read and write to network ports using TCP or UDP. The command literally just opens up the localhost 30000 for listening, then you send the password through standard input. This will definitely be a tool I will want to learn in the future. As [Wikipedia](https://en.wikipedia.org/wiki/Netcat) says:

> **netcat** (often abbreviated to **nc**) is a computer networking utility for reading from and writing to network connections using [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) or [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol). The [command](https://en.wikipedia.org/wiki/Command_(computing)) is designed to be a dependable [back-end](https://en.wikipedia.org/wiki/Front_and_back_ends) that can be used directly or easily driven by other programs and  scripts. At the same time, it is a feature-rich network debugging and  investigation tool, since it can produce almost any kind of connection  its user could need and has a number of built-in capabilities.
>
> Its list of features includes port scanning, transferring files, and port listening: as with any server, it can be used as a [backdoor](https://en.wikipedia.org/wiki/Backdoor_(computing)).

* I had to look up the solution for this challenge

## [Level 15 -> Level 16](https://overthewire.org/wargames/bandit/bandit16.html)

Because this seemed a lot like the previous question, I looked up how to use `nc` with SSL encryption.

I found a [StackExchange post](https://serverfault.com/questions/476068/can-netcat-talk-to-an-encrypted-port) about using `nc` to access a port with SSL, and they recommended to use `openssl` instead. So I configured the command in the StackExchange post to use `localhost` on port `30001`, and got the solution I was looking for:

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICBjCCAW+gAwIBAgIEfftLGTANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDDAls
b2NhbGhvc3QwHhcNMjEwNDEzMDgzODA3WhcNMjIwNDEzMDgzODA3WjAUMRIwEAYD
VQQDDAlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMLfXBVa
jVKDHlA3U+S0hBMJMJlfue3xKECpmx1Ajp4/khUuWwvPB7+wLjqasBO2WfFYJzcq
z9t7FfAPIlYjgvOTQs5X4vQ1aGzanvnNn+1VknpOnFAJQBSFq6ZD3ipWrhwm9XZq
8CgFhTGp9IPthZp8Y0B7OgobhlMtXD/zLaTbAgMBAAGjZTBjMBQGA1UdEQQNMAuC
CWxvY2FsaG9zdDBLBglghkgBhvhCAQ0EPhY8QXV0b21hdGljYWxseSBnZW5lcmF0
ZWQgYnkgTmNhdC4gU2VlIGh0dHBzOi8vbm1hcC5vcmcvbmNhdC8uMA0GCSqGSIb3
DQEBBQUAA4GBAMFH9rsZovwnb5k71/MpyCnXEwGlIhixUu6qfi1kiFvhJ6lJCvaO
weOYxV4oJy1OEB0LSEAQOnSPfzC8dDasijFcdVhuIGGPuQ2GZ05nCiiIZUNnrMRB
0z2RuRxgxMVjOvcSIJyvwyjVH4jY4I434fMyldePLxO1POLd1cxoKNTO
-----END CERTIFICATE-----
subject=/CN=localhost
issuer=/CN=localhost
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 1019 bytes and written 269 bytes
Verification error: self signed certificate
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 1024 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: FF036EB2E84C3E2FFC3144D0CC91E196CB37ECC7946B61F0371B0AE7F4912B65
    Session-ID-ctx:
    Master-Key: 3069616FB2173090851F17C9FBCFCF350728DC320908E6D18043D72400ECEAC83015CD83C10E6E2BA7B055A9F73F2297
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - f2 5b 83 7e f0 ca 58 ca-aa f3 8f 83 b9 65 d5 23   .[.~..X......e.#
    0010 - dc 45 65 70 d3 a6 e4 19-23 34 4f 84 8a d0 13 0b   .Eep....#4O.....
    0020 - 57 70 4b 9c 82 7c 45 ad-e7 c7 71 60 9b 90 45 25   WpK..|E...q`..E%
    0030 - fc 94 9e 1d 47 9a 97 43-01 4a b1 5f 61 92 fe de   ....G..C.J._a...
    0040 - 54 83 5c 95 10 08 64 1b-3c 7e 15 93 63 0e b2 bf   T.\...d.<~..c...
    0050 - ee a9 ab eb 86 01 89 38-91 6d 86 de 07 6e 6f 9f   .......8.m...no.
    0060 - a6 4b 42 3a e1 4f f6 96-3f 90 ca c6 d0 d7 6a a8   .KB:.O..?.....j.
    0070 - 97 a1 b9 5e ac 16 0f 1a-1f f1 0e af f9 03 96 7a   ...^...........z
    0080 - b4 ea 23 69 10 00 0f d2-27 6c ea 9f 45 9f 2a 1f   ..#i....'l..E.*.
    0090 - 35 d9 4e 2c b8 6d 06 7d-14 6b 0f 60 e4 00 f7 22   5.N,.m.}.k.`..."

    Start Time: 1626221773
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
```

My solution works great! But as a follow-up I decided to see what other people did for solutions, and it turns out `ncat` does have an `--ssl` flag that can be used. This was what was used in [HackerSploit's walkthrough](https://youtu.be/q1c8yiMu_24).

### SSL Explanation

A brief description of OpenSSL from the man pages:

> OpenSSL is a cryptography toolkit implementing the Secure Sockets Layer (SSL v2/v3) and Transport Layer Security (TLS v1) network protocols and related cryptography standards required by them. The openssl program is a command line tool for using the various cryptography functions of OpenSSL's crypto library from the shell.

<iframe width="560" height="315" src="https://www.youtube.com/embed/rROgWTfA5qE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



According to the video above, SSL is what makes the 's' in `https` secure. `https` is secure in two ways:

1. data encryption, so only the client and server share information (no intercepted data); this encryption method is **SSL**
2. certificates, issued by a certificate authority to verify if a website is what it claims to be
   * these certificates can be verified by several different authorities (ex: Google Trust Services LLC,  [Let's Encrypt](https://letsencrypt.org/) (a TLS certificate nonprofit), Cloudflare)
     * typically big tech companies like Google, Microsoft, Apple have their own certification services for their websites

**Password for Level 16**

```
cluFn7wTiGryunymYOu4RcffSxQluehd
```

## [Level 16 -> Level 17](https://overthewire.org/wargames/bandit/bandit17.html)

> The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. 

```bash
cat /usr/share/nmap/nmap-services | grep "\W31.*/"
```

Running the command above will give you a description of all ports from `31000` to `32000`, excluding `32000` because my regular expression is too lazy to include it. This is still a bit too much information. I could remove the ports that are listed as "unknown" , but there are still a lot of used ports to explore. This was still helpful to get an idea of what some of the higher level ports are doing, and got the command idea from [this article](https://www.plesk.com/blog/various/open-ports-in-linux/).

I think the next best thing to do is see all the servers running SSL encryption, and just select the one that is in the 31000 to 32000 range. After that, I will just use the same command as last time.

I want to use `netstat` for this solution, because it's a common tool used in forums. However I don't think it's compatible on this server. Here's what happens when I run a command to see ports:

```bash
bandit16@bandit:~$ netstat -t -l -p
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
netstat: no support for `AF INET (tcp)' on this system.
```

Same thing happens with `udp`. Also, `netstat` is not listed as a command to use for this exercise.

I am going to do something stupid. I am going to loop through all the ports with `openssl` and attempt to give it the password using a bash script:

```bash
for ((i = 1000 ; i <= 2000 ; i++)); do
  echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -connect "localhost:3$i"
done > /tmp/beto/results
```

When looking through the results, I saw some connections were established. However, none of the output appeared to show a 'Correct!' acknowledgement message. Because this is getting tricky, I am going to look at a walkthrough for guidance.

### [HackerSploit Solution](https://youtu.be/q1c8yiMu_24)

To check for ports used, [HackerSploit](https://youtu.be/q1c8yiMu_24) used the following `nmap` command:

```
bandit16@bandit:~$ nmap localhost -p 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2021-07-14 23:50 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00023s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds
```

Now I am test each of these ports using the following SSL command:

```
 openssl s_client -connect localhost:[port]
```

* `31046`: connects but closes
* `31518`: just repeats the password given by the user
* `31691`: connects but closes
* `31790`: returns an RSA Key

I copied that RSA key and am now using it for the next level. I am still not sure why the brute force method did not work. It appears some of the connections were made. Anyways, I hope through some other tutorials that I will learn more about port scanning in the future! This was a good first exposure to it, but I definitely want to get more familiar with `nmap` and `openssl`.

## [Level 17 -> Level 18](https://overthewire.org/wargames/bandit/bandit18.html)

This one is pretty chill:

```bash
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

**Password for Level 18**

```
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

## [Level 18 -> Level 19](https://overthewire.org/wargames/bandit/bandit19.html)

* I looked up how to do commands immediately upon login
* then looked at another post about `bash.rc` and an alternative is to start another shell up using `/bin/sh`

```powershell
ssh -p 2220 bandit18@bandit.labs.overthewire.org -t "/bin/sh"
```

At the end of the `.bashrc` file is this:

```bash
echo 'Byebye !'
exit 0
```

**Password for Level 19**

```
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

## [Level 19 -> Level 20](https://overthewire.org/wargames/bandit/bandit20.html)

* each bandit level password has it's access restricted to it's associated level

```bash
bandit19@bandit:~$ ls -l /etc/bandit_pass/bandit20
-r-------- 1 bandit20 bandit20 33 May  7  2020 /etc/bandit_pass/bandit20
bandit19@bandit:~$ cat /etc/bandit_pass/bandit20
cat: /etc/bandit_pass/bandit20: Permission denied
```

* the `./bandi20-do` executable is a program that lets you act with permissions of user `bandit20`

```bash
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```

```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

* never actually had to use `setuid` for this level; my guess is that it was part of the program provided in the executable

**Password for Level 20**

```
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

## [Level 20 -> Level 21](https://overthewire.org/wargames/bandit/bandit21.html)

The wording on this one was kind of confusing. Basically what I had to do was:

1. Open a free port an send the text of the password to it

```bash
bandit20@bandit:~$ echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l -p 1234
```

I chose `1234` because [HackerSploit](https://youtu.be/uFxs3wzgDGU) recognized that it was a common available port. So I did receive quite a bit of help to figure this one out, but attempted to write my own command. I also found out how to use `netcat` for this task using this [StackExchange post](https://askubuntu.com/questions/443227/sending-a-simple-tcp-message-using-netcat).

2. In another shell, use the `./suconnect` command to connect to the port you sent the password to

```bash
bandit20@bandit:~$ ./suconnect 1234
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

3. The `./suconnect` will confirm it received the password, and send the next password to the open port (the first shell created) and close the connection.

**Password for Level 21**

```
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

## [Level 21 -> Level 22](https://overthewire.org/wargames/bandit/bandit22.html)

```bash
bandit21@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

**Password for Level 22**

```
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

## [Level 22 -> Level 23](https://overthewire.org/wargames/bandit/bandit23.html)

```bash
bandit22@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

**Goal:** run that target bash command to get the tmp folder name

```bash
mytarget=$(echo I am user bandit22 | md5sum | cut -d ' ' -f 1)
```

```bash
bandit22@bandit:~$ mytarget=$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)
bandit22@bandit:~$ cat /tmp/$mytarget
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

**Password for Level 23**

```
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

## [Level 23 - > Level 24](https://overthewire.org/wargames/bandit/bandit24.html)

```
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

```bash
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

My updates:

* we have to pretend we are `bandit24`, because there is no `bandit23` directory in `/var/spool/`

```bash
myname="bandit24"

cd /var/spool/$myname
pwd
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

Where I get stuck is in modifying the script to execute commands in the `var/spool/bandit24` directory. I get an error message stating that `.*` can't be executed, meaning that the bash script is not able to see all the contents in the directory, or else the `.*` would have expanded to all the files in the directory. I'm guessing this occurs because I do not have read access to the directory, but I do have write and execute access to it.

```bash
bandit23@bandit:~$ /tmp/beto/test.sh
/var/spool/bandit24
Executing and deleting all scripts in /var/spool/bandit24:
Handling *
stat: cannot stat './*': No such file or directory
Handling .*
stat: cannot stat './.*': No such file or directory
```

After seeing the beginning of a tutorial, I understand what needs to be done. We do not need to recreate the script. We need to send a copy of a bash script we want to execute in the `/var/spool/bandit24` directory to copy the password of `bandit24` to the directory we want.

```bash
cp /etc/bandit_pass/bandit24 /tmp/beto/bandit24
chmod 777 /tmp/beto/bandit24
```

Also make sure to `chmod 777` both `/tmp/beto/` and `test.sh` so `bandit24` can execute the file given to it and has write permission for the temp directory you are working in.

```bash
bandit23@bandit:/tmp/beto$ cat bandit24
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

## [Level 24 -> Level 25](https://overthewire.org/wargames/bandit/bandit25.html)

I plan on using a previous Bash loop I made as a template for this exercise. First I looked up how to make a loop of numbers with leading zeros. Thanks [StackOverflow](https://stackoverflow.com/questions/18460123/how-to-add-leading-zeros-for-for-loop-in-shell)!

```
for i in {0000..9999}; do echo "$i"; done
```

Naive solution:

```bash
for i in {0000..9999}; do
  echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i" | nc localhost 30002
done > /tmp/beto/results
```

The problem with the solution above is that it re-establishes the connection to the daemon each time I try a new password. However the daemon does not exit when the wrong password is given. So the program above will hang on the first code. Therefore, it's better to generate the input before connecting to the server, then piping it to the daemon all at once:

```bash
for i in {0000..9999}; do
  echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i"
done | nc localhost 30002 # > /tmp/beto/results
```

Result:

```bash
...
Wrong! Please enter the correct pincode. Try again.
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.
```

## [Level 25 -> Level 26](https://overthewire.org/wargames/bandit/bandit26.html)

Initially, my thoughts are to do the exact same thing as I did with the startup script that would log me out. (Level 18 -> Level 19)

```bash
ssh -i 26/bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org -t "/bin/sh"
```

```powershell
PS C:\Users\_\Documents\GitHub\wargames\Bandit> ssh -i 26/bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org -t "/bin/sh"
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
Connection to bandit.labs.overthewire.org closed.
```

As expected, this is not helping me out.

The `.dot` files look pretty normal:

```bash
bandit25@bandit:~$ ls -al /home/bandit26/
total 36
drwxr-xr-x  3 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rwsr-x---  1 bandit27 bandit26 7296 May  7  2020 bandit27-do
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
drwxr-xr-x  2 root     root     4096 May  7  2020 .ssh
-rw-r-----  1 bandit26 bandit26  258 May  7  2020 text.txt
bandit25@bandit:~$ diff .bashrc /home/bandit26/.bashrc
bandit25@bandit:~$ diff .profile /home/bandit26/.profile
bandit25@bandit:~$ diff .bash_logout /home/bandit26/.bash_logout
bandit25@bandit:~$
```

Nothing abnormal in `.ssh` directory either. 

Dumb idea, I could lookup the text for that mysterious `bandit26` keyart.

```
grep -rnw '/' -e $(cat art.txt) --no-messages
```

```
Binary file /proc/config.gz matches
```

I don't think grepping that phrase will help me out. 

So lets find out how to find which shell the user is using. After googling this, it appears to be stored in the `/etc/passwd` file.

>The **/etc/passwd** file stores essential  information, which required during login. In other words, it stores user account information. The /etc/passwd is a plain text file. It contains a list of the system’s accounts, giving for each account some useful  information like user ID, group ID, home directory, shell, and more. The /etc/passwd file should have general read permission as many command  utilities use it to map user IDs to user names. However, write access to the /etc/passwd must only limit for the superuser/root account. 

* [article on `/etc/passwd`](https://www.cyberciti.biz/faq/understanding-etcpasswd-file-format/)

```bash
bandit25@bandit:~$ cat /etc/passwd | grep -F "bandit26"
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

So it basically opens up the `text.txt` file before immediately closing. I'm guessing this `text.txt` file is the ASCII art.

Had to look up the solution to this. So basically, `more` uses a version of `vim` to display text to the screen. `vim` has a feature if you press `v` where you can execute commands within vim using the `:e command`. `more` will only enter this `vim` mode if the shell screen is small enough. Therefore you have to reduce the shell screen to a small height because the ASCII art is small. Then you can run a command to retrieve the password. I would have never guessed that on my own lol.

**Password for Bandit26**

```
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
```

## Level 26 -> Level 27

But in order to make `bandit26` usable, you still need to change the shell. So here are the steps to do that:

1. Decrease screen for `more` interface to appear
2. Hit `v` to enter `vim` mode (you can expand screen now)
3. In `vim` editor mode, type `:set shell=/bin/bash`
4. Type in `:shell` to exit `vim`

Once in, you have to grab the next bandit password for `bandit27` using a command that acts as a `bandit27` user, like in previous exercises:

```bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```

Overall I wish there were more hints for this exercise. Because you had to know ahead of time that `more` had a `vim` feature, and that `vim` has execution features within the editor, and that you can access `vim` if the `more` interface is fully utilized. However it was entertaining to learn how to approach this problem, and demonstrates how seemingly simple commands can have unexpected vulnerabilities if you look carefully through them.

Going forward, I don't mind looking up solutions as long as I:

1. understand what is going on in the solution 
2. enjoy seeing the process of watching a person's approach to tackling a task

## [Level 27 -> Level 28](https://overthewire.org/wargames/bandit/bandit28.html)

```bash
bandit27@bandit:/tmp/beto$ git clone "ssh://bandit27-git@localhost/home/bandit27-git/repo"
bandit27@bandit:/tmp/beto$ cd repo
bandit27@bandit:/tmp/beto/repo$ ls
README
bandit27@bandit:/tmp/beto/repo$ cat README
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2
```

## [Level 28 - > Level 29](https://overthewire.org/wargames/bandit/bandit29.html)

```bash
bandit28@bandit:/tmp/beto2/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx

```

* the password is 10 characters long? 
* or maybe it literally is `xxxxxxxxxx` lol (not the case)

* maybe the password is stored in an earlier version

```bash
bandit28@bandit:/tmp/beto2/repo$ git log -1
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak
```

```bash
bandit28@bandit:/tmp/beto2/repo$ git log
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak

commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data

commit de2ebe2d5fd1598cd547f4d56247e053be3fdc38
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    initial commit of README.md
```

```bash
bandit28@bandit:/tmp/beto2/repo$ git checkout -b c086d11a00c0648d095d04c089786efef5e01264
Switched to a new branch 'c086d11a00c0648d095d04c089786efef5e01264'
bandit28@bandit:/tmp/beto2/repo$ ls
README.md
bandit28@bandit:/tmp/beto2/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: bbc96594b4e001778eee9975372716b2
```

## [Level 29 -> Level 30](https://overthewire.org/wargames/bandit/bandit30.html)

```bash
bandit29@bandit:/tmp/beto4/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

I am looking at various branch types for this one: https://www.nobledesktop.com/learn/git/git-branches

```bash
bandit29@bandit:/tmp/beto4/repo$ git branch -r
  origin/HEAD -> origin/master
  origin/dev
  origin/master
  origin/sploits-dev
```

```bash
bandit29@bandit:/tmp/beto4/repo$ git checkout -b origin/dev
Switched to a new branch 'origin/dev'
bandit29@bandit:/tmp/beto4/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```

## [Level 30 -> Level 31](https://overthewire.org/wargames/bandit/bandit31.html)

Basically it's hidden in an obscure `git` feature called "tags". Not quite as fun of a challenge because it literally could be hidden in any random `git` feature.

```bash
bandit30@bandit:/tmp/betobob/repo$ git tag
secret
bandit30@bandit:/tmp/betobob/repo$ git show secret
47e603bb428404d265f59c42920d81e5
```

## [Level 31 -> Level 32](https://overthewire.org/wargames/bandit/bandit32.html)

```bash
bandit31@bandit:/tmp/beto/repo$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

* make the `key.txt` file as described
* have to remove `*.txt` from the `.gitignore` file

```bash
bandit31@bandit:/tmp/beto/repo$ git push
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
Counting objects: 6, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 491 bytes | 0 bytes/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'
```

**Level 32 Password**

```
56a9bf19c63d650ce78e6ec0354ee45e
```

## [Level 32 -> Level 33](https://overthewire.org/wargames/bandit/bandit33.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/8KFjql050gI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* there is an exploit using positional parameters
* basically, the first parameter (`sh`) can be run using `$0` because it's the first parameter, changing it to a default shell
  * you can take stuff a step further by typing `bash` after to have the traditional `bash` shell

* also didn't realize that I ended up in Level 33, I thought I was on the Level 32 server lol

```bash
bandit33@bandit:~$ cat /etc/bandit_pass/bandit33
c9c3199ddf4121b10cf581a98d51caee
```

