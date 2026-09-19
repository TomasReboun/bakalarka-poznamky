---
tags:
  - Feistel
  - MaláBezpečnost
---
##### Struktura
- počet rund. 16
- rundovní funci tvoří:
	- permutace daná klíčem
	- fixní expanzní funkce
	- 2 S-boxy tvaru 13x8 a 11x8
	- fixní permutace
	- expanze podle klíče
	- znovu aplikování S-boxů
- S-boxy vznikly mocněním v GF(2^13) a GF(2^11)
- celý popis [zde](https://www.researchgate.net/publication/2331541_Introducing_the_new_LOKI97_Block_Cipher)
##### Matematika
- [[GF(2)]]
- [[konečná tělesa]]
- [[Modulární aritmetika]]
- [[bitové permutace]]
##### Útoky
- slabiny v rundovní funkci [kratší](https://www.researchgate.net/publication/2512721_Weaknesses_in_LOKI97), [delší](https://cosicdatabase.esat.kuleuven.be/backend/publications/files/conferencepaper/366)
### Poznámky
- matematicky potencálně zajímavější
- slabé klíče


