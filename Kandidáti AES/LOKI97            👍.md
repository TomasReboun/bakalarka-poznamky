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
##### Útok na LOKI97
- [zdroj](https://cosicdatabase.esat.kuleuven.be/backend/publications/files/conferencepaper/366)
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
### Poznámky
- matematicky potenciálně zajímavější
- slabé klíče


