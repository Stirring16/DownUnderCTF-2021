# Substitution Cipher II

> That's an interesting looking substitution cipher...

> Author: joseph#8210

 [output2.txt](https://github.com/Stirring16/DownUnderCTF-2021/files/7248227/output2.txt)
 
 
```
from string import ascii_lowercase, digits
CHARSET = "DUCTF{}_!?'" + ascii_lowercase + digits
n = len(CHARSET)

def encrypt(msg, f):
    ct = ''
    for c in msg:
        ct += CHARSET[f.substitute(CHARSET.index(c))]
    return ct

P.<x> = PolynomialRing(GF(n))
f = P.random_element(6)

FLAG = open('./flag.txt', 'r').read().strip()

enc = encrypt(FLAG, f)
print(enc)

```

## Solution

I find that the polynomial is:  `f(x) = 41x^6 + 15x^5 + 40x^4 + 9x^3 + 28x^2 + 27x + 1`

My code for the equation:


```
from numba import jit

@jit(nopython=True)
def main():
    x=0
    for a in range(47):
        for b in range(47):
            for c in range(47):
                for d in range(47):
                    for e in range(47):
                        for f in range(47):
                            if (a+b+c+d+e+f+1)%47 == 20 and (64*a+32*b+16*c+8*d+4*e+2*f+1)%47 == 35 and (729*a+243*b+81*c+27*d+9*e+3*f+1)%47 == 33 and (4096*a+1024*b+256*c+64*d+16*e+4*f+1)%47 == 42 and (15625*a+3125*b+625*c+125*d+25*e+5*f+1)%47 == 14 and (46656*a+7776*b+1296*c+216*d+36*e+6*f+1)%47 == 41:
                                print(a,b,c,d,e,f)
    print('done')

main()
```
lol I brute forced it

I dont think i was supposed to but it works

```
┌──(kali㉿kali)-[~/Desktop/DUCTF/CipherII]
└─$python3 CipherII.py
41 15 40 9 28 27
done
```

Then we can brute force the flag 
I used this [https://sagecell.sagemath.org/](https://sagecell.sagemath.org/)

```
from string import ascii_lowercase, digits
CHARSET = "DUCTF{}_!?'" + ascii_lowercase + digits
n = len(CHARSET)

def encrypt(msg, f):
    ct = ''
    for c in msg:
        ct += CHARSET[f.substitute(CHARSET.index(c))]
    return ct

P.<x> = PolynomialRing(GF(n))
f = 41*x^6 + 15*x^5 + 40*x^4 + 9*x^3 + 28*x^2 + 27*x + 1

FLAG = "DUCTF{"

enc = encrypt(FLAG, f)
print(enc)
print('Ujyw5dnFofaou0au3nx3Cn84')
```
![image](https://user-images.githubusercontent.com/62060867/135188788-54d7770a-980a-431b-b81b-bf4b280a39c9.png)

> So we got the flag: `DUCTF{go0d_0l'_l4gr4fg3}`



