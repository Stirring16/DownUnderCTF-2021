# Substitution Cipher I

>Just a simple substitution cipher to get started...

>Author: joseph#8210

[output.txt](https://github.com/Stirring16/DownUnderCTF-2021/files/7248206/output.txt)

```
def encrypt(msg, f):
    return ''.join(chr(f.substitute(c)) for c in msg)

P.<x> = PolynomialRing(ZZ)
f = 13*x^2 + 3*x + 7

FLAG = open('./flag.txt', 'rb').read().strip()

enc = encrypt(FLAG, f)
print(enc)

```
When we read this script carefully we can see that it basically just calculates the formula

![image](https://user-images.githubusercontent.com/62060867/135187505-3d282ce9-5d10-4703-8015-352f4cd2c423.png)

## Solution 

```
from sympy import *
x = symbols('x')
from sympy import roots, solve_poly_system

def decrypt(msg):
    final = []
    for letter in msg:
        equation = 13*x**2 + 3*x + 7 - ord(letter)
        solution = solve(equation, x)        
        final.append(chr(solution[1]))
    return ''.join(final)


FLAG = "𖿫𖝓玲𰆽𪃵𢙿疗𫢋𥆛🴃䶹𬑽蒵𜭱𫢋𪃵蒵🴃𜭱𩕑疗𪲳𜭱窇蒵𱫳"
print(decrypt(FLAG))
```

> So we got the flag: `DUCTF{sh0uld'v3_us3d_r0t_13}`

