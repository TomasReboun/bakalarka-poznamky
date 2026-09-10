---
tags:
  - Feistel
  - MaláBezpečnost
---
##### Struktura
- Feistlovo schéma bez prohození po poslední rundě
- počet rund: 6 pro 128/192 bitový klíč, 8 pro 256 bitový klíč
- rundovní funkci tvoří:
	- fixní permutace bajtů
	- XOR klíče
	- Fourierova transformace
	- lineární transformace
- tato permutace je diskrétní mocnění fixního primitivního prvku v GF(2^8)
- 1 S-box: 8bitů -> 8bitů
- rundovní klíče jsou 64 bitové výseče klíče -> symetrie
- jednoduchý key schedule
##### Matematika
- [[GF(2)]]
- [[GF(2^8)]]
- [[diskrétní mocnění]]
- [[Fourierova transformace]]
- [[nelineární transformace]]
- [[bitové permutace]]
##### Útoky
- útok založený na symetrii subklíčů [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-magenta.pdf)
- reflection attack [zde](https://eprint.iacr.org/2007/043.pdf?utm_source=chatgpt.com)
### Poznámky
- nepodařilo se dohledat popis
- potenciálně zajímavá
- [link](https://www.semanticscholar.org/paper/The-MAGENTA-Block-Cipher-Algorithm-Jacobson-Huber/7eea680e2bb04a22f247c381e1a3cdac0a1e6c62)
- [link2](https://link.springer.com/chapter/10.1007/978-3-540-47942-0_3) - odkazuje i na [[LOKI97]] a [[DFC]]
