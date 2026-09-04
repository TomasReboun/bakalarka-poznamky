---
tags:
  - SPN
  - SQUARE
  - StředníBezpečnost
---
na první konferenci objeveny slabé klíče, na druhé konferenci šifra opravena
##### Struktura
- stav: matice 4x4 bajtů
- rundovní funkce:
	- AddRoundKey
	- substituce
	- transpozice = permutace bajtů
	- mixing = lineární transformace po řádcích/sloupcích
- počet rund: 12
- 4 varianty 1 S-boxu: 8bitů -> 8bitů
- key schedule - různý podle délky klíče
- šifrování == dešifrování, až na pořadí rundovních klíčů
- popis revidované verze [zde](https://scispace.com/pdf/a-revised-version-of-crypton-crypton-v1-0-43i5o2m7zl.pdf)
##### Matematika
- [[GF(2)]]
- [[bitové permutace]]
- [[lineární transformace]]
- [[matice]]
##### Útoky
- útok na 6ti kolovou verzi [zde](https://www.researchgate.net/publication/220942446_Attack_on_Six_Rounds_of_CRYPTON)
- stochastická analýza (8 kol) [zde](https://www.researchgate.net/publication/220942318_Stochastic_Cryptanalysis_of_Crypton)
- collision attacks (8 kol) [zde](https://www.researchgate.net/publication/275073613_Collision_Attacks_on_AES-192256_Crypton-192256_mCrypton-96128_and_Anubis)


