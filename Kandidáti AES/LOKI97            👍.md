# Struktura
celý popis [zde](https://www.researchgate.net/publication/2331541_Introducing_the_new_LOKI97_Block_Cipher)
#### ==Šifrování==
vstup: 128-bitový plaintext rozdělen na 2 64-bitová slova $[L|R]$
následuje 16 rund **Feistelova schématu**:
		$L_0 = L$
		$R_0=R$
		potom pro $i=1,...,16$
		$R_i=L_{i-1} \oplus f(R_{i-1}+SK_{3i-2}, SK_{3i-1})$
		$L_i=R_{i-1}+SK_{3i-2}+SK_{3i}$
		kde $f(A,B)$ je rundovní funkce, $+$ je sčítání modulo $2^{64}$
výstup: 128-bitový ciphertext složený jako $[R_{16},L_{16}]$

celé šifrovací schéma: [[Pasted image 20261001190545.png]]

#### ==Dešifrování==
vstup: $[R_{16},L_{16}]$
projetí rund pozpátku, pro $i=16,...,1$:
		$L_{i-1}=R_i \oplus f(L_i-SK_{3i}, SK_{3i-1})$
		$R_{i-1}=L_i-SK_{3i}-SK_{3i-2}$
výstup: $[L_0,R_0]$

tedy dešifrování je ekvivalentní šifrování až na opačné pořadí použití subklíčů a aditivní inverz u $SK_{3i-2}$ a $SK_{3i}$

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

#### ==Rundovní funkce==
nelineární funkce $f(A,B)$ bere dva 64-bitové vstupy
využívá 2 vrstvy S-boxů a 2 permutace $$f (A, B) = Sb(P (Sa(E(KP (A, B)))), B)$$celé schéma zde [[Pasted image 20261002085239.png]]

1️⃣**Keyed Permutation** $KP(A,B)$
2️⃣**Expanzní funkce** $E()$
3️⃣**1. vrstva S-boxů** $Sa()$
4️⃣**Permutace** $P()$
5️⃣**2. vrstva S-boxů** $Sb()$

#### ==S-boxy==
TODO

 
# Útok na LOKI97
 [zdroj](https://cosicdatabase.esat.kuleuven.be/backend/publications/files/conferencepaper/366)
- slabiny v rundovní funkci -> teoretické útoky
 1) ==Diferenční kryptoanalýza== 
	- 1bitový rozdíl vstupu rundovní funkce má relativně velkou pravděpodobnost na 1bitový rozdíl výstupu
	- two-round iterative characteristics
	- využívá vlastnosti S-boxů
	- na konci článku 2 nástřely útoků (odhadnuto $2^{56}$ potřebných chosen plaintextů)
2) ==Lineární kryptoanalýza== 
	- snaha aproximovat výstup rundovní funkce
	- korelace mezi nejméně důležitými bity vstupu a výstupu
	- $2^{-16}$ z klíčů jsou slabé -> možný útok 
		(odhadnuto $2^{56}$ potřebných known plaintextů)
	- zmíněno partitioning cryptanalysis (zobecnění lineární kryptoanalýzi) 
- krátký popis, málo matiky
 [zdroj2](https://link.springer.com/chapter/10.1007/978-3-540-47942-0_3)(strana 27 - 30)
 - ==Lineární kryptoanalýza==
 - využívá analýzu S-boxů -> algebra a booleovské funkce