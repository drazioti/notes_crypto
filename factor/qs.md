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
| 1  | 243 | $3^5$ | **True** |
| 2  | 242 | $2 \cdot 11^2$ | **True** |
| 3  | 244 | $2^2 \cdot 61$ | False |
| 4  | 241 | $241$ | False |
| 5  | 245 | $5 \cdot 7^2$ | **True** |
| 6  | 240 | $2^4 \cdot 3 \cdot 5$ | **True** |
| 7  | 246 | $2 \cdot 3 \cdot 41$ | False |
| 8  | 239 | $239$ | False |
| 9  | 247 | $13 \cdot 19$ | False |
| 10 | 238 | $2 \cdot 7 \cdot 17$ | **True** |
| 11 | 248 | $2^3 \cdot 31$ | False |
| 12 | 237 | $3 \cdot 79$   | False |
| 13 | 249 | $3\cdot 83$    | False |
| 14 | 236 | $2^2\cdot 59$   | False |
| 15 | 250 | $2\cdot 5^3$ |**True**|

Ακολουθεί ο κώδικας sage που παράχθηκε ο πίνακας.

```python

def alternating_range(x: int, y: int):
    """Generate x, x-1, x+1, x-2, x+2, ... until x+y."""
    if x >= y:
        raise ValueError("x must be smaller than y")

    yield x  # Initial value

    for distance in range(1, y - x + 1):
        yield x - distance  # x-1, x-2, ...
        yield x + distance  # x+1, x+2, ...


def is_B_smooth(B, x):
    """Return True if x is B-smooth."""
    S = prime_factors(x)
    return max(S) <= B


n = 58801
B = 17
temp = ceil(sqrt(n))

i = 1  # Row index
s = 0  # Number of B-smooth values found

for x in alternating_range(temp, temp + 10):
    if is_B_smooth(B, x):
        s += 1

    print(i, x, factor(x), is_B_smooth(B, x))
    i += 1

    if s == 5:
        break
```

Μετά συνεχίζουμε όπως και στον Dixon.

