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
##### Útoky
- related-key attack [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-safer.pdf)


