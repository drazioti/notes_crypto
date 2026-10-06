# Εισαγωγή στους αλγορίθμους παραγοντοποίησης

Δείτε το [textbook](https://www.dropbox.com/scl/fi/qmokv3plzpjte07xlicvz/draziotis_master.pdf?rlkey=a2v05lceg3d37gwk2wugk9id5&st=rnm0u92p&dl=0) 10.1.2, σελ. 136

## Μέθοδος Fermat για Παραγοντοποίηση

### 1. Ιδέα της μεθόδου

Η μέθοδος παραγοντοποίησης του Fermat βασίζεται στην ταυτότητα:

$$
n = x^2 - y^2=(x-y)(x+y), \text{ όπου }x,y\in {\mathbb{Z}}
$$

Aν $n$ περιττός πάντα υπαρχει αυτη η αλγεβρική έκφραση. Πράγματι, αν $n=Α\times Β$ τότε

$$
n = \big(\frac{Α+Β}{2}\big)^2 - \big(\frac{Α-Β}{2}\big)^2,
$$

και επειδή $n$ περιττός, αναγκαστικά $a,b$ περιττοί, επομένως τα 

$$ \big(\frac{Α+Β}{2}\big), \big(\frac{Α-Β}{2}\big) $$

είναι ακέραιοι.

Άρα, αν μπορέσουμε να γράψουμε έναν περιττό ακέραιο $n$ ως διαφορά δύο τετραγώνων, τότε έχουμε βρει μια παραγοντοποίησή του.
Aν $1<A,B<n$ τότε η παραγοντοποίηση είναι μη τετριμένη.

Αν ο $n$ είναι άρτιος, τότε γράφεται στη μορφή

$$
n = 2^k n',
$$

όπου $k$ είναι θετικός ακέραιος και $n'$ είναι περιττός. 
Επομένως μπορούμε χωρίς βλάβη της γενικότητας να υποθέσουμε ότι $n$ περιττός.

---

### Περιγραφή της μεθόδου

Η μέθοδος του Fermat δουλεύει ως εξής.

1. Θέτουμε αρχικά
a = \lceil \sqrt{n} \rceil.$$

2. Υπολογίζουμε την ακολουθία (γνησίως αύξουσα):


   $$a_1 = (a+1)^2 - n,$$

   $$a_2 = (a+2)^2 - n,$$

   $$\ldots$$

   $$a_k = (a+k)^2 - n.$$

   Σταματάμε μόλις βρούμε κάποιο $a_i$, με $i \in \lbrace 1,2,\ldots,k\rbrace$, που είναι τέλειο τετράγωνο.

Δηλαδή, αν

$$
a_i = b^2
$$

για κάποιον ακέραιο $b$, τότε

$$
(a+i)^2 - n = b^2.
$$

Άρα

$$
n = (a+i)^2 - b^2.
$$

Επομένως

$$
n = (a+i-b)(a+i+b).
$$

Αν οι παράγοντες $a+i-b$ και $a+i+b$ δεν είναι τετριμμένοι, τότε έχουμε βρει μη τετριμμένους διαιρέτες του $n$.

---

## Πλήθος επαναλήψεων

Ένα άνω φράγμα για το $k$ είναι

$$
k < n - \lceil \sqrt{n} \rceil.
$$

Άρα, στη χειρότερη περίπτωση, απαιτούνται $O(n)$ τιμές των $a_i$.

Επομένως, ως προς το μήκος εισόδου, δηλαδή ως προς τον αριθμό των bits του $n$, η μέθοδος έχει εκθετική πολυπλοκότητα.

---

### Πότε είναι αποδοτική η μέθοδος Fermat;

Η μέθοδος είναι αποδοτική, δηλαδή βρίσκει γρήγορα έναν διαιρέτη, όταν ο $n$ έχει κάποιον διαιρέτη κοντά στο $\sqrt{n}$.

Πράγματι, έστω ότι

$$
n = AB
$$

και ότι ο διαιρέτης $A$ είναι κοντά στο $\sqrt{n}$. Επειδή $AB=n$, τότε και ο $B$ είναι αναγκαστικά κοντά στο $\sqrt{n}$.

Άρα οι $A$ και $B$ είναι κοντά μεταξύ τους, οπότε η διαφορά

$$
A-B
$$

είναι κοντά στο μηδέν. Συνεπώς, ο ακέραιος

$$
b = \frac{A-B}{2}
$$

είναι επίσης κοντά στο μηδέν.

Σε αυτήν την περίπτωση, γρήγορα κάποια από τις ποσότητες $a_i$ που υπολογίζουμε αρχικά θα γίνει ίση με $b^2$.

---

### Σχέση με RSA

Αν το $n$ είναι της μορφής

$$
n = pq,
$$

όπου $p,q$ είναι πρώτοι αριθμοί, δηλαδή αν το $n$ είναι ένα RSA modulus, τότε ο αλγόριθμος του Fermat είναι αποτελεσματικός όταν οι πρώτοι $p$ και $q$ είναι πολύ κοντά μεταξύ τους.

Για αυτόν τον λόγο, κατά την παραγωγή RSA modulus, οι δύο πρώτοι παράγοντες δεν πρέπει να επιλέγονται υπερβολικά κοντά.

---

### Αλγόριθμος: Η μέθοδος του Fermat

**Είσοδος:** Θετικός περιττός ακέραιος $n$.

**Έξοδος:** Ένας μη τετριμμένος διαιρέτης του $n$.

```text
for ceil(sqrt(n)) <= a <= floor((n+9)/6) do
    b <- sqrt(a^2 - n)

    if b είναι ακέραιος then
        return gcd(a-b, n)
    end if
end for
```

# Fermat Factorization

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Algorithm](https://img.shields.io/badge/Algorithm-Fermat%20Factorization-green)
![Status](https://img.shields.io/badge/Status-Educational-orange)

This repository contains a simple Python implementation of **Fermat factorization**.

The algorithm searches for a non-trivial divisor of an odd composite integer $begin:math:text$n$end:math:text$.

See the [colabcode](https://colab.research.google.com/drive/1nIoWD2HAwMze5-JGfPEa57e3r06VU_eY?usp=sharing)

---

## Python Code

```python
from math import isqrt, gcd


def fermat_divisor(n: int) -> int | None:
    """
    Fermat factorization search.

    Input:
        n: positive odd composite integer

    Output:
        a non-trivial divisor of n, or None if none is found
    """
    # trivial cases
    if n <= 1:
        raise ValueError("n must be greater than 1")

    if n % 2 == 0:
        # For even n, 2 is already a non-trivial divisor unless n = 2.
        return 2 if n > 2 else None

    # define start point and end point
    x_start = isqrt(n) # floor(sqrt(n))
    if x_start ** 2 < n:
        x_start += 1
    x_end = (n + 9) // 6

   # searching for n=x^2-y^2
    for x in range(x_start, x_end + 1):
        c = x ** 2 - n
        y = isqrt(c)
        if y ** 2 == c:
            return x-y
    return None


# Example
n = 5959
d = fermat_divisor(n)

if d is not None:
    print(f"factor 1: {d}")
    print(f"factor 2: {n // d}")
else:
    print("No non-trivial divisor found")
```

---

## Example Output

```text
factor 1: 59
factor 2: 101
```

