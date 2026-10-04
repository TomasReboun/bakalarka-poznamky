# Struktura
celý popis [zde](https://www.researchgate.net/publication/2331541_Introducing_the_new_LOKI97_Block_Cipher)
#### ==Šifrování==
vstup: 128-bitový plaintext rozdělen na dvě 64-bitová slova $[L|R]$
následuje 16 rund **Feistelova schématu**:
		$L_0 = L$
		$R_0=R$
		potom pro $i=1,...,16$
		$R_i=L_{i-1} \oplus f(R_{i-1}+SK_{3i-2}, SK_{3i-1})$
		$L_i=R_{i-1}+SK_{3i-2}+SK_{3i}$
		kde $f(A,B)$ je rundovní funkce, $+$ je sčítání modulo $2^{64}$
výstup: 128-bitový ciphertext složený jako $[R_{16},L_{16}]$

obrázek: [[LOKI97 Feistelovo schéma.png]]

#### ==Dešifrování==
vstup: $[R_{16},L_{16}]$
projetí rund pozpátku, pro $i=16,...,1$:
		$L_{i-1}=R_i \oplus f(L_i-SK_{3i}, SK_{3i-1})$
		$R_{i-1}=L_i-SK_{3i}-SK_{3i-2}$
výstup: $[L_0,R_0]$

tedy dešifrování je ekvivalentní šifrování až na opačné pořadí použití subklíčů a aditivní inverz u $SK_{3i-2}$ a $SK_{3i}$

#### ==S-boxy==
Šifra používá dva S-boxy $S1,S2$, které jsou založeny na mocnění nad konečným tělesem.
$S1$ zobrazí 13-bitový vstup na 8-bitový výstup
$S2$ zobrazí 11-bitový vstup na 8-bitový výstup
jsou definovány následovně:
	$S1(x)=((x \oplus 1FFF)^3 \mod2911)\& FF$      počítáno v $GF(2^{13})$
	$S2(x)=((x \oplus 7FF)^3 \mod AA7)\&FF$         počítáno v $GF(2^{11})$

Poznámky:
	všechny výpočty provedeny jako polynomy v $GF(2^n)$
	všechny konstanty jsou hexadecimální
	XOR zaručuje, že 0,1 se nezobrazí na 0,1
	maska $\& FF$ vybírá právě 8 (spodních) bitů jako výstup

#### ==Rundovní funkce==
nelineární funkce $f(A,B)$ bere dva 64-bitové vstupy
využívá 2 vrstvy S-boxů a 2 permutace $$f (A, B) = Sb(P (Sa(E(KP (A, B)))), B)$$obrázek: [[LOKI97 Rundovní funkce.png]]

1️⃣**Keyed Permutation** $KP(A,B)$
	rozdělí 64-bitový vstup $A$ na dvě 32-bitová slova,
	ze vstupu $B$ se vezme (spodních/pravých) 32 bitů  
	a ty určují jestli se prohodí odpovídající pár bitů ve slovech
	(ve zkratce prohazuje bity $A$ v závislosti na $B$)
	přesune $i$-tý bit na pozici $i$ nebo $(i+32)\mod 64$ 
2️⃣**Expanzní funkce** $E()$
	rozdělí vstupní bity do překrývajících se skupin (po 11 nebo 13 bitech)
	cílem je aby některé bity ovlivnili dva S-boxy najednou
	$E$ z 64-bitového vstupu vytvoří 96-bitový výstup následovně:
	$[4-0;63-56||58-48||52-40||42-32||34-24||28-16||18-8||12-0]$ 
3️⃣**1. vrstva S-boxů** $Sa()$
	sloupec S-boxů
	$Sa()=[S1,S2,S1,S2,S2,S1,S2,S1]$ 
4️⃣**Permutace** $P()$
	difuze výstupů z S-boxů, používá regulární latinské čtverce
	$P()$ je permutace na $\mathbb{F}_2^{64}$, splňující pro každý vstup $a$, že $P(a) \neq a$  
5️⃣**2. vrstva S-boxů** $Sb()$
	sloupec S-boxů
	$Sb()=[S2,S2,S1,S1,S2,S2,S1,S1]$
	vstupem je $A$ plus (horní/levá) půlka $B$

#### ==Key Schedule==
operuje na čtyřech 64-bitových slovech $[K4_0|K3_0|K2_0|K1_0]$
inicializace závisí na délce uživatelova klíče následovně:
1️⃣ pro **256-bitový** klíč $[K_a|K_b|K_c|K_d]$, označ $[K4_0|K3_0|K2_0|K1_0]=[K_a|K_b|K_c|K_d]$
2️⃣ pro **192-bitový** klíč $[K_a|K_b|K_c]$, označ $[K4_0|K3_0|K2_0|K1_0]=[K_a|K_b|K_c|f(K_a,K_b)]$
3️⃣ pro **128-bitový** klíč $[K_a|K_b]$, označ $[K4_0|K3_0|K2_0|K1_0]=[K_a|K_b|f(K_b,K_a)|f(K_a,K_b)]$

tři subklíče jsou třeba na jednu rundu zpracování dat
vypočteno 48 subklíčů $SK_i \text{ kde }i=1,...,48$ následovně:
	$SK_i=K1_i=K4_{i-1} \oplus g_i(K1_{i-1},K3_{i-1},K2_{i-1})$
	$K4_i=K3_{i-1}$
	$K3_i=K2_{i-1}$
	$K2_i=K1_{i-1}$
kde
	$g_i(K1,K3,K2)=f(K1+K3+(Delta*i),K2)$
	$Delta= \lfloor(\sqrt5-1)*2^{63} \rfloor=(9E3779B97F 4A7C15)_{16}$ 

# Diferenční kryptoanalýza
 [zdroj](https://cosicdatabase.esat.kuleuven.be/backend/publications/files/conferencepaper/366) (Weaknesses in LOKI97)
 Jedná se o **chosen plaintext attack**.
 **Značení**: $e_i=$ 64-bitové slovo, kde $i$-tý bit je 1, ostatní jsou 0 
 
 Uvažujme dva vstupy: $[L|R]$ a $[L^*|R^*]$ takové, že $L=L^*$ a $R=R^* \oplus e_i$ 
 
 Hledáme takové $i$, aby pro $\Delta R=e_i$  platilo $\Delta f(R)=0$
 s relativně vysokou pravděpodobností.
 (Tato pravděpodobnost závisí na počtu aktivních S-boxů. Čím míň tím líp)
 Definujeme $\Delta f(R) =f(R)\oplus f(R^*)$ 

Proč? Z Feistelovy struktury plyne:
	$R_1=L_0 \oplus f(R_0)$
	$L_1=R_0$
(rundovní klíče se považují za konstanty, jejich přičtení zanedbáme, protože jen mění znaménko)
Paralelně probíhá:
	$R_1=L_0 \oplus f(R_0)$
	$R_1^*=L_0^* \oplus f(R_0^*)$
	------------------------
	$\Delta R_1=\Delta L_0 \oplus \Delta f(R_0)$
	------------------------
	máme $\Delta L_0=0$ a podaří se $\Delta f(R_0)=0$
	potom máme také $\Delta R_1=0$.
Zároveň se na konci rundy prohodí obě poloviny.
Proto se po první rundě z diference $[0|e_i]$ stane diference $[e_i|0]$
(s určitou pravděpodobností).

Chceme **two round iterative charakteristic**.
**Iterativní** znamená, že po určitém počtu kol se dostaneme zpět ke stejnému typu rozdílu, se kterým jsme začínali.
diference $[0|e_i]$ --(1.runda)--> diference $[e_i|0]$ --(2.runda)--> diference $[0|e_i]$.
Toto lze zřetězit.

#### Charakteristika pro $i=63$
**Poznámka:** Co se děje při přičtení klíče modulo $2^{64}$?
Označme jednotlivé bity slova $x=x_{63}x_{62}...x_2x_1x_0$
(kde $x_{63}$ je nejvýznamnější bit).
Potom pravděpodobnost, že se diference $e_i$ **nezmění** po přičtení klíče je: 
	$50\%$ pro $i<63$, protože carry (přenos) se může propagovat do vyšších bitů,
	$100\%$ pro $i=63$, protože není kam dál pokračovat.

  $\implies e_{63}$  vypadá jako dobrá diference

Co se stane v rundovní funkci?
Funkce $KP()$ zobrazí diferenci $e_{63}$ buď na $e_{63}$ nebo ne $e_{(63+32)mod64}=e_{31}$
(v závislosti na klíči).
Expanzní funkce $E()$ **neduplikuje** bity 63 a 31 🥳
Tudíž diference $e_{63}$ aktivuje jen jeden S-box    🥳

Do S-boxu přichází dvě (13-bitová nebo 11-bitová) čísla $x,x^*$.
	S-box je **neaktivní**, pokud $x=x^*$. 
	S-box je **aktivní**, pokud $x \neq x^*$. 

Předpokládejme, že je aktivní S-box $S1$.
Máme nenulovou vstupní diferenci $\Delta x =x \oplus x^* \neq 0$.
Chceme stejné výstupy $S1(x)=S1(x^*)$.
Počet možných vstupů je $2^{13}=8192$.
Počet možných výstupů je $2^{8}=256$.
Pravděpodobnost, že budou dva výstupy stejné je tedy $2^{-8}$. 🧐

Z toho plyne $$P[\Delta f(e_{63})]=P[f(R)\oplus f(R \oplus e_{63})=0]=2^{-8}$$
	Mimochodem pravděpodobnost je trochu větší než $2^{-8}$,
	protože nenulový výstup z první vrstvy S-boxů může zmizet ve druhé vrstvě. 
	Tím se ale nebudeme zabývat.

Takto dostaneme iterativní charakteristiku po dvou rundách. $$[0|e_{63}] \to [e_{63}|0] \to [0|e_{63}] \text{ s pravděpodobností } 2^{-8} $$Toto lze opakovat 7krát a dostat 15-kolovou charakteristiku s pravděpodobností $2^{-56}$. 🧐

#### Ostatní charakteristiky
Zvolíme $i \neq 63$. Platí $\Delta R=R \oplus R^*=e_i$.

Při každém přičtení subklíče se diference $e_i$ **nezmění** s pravděpodobností $1/2$.
Navíc se v každé rundě přičtou 2 subklíče.

Funkce $KP()$ "přesune" diferenci z bitu $i$ na bit $i$ nebo bit $i+32 \mod 64$.
Uvažujme všechny dvojice $(i,i+32 \mod 64)$.

Můžeme bity $i$ rozdělit do tří skupin podle toho co se děje při expanzi $E()$.
(vyjdeme z popisu $E()$)

1️⃣ $i \in \{7, 15, 23, 31, 39, 47, 55, 63\}$
	Potom se ani jeden z bitů $i,i+32 \mod 64$ neexpanduje.
	(jen jeden aktivní S-box)
	Celkem 7 bitů. (bit 63 vyřešen dříve)

2️⃣ $i \in \{14, 19, 20, 30, 35, 36, 38, 43, 44, 54, 59, 60\}$
	Potom se bit $i$ neexpanduje.
	Podmínka na permutační klíč: bit $0$ na pozici $i\mod32$.
	Celkem 12 bitů.

3️⃣ $i \in \{3, 4, 6, 11, 12, 22, 27, 28, 46, 51, 52, 62\}$
	Potom se bit $i+32\mod64$ neexpanduje.
	Podmínka na permutační klíč: bit $1$ na pozici $i\mod32$.
	Celkem 12 bitů.

Pro tyto $i$ je tedy aktivován jen jeden S-box a proto platí $$P[\Delta f(e_i)]=P[f(R)\oplus f(R \oplus e_i)=0]=2^{-8}$$navíc se ale musí zohlednit 2 přičtení sub-klíče,
tedy pravděpodobnost, že diference $[0|e_i]$ --(1.runda)--> diference $[e_i|0]$ 
je $2^{-1}*2^{-8}*2^{-1}=2^{-10}$.

Toto dohromady dává 7 charakteristik s pravděpodobností $2^{-10}$
a 24 key-dependent charakteristik s pravděpodobností $2^{-10}$.

Z nich lze poskládat 15ti kolovou charakteristiku s pravděpodobností $2^{-70}$.

#### Resynchronizace
Při modulárním sčítání může jednobitová diference $e_i$ v důsledku propagace carry přejít na vícebitovou diferenci. Pravděpodobnost konkrétního carry řetězce klesá exponenciálně s jeho délkou. Pro $i=63$ již nemůže carry ovlivnit žádný další bit 64bitového výsledku, a proto se diference $e_{63}$ zachová s pravděpodobností 1.

Princip resynchronizace: $$e_i \to e_i \oplus e_{i+1} \oplus e_{i+2} \to e_i$$První přechod vznikne kvůli carry a druhé sčítání *může* rozdíl zase **synchronizovat zpět**.

Takže toto ASI nějak zvyšuje pravděpodobnost charakteristiky,
ale v článku to už neřeší. 😒

#### Útok
Máme 15-ti kolovou charakteristiku, ta vytváří vztah mezi plaintextem a stavem před posledním kolem. Poslední kolo chceme nechat stranou.

             15 kol charakteristiky
P ───────────────────────────────────► ● ──► 16. kolo ──► C
                                      ↑
                               útočník zde

Můžeme pozorovat ciphertext a zkoušet kandidáty posledního round key.
Pravděpodobnost úspěšného páru je $2^{-56}$.
(proto (statisticky) potřebujeme $2^{56}$ chosen plaintextů ???)

Generujeme dvojice plaintextů: $(P, P^*=P\oplus [0|e_{63}])$.
Každý pár má tedy požadovanou vstupní diferenci.

Po 15 rundách se z $(P,P^*)$ stane $(X_{15},X_{15}^*)$.
Pokud to prošlo úspěšně, platí $X_{15}=X_{15}^*\oplus [0|e_{63}]$.

Máme odpovídající ciphertexty $C,C^*$.
Můžeme **částěčně dešifrovat** poslední kolo, pokud uhádneme příslušnou část posledního sub-klíče.

Takže: $C,C^*$ --(inverze last round | kandidát $K_{16}$)--> $X_{15},X_{15}^*$.
Pokud bude sedět diference u většího počtu párů, je $K_{16}$ správně.


# Lineární kryptoanalýza 1
 [zdroj](https://cosicdatabase.esat.kuleuven.be/backend/publications/files/conferencepaper/366) (Weaknesses in LOKI97)
Cílem je najít lineární aproximaci (části) šifry. Existují 2 druhy:

🅰️ aproximace využívá korelace mezi sumou 
	vstupních/výstupních bitů rundovní funkce $f$.
	použito při útoku na DES
	kvůli 2 vrstvám S-boxů u LOKI97 je nízká
	korelace -> nepoužitelné

🅱️ aproximace využívá nevyváženost (imbalance) 
	ve výstupu rundovní funkce.
	Počítá se jen každá druhá runda (proč??).

Část vstupu 2. vrstvy S-boxů je určena pouze klíčem,
takže pro daný klíč jsou fixní.
# Lineární kryptoanalýza 2
 [zdroj2](https://link.springer.com/chapter/10.1007/978-3-540-47942-0_3)(strana 27 - 30)
 Zatím nezpracováno...