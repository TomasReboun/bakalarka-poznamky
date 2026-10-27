[AES finalista](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197-upd1.pdf) (sekce 3 a 4)

### Základní pojmy

- *AES* = Advanced Encryption Standart
- *Afiní transformace* = transformace tvořená násobením maticí a přičtením vektoru
- *bit* = binární jednotka: 0 nebo 1
- *blok* = posloupnost bitů pevné délky
- *bloková šifra* = systém permutací bloků parametrizovaný klíčem
- *plaintext* = vstup šifry
- *ciphertext* = výstup šifry
- *bajt* = posloupnost 8 bitů
- *klíč* = parametr blokové šifry určující výběr permutace
- *key schedule* = proces generování rundovních klíčů
- *runda / kolo* = posloupnost transformací stavu šifry
- *rundovní klíč / sub-klíč* = další parametr rundy odvozený z hlavního klíče
- *stav* = plaintext po N krocích šifrování
- *S-box* = nelineární substituční tabulka
- *Slovo* = posloupnost 8N bitů, která se zpracuje jako 1 entita nebo jako posloupnost N bajtů

### Reprezentace bajtů

Hodnota bajtu je označena jako posloupnost 8 bitů, např. {10100011}.
Pokud jsou to proměnné značíme je zleva doprava klesajícími indexy {$b_7 b_6 b_5 b_4 b_3 b_2 b_1 b_0$}.
Někdy je vhodné bajt reprezentovat jako dvojici hexadecimálních znaků.
![[Hexadacimální reprezentace.png]]
Například hexadecimální forma bajtu {10100011} je {a3}.

### Operace na bajtech

Při některých transformacích v šifře se bajt bere jako prvek 256 prvkového tělesa $\mathbb Z_2^8$. Každý bajt {$b_7 b_6 b_5 b_4 b_3 b_2 b_1 b_0$} budeme vnímat jako polynom $b(x)$ následujícím způsobem: $$b(x) = b_7 x^7 +b_6 x^6 +b_5 x^5 +b_4 x^4 +b_3 x^3 +b_2 x^2 +b_1 x+b_0$$Například {01100011} je zastoupen polynomem $x_6 +x_5 +x+1$.

#### Sčítání
Při sčítání prvků v $\mathbb Z_2^8$ se koeficienty příslušných polynomů sečtou modulo 2. 
Toto prování operace XOR, označována $\oplus$, následujícím způsobem: $$1 \oplus 1 = 0 \oplus 0 = 0 \\  1 \oplus 0=0\oplus1=1$$Tedy pro bajty  {$a_7 a_6 a_5 a_4 a_3 a_2 a_1 a_0$} a  {$b_7 b_6 b_5 b_4 b_3 b_2 b_1 b_0$} je jejich součet  {$a_7 \oplus b_7\ a_6 \oplus b_6\ a_5 \oplus b_5\ a_4 \oplus b_4\ a_3 \oplus b_3\ a_2 \oplus b_2 \ a_1 \oplus b_1\ a_0 \oplus b_0$}.

Například následující 3 reprezentace sčítání jsou ekvivalentní:
	$(x^6 +x^4 +x^2 +x+1) + (x^7 +x+1) = x^7 +x^6 +x^4 +x^2$             (polynomická)
	{01010111} $\oplus$ {10000011} = {11010100}                                          (binární)
	{57} $\oplus$ {83} = {d4}                                                                             (hexadecimální).

#### Násobení 
Symbol $*$ označuje násobení v $\mathbb Z_2^8$. Násobení probíhá ve dvou krocích: nejprve se vynásobí odpovídající polynomy a výsledek se následně moduluje fixním polynomem $$m(x) = x^8 +x^4 +x^3 +x+1$$Tedy pro bajty $b$ a $c$ máme polynomy $b(x)$ a $c(x)$ a jejich součin $$b(x)*c(x)=b(x)c(x) \mod m(x)$$
#### Multiplikativní inverze
Pro nenulový bajt $b \neq${0,0} je jeho inverze jednoznačně určený bajt $b^{-1}$ 
splňující $b*b^{-1}=${01}.

Toto zle spočítat buď jako $$b^{-1}=b^{254}$$anebo pomocí rozšířeného Euklidova algoritmu použitého na polynomy $b(x)$ a $m(x)$ najít polynomy $a(x)$ a $c(x)$ splňující $$b(x)a(x)+m(x)c(x)=1$$potom $a(x)$ je polynom zastupující $b^{-1}$.