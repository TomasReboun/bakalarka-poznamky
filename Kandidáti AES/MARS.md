---
tags:
  - Feistel
  - ModifikovanýFeistel
  - VelkáBezpečnost
---
##### Struktura
- pracuje se čtyřmi 32 bitovými slovy
- počet rund: 32
- 8 kol forward mixing
- 16 kol cryptographic core
- 8 kol backward mixing
- používá 2 S-boxy tvaru 8x32
- celý popis [zde](https://shaih.github.io/pubs/mars/mars-short.pdf)
##### Matematika
- [[GF(2)]]
- [[Modulární aritmetika]]
- [[bitové rotace]]
- [[rotace závislá na vstupu]]
##### Útoky
- útok na redukované verze [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-mars-attacks.pdf)

### Poznámky
- problémy s efektivitou, potenciálně spíše měně zajímavá šifra