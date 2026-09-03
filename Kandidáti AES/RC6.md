---
tags:
  - Feistel
  - ModifikovanýFeistel
  - VelkáBezpečnost
---
##### Struktura
- počet rund: 20
- blok rozdělen na čtyři 32 bitová slova, v každé rundě 2. ovlivní 1. a 4. ovlivní 3. a potom se posunou pozice
- toto ovlivnění tvoří:
	- kvadratická transformace
	- 32 bitové modulární násobení
	- XOR
	- rotace závislá na vstupu
	- přičtení klíče
- nepoužívá S-boxy
- celý popis [zde](https://people.csail.mit.edu/rivest/pubs/CRRY98.pdf)
##### Matematika
- [[GF(2)]]
- [[ARX]]
- [[Modulární aritmetika]]
- [[bitové rotace]]
- [[rotace závislá na vstupu]]
- [[kvadratická transformace]]
##### Útoky



