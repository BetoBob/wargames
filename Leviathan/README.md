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

Looking at the `.dot` files, there is a hidden directory called `.backup` in the `/leviathan0/` directory.

In it, is a `bookmarks.html` files, which had a list of a bunch of links to interesting websites.

I tried to download it with `scp` to view the HTML file locally, but it didn't work. So I opened the file with `cat`, and did a mass copy / past of it to view it locally. This step probably could have been done a lot better because it's a pretty big file to manually copy over.

So I key search `password` and find a link to "password for leviathan1", which gives me the password below. 

And now that I think about it, I could have searched for the password locally using a tool like `grep` or a file reader with word search functionality. But I found the password anyways! And that's what matters.

**Level 1 Password**

```
rioGegei8m
```

## Level 1 -> Level 2

* in the directory is a file called `check`
* it appears to be some sort of executable:

```bash
check: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=c735f6f3a3a94adcad8407cc0fda40496fd765dd, not stripped
```

I feel like this involves exploring the executable file somehow. I have a feeling that the password might be hard-coded into the file and I need to find it. This is what the strings of the executable look like, but so far I am not having much luck finding a string that looks like a password. I see a reference to `strcmp`, but no password variable associated with it. Here are the file's strings:

```bash
leviathan1@leviathan:~$ strings check
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
puts
setreuid
printf
getchar
system
geteuid
strcmp
__libc_start_main
__gmon_start__
GLIBC_2.0
PTRhp
QVh;
secrf
love
UWVS
t$,U
[^_]
password:
/bin/sh
Wrong password, Good Bye ...
;*2$"
GCC: (Debian 6.3.0-18+deb9u1) 6.3.0 20170516
crtstuff.c
__JCR_LIST__
deregister_tm_clones
__do_global_dtors_aux
completed.6587
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
check.c
__FRAME_END__
__JCR_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
strcmp@@GLIBC_2.0
__x86.get_pc_thunk.bx
printf@@GLIBC_2.0
getchar@@GLIBC_2.0
_edata
geteuid@@GLIBC_2.0
__data_start
puts@@GLIBC_2.0
system@@GLIBC_2.0
__gmon_start__
__dso_handle
_IO_stdin_used
setreuid@@GLIBC_2.0
__libc_start_main@@GLIBC_2.0
__libc_csu_init
_fp_hw
__bss_start
main
__TMC_END__
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rel.dyn
.rel.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.jcr
.dynamic
.got.plt
.data
.bss
.comment
```

This [StackExchange post](https://unix.stackexchange.com/questions/194521/open-read-unix-executable-file) gives a pretty helpful overview of various commands I can use to explore an executable file.

One thing I can do is use `objdump` to view some of the assembly commands of the executable. However I cannot see any strings in this

