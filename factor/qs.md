# Quadratic Sieve
## B-smooth
Θέτουμε $\psi(x,B)$ το πλήθος των θετικών ακεραίων έως το $x$ που είναι $B$-smooth. Για παράδειγμα, αν $x\in\mathbb{N}$ και $x\le B$, τότε $\psi(x,B)=x$, αφού όλοι οι θετικοί ακέραιοι έως το $B$ είναι $B$-smooth.

Ενδιαφερόμαστε για την περίπτωση $B=x^{1/u}$. Ο Dickman (1930) απέδειξε ότι, για σταθερό $u>0$ και καθώς $x\to\infty$,

$$
\psi(x,x^{1/u})\sim x \rho(u),
$$

όπου $\rho(u)$ η συνάρτηση των Dickman–de Bruijn,η οποία ικανοποιεί

$$\rho'(u) u=-\rho(u-1), u>1 \ και\ \rho(u)=1, 0\le u\le 1. $$

O τύπος ισχύει για σταθερά $u>0,$ και μεγάλα $x.$

Το σύμβολο $\sim$ σημαίνει ότι

$$
\lim_{x\to\infty}\frac{\psi(x,x^{1/u})}{x \rho(u)}=1.
$$

<p align="center">
<img width="282" height="197" alt="Η συνάρτηση Dickman–de Bruijn" src="https://github.com/user-attachments/assets/1e403675-8cd4-4a27-8323-f069d55a543d" />
</p>

Ο λόγος

$$
u=\frac{\ln x}{\ln B}
$$

λέγεται παράμετρος του Dickman.

Με τη βοήθεια της $\psi(x,B)$ μπορούμε να υπολογίσουμε την πιθανότητα ένας ακέραιος $w$, που επιλέγεται ομοιόμορφα και τυχαία από το σύνολο $\{1,2,\ldots,x\}$, με $x\in\mathbb{Z}_{>0}$, να είναι $B$-smooth:

$$
\Pr(w\text{ είναι }B\text{-smooth})=\frac{\psi(x,B)}{x}.
$$

Αν $B=x^{1/u}$, για σταθερό $u>0$ και καθώς $x\to\infty$, έχουμε

$$
\frac{\psi(x,x^{1/u})}{x}\longrightarrow\rho(u).
$$

Συνεπώς, για μεγάλα $x$,

$$
\Pr(w\text{ είναι }B\text{-smooth})\approx\rho(u).
$$

Οι Canfield, Erdős και Pomerance απέδειξαν ότι, υπό κατάλληλες συνθήκες για τα $x,B$, ισχύει

$$
\psi(x,B)=x u^{-u(1+o(1))},
\qquad u=\frac{\ln x}{\ln B},
$$

όπου ο όρος $o(1)$ τείνει στο μηδέν καθώς $u\to\infty$, στο εύρος ισχύος του αποτελέσματος.

Επομένως, στο ίδιο εύρος,

$$
\Pr(w\text{ είναι }B\text{-smooth})
=\frac{\psi(x,B)}{x}
=u^{-u(1+o(1))}.
$$

Ως χονδρική προσέγγιση μπορούμε να γράψουμε

$$
\Pr(w\text{ είναι }B\text{-smooth})\approx u^{-u},
$$

αλλά όχι ασυμπτωτική ισοδυναμία με το $u^{-u}$.
(Δείτε 10.1.6 στο βιβλίο).
## Eισαγωγή
O Quadratic Sieve παράγει $B-$ smooth ακεραίους με την εφαρμογή ενός sieving. Αντι να υπολογίζει την παραγοντοποίηση
του $x^2\pmod{n}$ υπολογίζει την παραγοντοποίηση του $Q(x)=x^2-n$. To δεύτερο που κάνει ο αλγοριθμός αυτός είναι να μην υπολογίζει όλες τις παραγοντοποιήσεις του $x^2-n$ αλλά να "κοσκινίζει" (χωρίς να παραγοντοποιει) ώστε να εντοπίζει τους $B-$ smooth ακεραίους $Q(x).$ Παρακάτω, θα κάνουμε τον εντοπισμό των $B-$ smooth ακεραίων με πλήρη παραγοντοποίηση και σε δευτερη φάση θα δείξουμε το sieve. 

Θα ξεκινήσουμε με μια factor base που θα περιέχει και το -1, $F=[-1,2, 3, 5, 7, 17, 23].$ Μια ακόμη αλλαγή που θα κανουμε είναι ότι θα ξεκινήσουμε από το ceiling του $\sqrt{n}$ και θα αυξομειώνουμε τις τιμές.
 
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

και οι $B-$smooth είναι,

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
0 & 0 & 1 & 0 & 0 & 1 & 1 & 0 \\
1 & 0 & 0 & 0 & 1 & 1 & 0 & 1 \\
1 & 1 & 0 & 1 & 1 & 0 & 0 & 1 \\
0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 1 & 0 & 1
\end{bmatrix}
$$

που οι γραμμές αντιστοιχούν στους εκθέτες που εμφανίζονται στους πρώτους [2,3,5,7,17,23].

O rref (reduced row echelon form : ανηγμένος κλιμακωτός) είναι

$$\tilde{M}=
\begin{bmatrix}
1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 1 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 1 & 0 & 1 \\
0 & 0 & 0 & 0 & 0 & 0 & 1 & 1
\end{bmatrix}
$$

Oι λύσεις είναι 

$$[t,t+w,0,t,t,w,w,w], t, w\in \lbrace 0,1\rbrace$$

Π.χ. για t=0,w=1 έχουμε την  λύση

$$(0,1,0,0,0,1,1,1).$$

Δηλ. οι στήλες 2,6,7,8 είναι γ.ε. mod2.


Οπότε έχουμε,

$x^2=2^{16}\cdot 3^{6}\cdot 5^4\cdot 23^2$ άρα 
$x=2^{8}\cdot 3^{3}\cdot 5^2\cdot 23$ και 
$y=241\cdot 247\cdot 249\cdot 236$ και τέλος
$\gcd(x-y,n)=127.$

H λύση για $t=1,w=0$ είναι

$$(1,1,0,1,1,0,0,0)$$

από την οποία δεν προκύπτει κάποιος μη τετριμμένος διαιρέτης, και

για $t=w=1$ έχουμε την λύση

$$(1,0,0,1,1,1,1,1)$$

όπου προκύπτει μη τετριμένος διαιρέτης.

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
# Sieving B-smooth numbers
H ιδέα που προσθέτει ο quadratic sieve στον Dixon είναι ο τρόπος εντοπισμού των B-smooth ακεραιών.
Αντί να κάνουμε δοκιμαστική διαίρεση, χρησιμοποιούμε το παρακάτω:

Ξεκινάμε με την factor base $FB=\lbrace -1,2,p_2,p_3,...,p_k \rbrace$ όπου προσοχή εδω ο $p_3$ δεν είναι απαραίτητα ο τρίτος πρώτος αλλά ο επόμενoς πρώτος από τον 2, που εχει την ιδιότητα το $n$ να είναι τετραγωνικό υπόλοιπο $\mod p_2.$ Ο $p_3$ είναι ο επόμενος πρώτος, μεγαλύτερος του $p_2,$ έτσι ώστε το $n$ να είναι τετραγωνικό υπόλοιπο $\mod p_3.$ Δηλαδή, 

$$FB=\big\lbrace -1 \big\rbrace \cup \big\lbrace p: \left(\frac{n}{p}\right)=1,  p\leq B \big\rbrace$$

Έστω $y_1,y_2$ οι δύο λύσεις της ισοτιμίας $x^2\equiv n \pmod{p}$ για κάποιον πρώτο $p$ στην FB.

Για κάθε μία από τις λύσεις 

# Eπιλογή του $B$
Στον QS η επιλογή του $B$ είναι $B=L(n)^{1/2}$ ($L(n)=exp(\sqrt{\ln{n}\ln\ln{n}})).$
Στον Dixon η επιλογή ήταν  $B=L(n)^{\sqrt{2}}.$

# Άσκηση

Να υλοποιήσετε τον αλγόριθμο "Quadratic Sieve"
