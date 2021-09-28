# General Skills Quiz
>QUIZ TIME! Just answer the questions. Pretty easy right?

>Author: Crem

>nc pwn-2021.duc.tf 31905

![image](https://user-images.githubusercontent.com/62060867/135068514-7ca3b864-5cfd-4211-afcc-7cfef5454b09.png)


This challenge requires you to decode and encode using different popular formats such as base64, binary and ROT13,..... Not enough time is given to do those manually.
There are 11 challenges in total and then you will receive the flag.

```
from pwn import *
import binascii
import codecs
from urllib.parse import unquote
import base64
import codecs

host = "pwn-2021.duc.tf"
port = 31905
s = remote(host,port)
s.recvline()
s.sendline("y")
s.recvline()
s.sendline("2")
s.recvuntil("(base 10): ")
hex_code = (s.recv(1024)).strip()
a = int(hex_code, 16)
s.sendline(str(a))
s.recvuntil("letter: ")
hex_code2 = (s.recv(1024)).strip()
b = hex_code2.decode('utf-8')
c = binascii.unhexlify(b)
s.sendline(c.decode('utf-8'))
s.recvuntil("symbols: ")
url = s.recv(1024).strip().decode('utf-8')
url = unquote(url)
s.sendline(url)
s.recvuntil("plaintext: ")
d = s.recv(1024).strip().decode('utf-8')
e = base64.b64decode(d).decode('utf-8')
s.sendline(e)
s.recvuntil("Base64: ")
f = s.recv(1024).strip().decode('utf-8')
g = base64.b64encode(f.encode('utf-8'))
s.sendline(g)
s.recvuntil("plaintext: ")
h = s.recv(1024).strip().decode('utf-8')
k = codecs.decode(h, 'rot_13')
s.sendline(k)
s.recvuntil("equilavent: ")
l = s.recv(1024).strip().decode('utf-8')
m = codecs.encode(l, 'rot_13')
s.sendline(m)
s.recvuntil("(base 10): ")
binary_code = (s.recv(1024)).strip().decode('utf-8')[2:]
n = int(binary_code, 2)
s.sendline(str(n))
s.recvuntil("equivalent: ")
o = s.recv(1024).strip().decode('utf-8')
o1 = bin(int(o))
s.sendline(o1)

s.interactive()
```
```
python3 ganeralskill.py                                                                               148 ⨯ 2 ⚙
[+] Opening connection to pwn-2021.duc.tf on port 31905: Done
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:12: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline("y")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:14: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline("2")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:15: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("(base 10): ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:18: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(str(a))
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:19: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("letter: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:23: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(c.decode('utf-8'))
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:24: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("symbols: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:27: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(url)
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:28: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("plaintext: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:31: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(e)
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:32: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("Base64: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:36: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("plaintext: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:39: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(k)
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:40: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("equilavent: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:43: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(m)
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:44: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("(base 10): ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:47: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(str(n))
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:48: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.recvuntil("equivalent: ")
/home/kali/Desktop/sherlock/sherlock/ganeralskill.py:51: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  s.sendline(o1)
[*] Switching to interactive mode
You're better than a bunnings sausage sizzle.

Final Question, what is the best CTF competition in the universe?
$ DUCTF
Bloody Ripper! Here is the grand prize!



   .^.
  (( ))
   |#|_______________________________
   |#||##############################|
   |#||##############################|
   |#||##############################|
   |#||##############################|
   |#||########DOWNUNDERCTF##########|
   |#||########(DUCTF 2021)##########|
   |#||##############################|
   |#||##############################|
   |#||##############################|
   |#||##############################|
   |#|'------------------------------'
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|
   |#|  DUCTF{you_aced_the_quiz!_have_a_gold_star_champion}
   |#|
   |#|
   |#|   
  //|\\

``
