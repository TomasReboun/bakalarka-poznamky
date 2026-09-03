---
tags:
  - SPN
  - VelkáBezpečnost
---
##### Struktura
- velmi konzervativní
- počet rund: 32
- každá runda:
	- XOR klíče
	- 32 stejných paralelních S-boxů
	- lineární transformace
- používá 8 různých S-boxů; 4bity -> 4bity
- celý popis [zde](https://www.karlin.mff.cuni.cz/~kozlik/udk_mat/serpent.pdf)
##### Matematika
- [[GF(2)]]
- [[lineární transformace]]
- [[bitové permutace]]
##### Útoky
- útok na redukovanou verzi [zde](https://homes.cs.washington.edu/~yoshi/papers/AES00/serpent_aes.pdf?utm_source=chatgpt.com)



