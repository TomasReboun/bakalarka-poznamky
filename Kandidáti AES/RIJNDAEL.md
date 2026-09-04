---
tags:
  - SPN
  - SQUARE
  - VelkáBezpečnost
---
##### Struktura
- počet rund: 10/12/14 podle délky klíče
- blok reprezentován jako 4x4 matice bajtů
- rundu tvoří:
	- aplikování S-boxu na každý bajt
	- shift rows
	- mix colums (pomocí MDS)
	- XOR klíče
- S-box: 8bitů -> 8bitů
- S-box tvoří multiplikativní inverz nad GF(2^8) a afiní transformace nad GF(2)
- celý popis [zde](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197-upd1.pdf)
- využívá Wide Trail Strategy [zde](https://www.researchgate.net/publication/221347831_AES_and_the_Wide_Trail_Design_Strategy)
##### Matematika
- [[GF(2)]]
- [[GF(2^8)]]
- [[lineární transformace]]
- [[afinní transformace]]
- [[MDS matice]]
- [[matice]]
- [[bitové permutace]]
##### Útoky
- útok na redukovanou verzi [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-rijndael.pdf)



zkouším jestli to funguje
