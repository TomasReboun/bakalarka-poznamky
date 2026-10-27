užitečné pojmy z [Matematická kryptografie a kryptoanalýza 1](https://www.sent.cz/MK/)

**Definice**
*==Symetrický kryptosystém==* $\mathcal{S}$ je pětice konečných množin $(\mathcal P, \mathcal C, \mathcal K,e,d)$, kde
	$\mathcal P$ je množina otevřených textů (plaintextů)
	$\mathcal C$ je množina zašifrovaných textů (ciphertextů)
	$\mathcal K$ je prostor klíčů
	$e:\mathcal P × \mathcal K \to \mathcal C$ je šifrovací zobrazení
	$d:\mathcal C × \mathcal K \to \mathcal P$ je dešifrovací zobrazení

Pro každý plaintext $x \in \mathcal P$ a každý $K \in \mathcal K$ musí platit: $d(e(x,K),K)=x$.
(neboli jinak značeno: $d_K \circ e_K=Id_{\mathcal P}$)

V (asi) celém textu bude platit:
	$\mathcal P = \mathcal C = \mathbb Z_2^{128}$
	$\mathcal K = \mathbb Z_2^N$, pro $N \in \{128,192,256\}$

Příklady: substituční, permutační, Hillova šifra

Podle možností útočníka rozlišujeme:
- ciphertext only attack
- known plaintext attack
- chosen plaintext attack

**Definice**
Nechť $I,J$ jsou konečné množiny indexů a $f:\prod_{i\in I}A_i \to \prod_{j\in J}B_j$ je zobrazení kartézských součinů množin. Pro $r \in I, s \in J$ řekneme, že $s$-tá složka obrazů $f$ ==*závisí na*== $r$, pokud existují $a,a'\in \prod_{i\in I}A_i$ takové, že $a \restriction I \setminus \{r\} = a' \restriction I \setminus \{r\}$ a  přitom $f(a)_s \neq f(a')_s$.
Označíme $I_{f,s}=\{r \in I; s \text{ závisí na }r\}$.

**Definice**
Pro $f:\mathbb Z_2^{n} \to \mathbb Z_2^{m}$ definujme ==*stupeň difuze*==: $$d(f)=\frac{|\{0\le s < m; |I_{f,s}|=n\}|}{m}$$Řekneme, že $f$ má *==plnou difuzi==*, pokud $d(f)=1$.

Obvyklým požadavkem pro iterované kryptosystémy je, aby kryptosystém
po malém počtu kol dosáhl plné difuze.