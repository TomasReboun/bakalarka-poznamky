---
tags:
  - Feistel
  - StředníBezpečnost
---
DFC = Decorrelated Fast Cipher
##### Struktura
- počet rund: 8
- rundovní funkce používá sčítání a násobení modulo 2^64+13 a permutaci se sčítáním modulo 2^64
- XOR 2 fixních hodnot
- nepoužívá S-boxy, místo toho konstrukce Confusion Permutation a lookup tably
- šifrování == dešifrování, až na pořadí rundovních klíčů
- Decorrelation theory [zde](https://www.researchgate.net/publication/220942360_On_the_Decorrelated_Fast_Cipher_DFC_and_Its_Theory)
##### Matematika
- [[Decorrelation theory]]
- [[Modulární aritmetika]]
- [[GF(2)]]
- [[nelineární transformace]]
##### Útoky
- útok na 6ti kolovou verzi [zde](https://www.researchgate.net/publication/220942360_On_the_Decorrelated_Fast_Cipher_DFC_and_Its_Theory)
- během konference objevena slabina v key schedule, opraveno [zde](https://www.di.ens.fr/david.pointcheval/Documents/Papers/w1999_DFCv2.pdf?utm_source=chatgpt.com)

