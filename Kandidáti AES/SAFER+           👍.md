---
tags:
  - SPN
  - StředníBezpečnost
---
##### Struktura
- počet rund: 8/12/16 podle délky klíče
- rundovní funkci tvoří:
	- substituce závislá na klíči
		- působí na 16 bajtů individuálně
		- kombinuje přičtení klíče, XOR klíče a fixní permutaci nebo její inverz
		- permutací je mocnění fixního generátoru multiplikativní grupy modulo 257
	- lineární transformace
		- využívá PHT
- 2 S-boxy (EXP a LOG): 8bitů->8bitů
- celý popis [zde](https://networkdls.com/File/Entity/article-archive/cylink-corporations-submission-for-aes.pdf?utm_source=chatgpt.com)
##### Matematika
- [[GF(2)]]
- [[Modulární aritmetika]]
- [[diskrétní mocnění]]
- [[Pseudo-Hadamard Transform]]
- [[lineární transformace]]
- [[bitové permutace]]
##### Útok na SAFER+
- [zdroj](https://www.schneier.com/wp-content/uploads/2016/02/paper-safer.pdf)
- ==key schedule== je horší pro delší klíče (špatná difuze)
	- 128bit klíč: v každém kole celý klíč ovlivní celý stav
	- 192bit klíč: zabere 5 rund (z 12) aby každý bajt klíče ovlivnil stav
	- 256bit klíč: zabere 9 rund (z 16) aby každý bajt klíče ovlivnil stav
		(poslední bajt klíče se projeví až v 9. rundě)
- každá runda využívá 2 128bitové sub-klíče

1) ==Meet-in-the-middle attack== na SAFER+/256
	- vyžaduje: 3 známé páry plaintext/ciphertext, $12×2^{24}$ bajtů paměti a $2^{240}$ operací šifrování (to není proveditelné ale je to míň než průměrných $2^{255}$)
2) ==Related-key attack== na SAFER+/256
	- vyžaduje: $3×2^{32}$ chosen plaintextů a přibližně $2^{200}$ operací šifrování
3) nenašli se slabé klíče 

- na konci článku návrh na zlapšení key schedulu
- oba útoky zajímavé, v článku málo matiky, ale asi bude možno rozvést
### Poznámky
- potenciálně matematicky zajímavý (dlog, dexp)


