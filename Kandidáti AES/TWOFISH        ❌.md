---
tags:
  - Feistel
  - ModifikovanýFeistel
  - VelkáBezpečnost
---
##### Struktura
- počet rund: 16
- rundovní funkce zpracuje 2 32bitová slova
- používá 4 S-boxy 8x8 závislé na klíči, MDS matici nad GF(2^8), PHT, přičtení klíče
- na rozdíl od klasického Feistela obsahuje navíc bitovou rotaci
- celý popis [zde](https://www.karlin.mff.cuni.cz/~kozlik/udk_mat/twofish.pdf)
##### Matematika
- [[GF(2)]]
- [[GF(2^8)]]
- [[MDS matice]]
- [[matice]]
- [[S-box závislý na klíči]]
- [[Modulární aritmetika]]
- [[bitové rotace]]
- [[Pseudo-Hadamard Transform]]
- [[lineární transformace]]
##### Útoky
- útoky na redukovanou verzi [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-twofish-related.pdf?utm_source=chatgpt.com)



