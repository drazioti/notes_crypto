# Quadratic Sieve
## B-smooth
Θέτουμε $\psi(x,B)$ το πλήθος των θετικών ακέραιων που είναι $B-smooth$ και $\le x$. Πχ $\psi(x,B)=x,$ για $x\le B$. Αφού όλοι οι αριθμοί που είναι
$\le B$ είναι $B-smooth.$ Eνδιαφερόμαστε για την περίπτωση $B=x^{1/u}.$ Έχει αποδειχτεί ότι
$$\psi(x,x^{1/u})=\rho(u) x + Ο(x/ln{x}),$$
όπου $\rho(u)$ η συνάρτηση των Dickman–de Bruijn,η οποία ικανοποιεί

$$\rho'(u) u=\rho(u-1), u>1 \ και\ \rho(u)=1, 0\le u\le 1. $$

<p align="center">
<img width="282" height="197" alt="Screenshot 2026-07-22 at 14 22 19" src="https://github.com/user-attachments/assets/1e403675-8cd4-4a27-8323-f069d55a543d" />
</p>

Στην συνάρτηση $\psi(x,y)$ ο λόγος $u=\frac{\ln x}{\ln y}$ λέγεται παράμετρος του Dickman.

## Quadratic Sieve
O Quadratic Sieve παράγει $B-$smooth ακεράιους με την εφαρμογή ενός sieving. Αντι να υπολογιζει την παραγοντοποίηση
του $x^2\pmod{n}$ υπολογίζει την παραγοντοποίηση του $x^2-n$. 

| # | x | Factorization x^2-n | B-smooth |
|--:|------:|---------------|:--------:|
| 1  | 243 | $2^3 \cdot 31$ | False |
| 2  | 242 | $-1 \cdot 3 \cdot 79$ | False |
| 3  | 244 | $3 \cdot 5 \cdot 7^2$ | True |
| 4  | 241 | $-1 \cdot 2^4 \cdot 3^2 \cdot 5$ | True |
| 5  | 245 | $2^3 \cdot 3^2 \cdot 17$ | True |
| 6  | 240 | $-1 \cdot 1201$ | False |
| 7  | 246 | $5 \cdot 7^3$ | True |
| 8  | 239 | $-1 \cdot 2^4 \cdot 3 \cdot 5 \cdot 7$ | True |
| 9  | 247 | $2^5 \cdot 3 \cdot 23$ | True |
| 10 | 238 | $-1 \cdot 3 \cdot 719$ | False |
| 11 | 248 | $3 \cdot 17 \cdot 53$ | False |
| 12 | 237 | $-1 \cdot 2^3 \cdot 7 \cdot 47$ | False |
| 13 | 249 | $2^7 \cdot 5^2$ | True |
| 14 | 236 | $-1 \cdot 3^3 \cdot 5 \cdot 23$ | True |

και 

| # | Value | Factorization | B-smooth |
|--:|------:|---------------|:--------:|
| 1 | 244 | $3 \cdot 5 \cdot 7^2$ | True |
| 2 | 241 | $-1 \cdot 2^4 \cdot 3^2 \cdot 5$ | True |
| 3 | 245 | $2^3 \cdot 3^2 \cdot 17$ | True |
| 4 | 246 | $5 \cdot 7^3$ | True |
| 5 | 239 | $-1 \cdot 2^4 \cdot 3 \cdot 5 \cdot 7$ | True |
| 6 | 247 | $2^5 \cdot 3 \cdot 23$ | True |
| 7 | 249 | $2^7 \cdot 5^2$ | True |
| 8 | 236 | $-1 \cdot 3^3 \cdot 5 \cdot 23$ | True |

Μετά συνεχίζουμε όπως και στον Dixon.

Σχηματίζουμε τον πίνακα,

$$M=
\begin{bmatrix}
0 & 0 & 1 & 0 & 1 & 1 & 0 \\
1 & 0 & 0 & 0 & 1 & 0 & 1 \\
1 & 1 & 0 & 1 & 0 & 0 & 1 \\
1 & 0 & 0 & 1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 1 & 0 & 1
\end{bmatrix}
$$

που οι γραμμές αντιστοιχούν στους εκθέτες [2,3,5,7,17,23].

Βρίσκουμε μια λύση

$$(0,1,0,0,1,1,1).$$

Δηλ. οι στήλες 2,5,6,7 είναι γ.ε. mod2.


Οπότε έχουμε,

$x^2=2^{16}\cdot 3^{6}\cdot 5^4\cdot 23^2$ άρα 
$x=2^{8}\cdot 3^{3}\cdot 5^2\cdot 23$ και 
$y=241\cdot 247\cdot 249\cdot 236$ και τέλος
$gcd(x+y,n)=127.$

## sage code
Ακολουθεί ο κώδικας sage που παράχθηκε ο πίνακας.

```python

def alternating_range(x: int, y: int):
    if x >= y:
        raise ValueError("x must be smaller than y")
    yield x # print the initial value x
    for distance in range(1, y - x + 1):
        yield x - distance # x-1,x-2,...
        yield x + distance # x+1,x+2,...

def is_B_smooth(B,x):
    S=prime_factors(x)
    if max(S)<=B:
        return True
    else:
        return False


n = 58801
B = 23
K=[]
k=prime_pi(B)
temp = ceil(sqrt(n))
i=1 # counting index
s=0 # success
for x in alternating_range(temp, temp+10):
    z =x^2-n
    if is_B_smooth(B,z):
        s+=1
        K.append([s,x,factor(z),is_B_smooth(B,z)])
    print(i,x,factor(z),is_B_smooth(B,z))
    i+=1
    if s==k-1:
        break
K
```
