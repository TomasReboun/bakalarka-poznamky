
**Definice**
Zobrazení $f:\mathbb F_2^n \to \mathbb F_2^m$ se nazývá ==*booleovská funkce==*.
V případě $m=1$ mluvíme o ==*binární booleovské funkci*== .

**Definice**
Na množině všech binárních booleovských funkcí $\mathbb F_2^n \to \mathbb F_2$ můžeme pomocí operací dvouprvkového tělesa definovat sčítání a násobení (po bodech): $$(f+g)(v)=f(v)+g(v)\\ (f\cdot g)(v)=f(v) \cdot g(v)$$Získáme tím *==okruh binárních booleovských funkcí==*, který budeme značit $R_n$.

Lze snadno ověřit, že $R_n$ je komutativní okruh.
	nulový prvek = konstantní zobrazení const$_0$
	jednotkový prvek = konstantní zobrazení const$_1$

**Definice**
Polynom $p\in \mathbb F_2[x_1,...,x_n]$ bez vyšších mocnin proměnných se nazývá ==*algebraická normální forma==* funkce $f \in R_n$, pokud pro každé $v \in \mathbb F_2^n$ platí $f(v)=p(v)$.
V tomto případě polynom značíme $ANF(f)$.

Následující věta dokazuje existenci a jednoznačnost algebraické normální formy.

**Věta** ==(o algebraické normální formě)==$$R_n \simeq \mathbb F_2[x_1,...,x_n]/\langle x_1+x_1^2,...,x_n+x_n^2 \rangle$$**Důkaz**
Označme $I=\langle x_1+x_1^2,...,x_n+x_n^2 \rangle$ ideál okruhu $\mathbb F_2[x_1,...,x_n]$. Pro každé $i=1,...,n$ 
platí tedy $x_i \equiv_I x_i^2$. Z toho plyne, že každý polynom je kongruentní modulo $I$ s polynomem bez vyšších mocnin proměnných.

Definujme zobrazení okruhů $\varphi: \mathbb F_2[x_1,...,x_n] \to R_n$ 
    $\varphi:p \mapsto f, \text{ kde } f(v)=p(v) \text{ pro každé } v \in \mathbb F_2^n$ 

Obraz $\varphi (p)$ definujeme dosazováním vektorů z $\mathbb F_2^n$ do polynomu $p$,kde za proměnné dosazujeme příslušné složky vektoru. Z vlastností dosazování a z definice operací $R_n$ zjistíme, že $\varphi$ je homomorfismus okruhů: $$(\varphi(p+q))(v)=(p+q)(v)=p(v)+q(v)=\varphi(p)(v)+\varphi(q)(v)=(\varphi(p)+\varphi(q))(p)\\(\varphi(p\cdot q))(v)=(p\cdot q)(v)=p(v)\cdot q(v)=\varphi(p)(v)\cdot \varphi(q)(v)=(\varphi(p)\cdot\varphi(q))(p)$$Úplný vzor $\varphi^{-1}(0)=Ker(\varphi)$ je tedy ideál okruhu $\mathbb F_2[x_1,...,x_n]$. Přitom platí
$\varphi(x_i+x_i^2)(v)=v_i+v_i^2=0$, tedy $\varphi(x_i+x_i^2)=$const$_0$ a proto $I \subseteq Ker(\varphi)$.
Naopak, zvolme $p\in Ker(\varphi)$. Víme, že existuje $p' \equiv_I p$ bez vyšších mocnin proměnných.
Je-li $p'=0$, pak $p'\in I$. Pokud by $p'\neq 0$, zvolíme $q$ mono člen $p'$ s nejnižším stupněm (nejmenším počtem proměnných) a vektor $v \in \mathbb F_2^n$ tak, že $v_i=1$ právě když $x_i|q$. Tím dostaneme $q(v)=1$ a hodnota zbylých mono členů $p'$ bude přitom ve $v$ nulová. Tedy $p'(v) =1$ a $p' \notin Ker(\varphi)$. Polynom $p$ tedy nemůže ležet v jádru $\varphi$, což je spor.

Ukázali jsme, že $Ker(\varphi)=I$. Navíc v každé třídě kongruence $\equiv_I$ leží právě jeden polynom bez vyšších mocnin proměnných.
Proto je indukovaný homomorfismus $\varphi':\mathbb F_2[x_1,...,x_n]/I \to R_n$ prostý.
Zbývá ukázat, že každá binární booleovská funkce je $\varphi$-obrazem nějakého polynomu.
Pro $v \in \mathbb F_2^n$ označme $f_v \in R_n$ funkci takovou, že $f_v(v)=1$ a pro každé $w \neq v: f_v(w)=0$.
Položme $$q_v=\prod_{i=1}^n (x_i+v_i+1)$$Snadno ověříme, že $\varphi(q_v)=f_v$. Pro $f \in R_n$ položme $$p = \sum_{v \in \mathbb F_2^n; f(v)=1}q_v$$Potom bude platit $$\varphi(p)=\sum_{v \in \mathbb F_2^n; f(v)=1}f_v=f$$                                                                                                                                       $\square$

**Definice**
==*Algebraický stupeň*== $deg(f)$ funce $f\in R_n$ je stupeň její algebraické normální formy, tedy největší délka mono členu $ANF(f)$.

**Věta**
Algebraický stupeň je afinně invariantní.
Tedy pro $f \in R_n$ a afinní bijekci $h: \mathbb F_2^n \to \mathbb F_2^n$  platí $deg(f) =deg(f\circ h)$.

**Důkaz**
ve skriptech.

**Definice**
Pro $f,g \in R_n$ definujme ==*korelaci*== $C(f,g)=2 \cdot P(f=g)-1$.

Hodnota korelace tedy odpovídá pravděpodobnost jevu $f=g$: $$C(f,g)=2\cdot \frac{|\{u \in \mathbb Z_2^n;f(u)=g(u)\}|}{2^n}-1$$Je-li $C(f,g)\neq0$ řekneme, že $f,g$ jsou korelovány.
Pro kryptoanalytické využití není podstatné  znaménko korelace, ale velikosti její odchylky od nuly.

**Tvrzení** (vlastnosti korelace)
Pro $f,g \in R_n$ platí: $$-1 \le C(f,g) \le 1 \\ C(f,g) = C(g,f) \\ C(f,g)=C(f+g,0_{R_n}) \\ C(f,g)=1 \iff f=g \\ C(f,g)=0 \iff f+g=1_{R_n}$$
**Definice**
Pro funkci $f \in R_n$ definujeme ==*znaménkovou funkci*== $\hat f: \mathbb F_2^n \to \{-1,1\}$ splňující
$\widehat f(u)=(-1)^{f(u)}$ pro každé $u \in \mathbb F_2^n$.