# Dixon's method

Η μέθοδος του Dixon ήταν ο πρώτος γενικού σκοπού αλγόριθμος παραγοντοποίησης ακεραίων με αυστηρά αποδεδειγμένο υποεκθετικό αναμενόμενο χρόνο εκτέλεσης. 
Σε αντίθεση με τις συνήθεις αναλύσεις του Quadratic Sieve και του κλασικού Number Field Sieve, η απόδειξή του δεν βασίζεται σε ευρετικές υποθέσεις 
σχετικά με την ομαλότητα τιμών πολυωνύμων. Ωστόσο, σήμερα δεν είναι ο μοναδικός αλγόριθμος παραγοντοποίησης για τον οποίο είναι γνωστό ένα αυστηρό υποεκθετικό φράγμα.

Έστω $n$ ένας σύνθετος θετικός ακέραιος.
Έστω $P_B=\lbrace p_1=2,...,p_k \rbrace$, διαδοχικοί πρώτοι με $p_k<B$ δηλ. $k=\pi(B)$. 
Παράγουμε τυχαίους ακέραιους $\lbrace z_1,z_2,...,z_r \rbrace$ από το διάστημα $[1,n]$,
και υπολογίζουμε $z_i^2\pmod{n}.$ Σχηματίζουμε όλους τος $B-smooth$ $z_i^2.$
Έστω $F$ το σύνολο που αποτελείται από αυτούς τους αριθμούς.
Για κάθε $x$ του $F$ θεωρούμε την παραγοντοποίηση του, η οποία θα είναι της μορφής

$$x=p_1^{a_1}p_2^{a_2}\cdots p_k^{a_k} $$ όπου $a_i\ge 0.$

Αν υποθέσουμε ότι το $F$ έχει $s$ στοιχεία $x_1,...,x_s$ τότε κάθε $x_i$ είναι της μορφής
$z^2 \pmod{n}$ και $B-smooth$. Απαιτούμε το $s=k+1.$

Σχηματίζουμε τα διανύσματα των εκθετών $mod{2},$
δηλ. 

$$(a_{11}\mod{2},a_{12}\mod{2},...,a_{1k}\mod{2}) $$ το διάνυσμα εκθετών του $x_1$

$$(a_{21}\mod{2},a_{22}\mod{2},...,a_{2k}\mod{2}) $$ το διάνυσμα εκθετών του $x_2$

$$....$$

$$(a_{s1}\mod{2},a_{s2}\mod{2},...,a_{sk}\mod{2}) $$ το διάνυσμα εκθετών του $x_s$

Μ o πίνακας $k\times (k+1)$ που έχει ώς στήλες αυτά τα διανύσματα.

Kάθε λύση του $Μx=0\pmod{2}$ δίνει μια σχέση γραμμικής εξάρτησης στις στήλες. 

Αν $(j_1,...,j_r)$ οι γρ.εξαρτημένες στήλες, τότε θέτουμε $x_{j_1}x_{j_2}\cdots x_{j_r}=x^2.$ 
Αλλά και κάθε $x_{j_i}$ είναι $z_{j_i}^2.$ Άρα,  $x_{j_1}x_{j_2}\cdots x_{j_r}=z^2.$
Eπομένως, $z^2\equiv x^2\pmod{ n}.$

### Παράδειγμα Dixon για $n = 58801, B = 7$

Factor base:

$$
P_B= \{2,3,5,7\}
$$

Ξεκινάμε από:

$$
x = \lceil \sqrt{58801} \rceil = 243
$$

| $x$ | $y^2 = x^2 \bmod n$ | Παραγοντοποίηση του $y^2$ | Είναι $B-smooth;$ |
|---:|---:|---|:---:|
| 243 | 248 | $2^3 \cdot 31$| Όχι |
| 244 | 735 | $3 \cdot 5 \cdot 7^2$ | Ναι |
| 245 | 1224 | $2^3 \cdot 3^2 \cdot 17$ | Όχι |
| 246 | 1715 | $5 \cdot 7^3$ | Ναι |
| 247 | 2208 | $2^5 \cdot 3 \cdot 23$ | Όχι |
| 248 | 2703 | $3 \cdot 17 \cdot 53$ | Όχι |
| 249 | 3200 | $2^7 \cdot 5^2$ | Ναι |
| 250 | 3699 | $3^3 \cdot 137$ | Όχι |
| 251 | 4200 | $2^3 \cdot 3 \cdot 5^2 \cdot 7$ | Ναι |
| 252 | 4703 | $4703$ | Όχι |
| 253 | 5208 | $2^3 \cdot 3 \cdot 7 \cdot 31$ | Όχι |
| 254 | 5715 | $3^2 \cdot 5 \cdot 127$ | Όχι |
| 255 | 6224 | $2^4 \cdot 389$ | Όχι |
| 256 | 6735 | $3 \cdot 5 \cdot 449$ | Όχι |
| 257 | 7248 | $2^4 \cdot 3 \cdot 151$ | Όχι |
| 258 | 7763 | $7 \cdot 1109$ | Όχι |
| 259 | 8280 | $2^3 \cdot 3^2 \cdot 5 \cdot 23$ | Όχι |
| 260 | 8799 | $3 \cdot 7 \cdot 419$| Όχι |
| 261 | 9320 | $2^3 \cdot 5 \cdot 233$ | Όχι |
| 262 | 9843 | $3 \cdot 17 \cdot 193$ | Όχι |
| 263 | 10368 | $2^7 \cdot 3^4$ | Ναι |

Kρατάμε μόνο τις $B$-smooth σχέσεις:

| $x$ | $B$-smooth τιμή | Παραγοντοποίηση | Διάνυσμα εκθετών mod 2 ως προς $(2,3,5,7)$ |
|---:|---:|---|:---:|
| 244 | $735$ | $3 \cdot 5 \cdot 7^2$ | $(0,1,1,0)$ |
| 246 | $1715$ | $5 \cdot 7^3$ | $(0,0,1,1)$ |
| 249 | $3200$ | $2^7 \cdot 5^2$ | $(1,0,0,0)$ |
| 251 | $4200$ | $2^3 \cdot 3 \cdot 5^2 \cdot 7$ | $(1,1,0,1)$ |
| 263 | $10368$ | $2^7 \cdot 3^4$ | $(1,0,0,0)$ |


$$
M =
\begin{pmatrix}
0 & 0 & 1 & 1 & 1 \\
1 & 0 & 0 & 1 & 0 \\
1 & 1 & 0 & 0 & 0 \\
0 & 1 & 0 & 1 & 0
\end{pmatrix}
$$

Ο ανηγμένος πίνακας είναι:

$$
M' =
\begin{pmatrix}
1 & 0 & 0 & 1 & 0 \\
0 & 1 & 0 & 1 & 0 \\
0 & 0 & 1 & 1 & 1 \\
0 & 0 & 0 & 0 & 0
\end{pmatrix}
$$

Oι μη μηδενικές λύσεις είναι οι εξής 
(1,1,0,1,1),(1,1,1,1,0),(0,0,1,0,1).

H πρώτη λύση δεν δίνει καποιον διαιρέτη $>1$, η δεύτερη λύση δίνει,
$x=2^5 * 3 * 5^3 * 7^3, y = 244 * 246 * 249 * 251$
και $gcd(x+y,n)=463.$

Γενικά ένα σύστημα $k\times k+1$ με βαθμίδα $r$ εχει $2^{k+1-r}-1$ μη μηδενικές λύσεις


# Πολυπλοκότητα
Aν $$L_n[\alpha,c]=\exp\left((c+o(1))(\ln n)^\alpha(\ln\ln n)^{1-\alpha}\right)$$, τότε η πολυπλοκότητα του Dixon είναι,

$$L_n(1/2,3\sqrt{2}).$$

Στον αλγόριθμο του Dixon εξετάζουμε $r$ τυχαίους ακεραίους $z \in [1,n]$ και ελέγχουμε αν το $z^2 \bmod n$ είναι $B$-ομαλό. Για την επιλογή 
$B=\exp\left(\sqrt{2\ln n\,\ln\ln n}\right)=L_n(1/2,\sqrt{2})$ και  $r=\lfloor B^2+1\rfloor$, το θεώρημα του Dixon δείχνει ότι η πιθανότητα αποτυχίας είναι $O(r^{-1/2})$. Επομένως, η πιθανότητα ο αλγόριθμος να βρει επιτυχώς έναν γνήσιο παράγοντα του $n$ είναι

$$
\Pr(\text{επιτυχία}) = 1 - O\left(\frac{1}{\sqrt{r}}\right).
$$

Πρόκειται για ασυμπτωτική εκτίμηση και όχι ακριβώς για $1-1/\sqrt{r}$, επειδή ο συμβολισμός $O$ αποκρύπτει μια σταθερά.

## Optimization
Η πολυπλοκότητα του Dixon μπορεί να βελτιωθεί στην,

$$L_n(1/2,2\sqrt{2}).$$


# Dixon's Factorization Algorithm

## Input

- An odd composite integer $n$ with at least two distinct prime factors.
- A list

$$
L=(z_1,z_2,\ldots,z_r),
\qquad
z_i\in\lbrace 1,\ldots,n\rbrace.
$$

- A smoothness bound $B$.

## Factor base

Let

$$
P=\lbrace -1,2,3,5,\ldots,p_k\rbrace,
$$

where $p_k$ is the largest prime satisfying $p_k\le B$.

Thus,

$$
|P|=\pi(B)+1=k+1.
$$

## Output

A proper factor of $n$, or `FAILURE`.

## Algorithm

### Initialization

Set

$$
\mathcal{B}=[\,],
\qquad
\mathcal{Z}=[\,].
$$

Here, $\mathcal{B}$ stores exponent vectors and $\mathcal{Z}$ stores the corresponding values of $z$.

### Step 1: Select an element

If $L$ is empty, return `FAILURE`.

Otherwise, remove the first element $z$ from $L$.

### Step 2: Compute a quadratic residue

Compute

$$
w=z^2\bmod n.
$$

Use the least positive residue.

### Step 3: Test for smoothness

Try to factor $w$ over the factor base $P$:

$$
w=(-1)^{a_0}\prod_{i=1}^{k}p_i^{a_i}.
$$

If $w$ is not $B$-smooth, return to Step 1.

Otherwise, form the exponent vector

$$
\mathbf{a}=(a_0,a_1,\ldots,a_k)\pmod 2.
$$

Append $\mathbf{a}$ to $\mathcal{B}$ and append the corresponding value $z$ to $\mathcal{Z}$.

### Step 4: Collect enough relations

If

$$
|\mathcal{B}|\le k+1,
$$

return to Step 1.

Otherwise, search for a nonzero vector

$$
\mathbf{c}=(c_1,c_2,\ldots,c_t)\in\mathbb{F}_2^t
$$

such that

$$
\sum_{j=1}^{t}c_j\mathbf{a}_j
\equiv
\mathbf{0}
\pmod 2.
$$

This dependency can be found using Gaussian elimination over $\mathbb{F}_2$.

### Step 5: Construct a congruence of squares

Let

$$
S=\lbrace j:c_j=1\rbrace.
$$

Compute

$$
x=\prod_{j\in S}z_j\pmod n.
$$

For each $i=0,1,\ldots,k$, define

$$
e_i=
\frac{1}{2}
\sum_{j\in S}a_{j,i}.
$$

The quantities $e_i$ are integers because the selected exponent vectors sum to the zero vector modulo $2$.

Now compute

$$
y=(-1)^{e_0}\prod_{i=1}^{k}p_i^{e_i}\pmod n.
$$

Then

$$
x^2\equiv y^2\pmod n.
$$

### Step 6: Extract a factor

If

$$
x\equiv y\pmod n
$$

or

$$
x\equiv -y\pmod n,
$$

discard this dependency and continue collecting relations.

Otherwise, compute

$$
d_1=\gcd(x-y,n)
$$

and

$$
d_2=\gcd(x+y,n).
$$

If $1<d_1<n,$ return $d_1$.

If $1<d_2<n,$ return $d_2$.

Otherwise, continue searching for another dependency.
# Ψηφιακό Υλικό

[Dixon's paper (1981)](https://www.ams.org/journals/mcom/1981-36-153/S0025-5718-1981-0595059-1/S0025-5718-1981-0595059-1.pdf)

https://every-algorithm.github.io/2024/04/08/dixons_factorization_method.html
