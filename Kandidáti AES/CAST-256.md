---
tags:
  - Feistel
  - ModifikovanýFeistel
  - VelkáBezpečnost
---
##### Struktura
- rozšíření šifry CAST-128, používá stejné 3 rundovní funkce
- počet rund: 48
- zobecněné Feistelovo schéma (4 větve), každá čtvrtina bloku ovlivní jinou čtvrtinu
- šifrování == dešifrování, až na pořadí rundovních klíčů
- rundovní funkce používají 2 typy subklíče:
	- Kr = 5bitový rotační subklíč - určuje bitovou rotaci
	- Km = 32bitový maskovací sublíč - přičtení/odečtení/xor k bloku
- obsahuje 4 S-boxy; 8bitový vstup → 32bitový výstup
- celý popis [zde](https://datatracker.ietf.org/doc/html/rfc2144#page-2)
##### Matematika
- [[Modulární aritmetika]]
- [[GF(2)]]
- [[bitové rotace]]
- [[permutace závislé na klíči]]
- [[ohnuté funkce]]
##### Útoky
- Differential Cryptanalysis of 24-Round [zde](https://www.researchgate.net/publication/4364792_Differential_Cryptanalysis_of_24-Round_CAST-256)
- **zero-correlation linear cryptanalysis** (28 rund) [zde](https://www.researchgate.net/publication/316248247_Multiple_differential-zero_correlation_linear_cryptanalysis_of_reduced-round_CAST-256/link/63fc7bee0cf1030a56567f43/download)
- nejlepší známé útoky kolem 33 rund



