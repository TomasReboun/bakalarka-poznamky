---
tags:
  - MaláBezpečnost
  - Jiné
---
##### Struktura
- iterovaná bloková šifra s výrazně key-dependent strukturou
- celý popis [zde](https://web.archive.org/web/20170708064547/http://www.grupolotusbrasil.com.br/grupoconceptprime.com.br/ftp.suporte/util/LIVROS%20E%20TREINAMENTOS/SEGURANCA/criptografia_diciplina/CIE/cd-rom/softwares/Sources/sources.pascal/frog/frog.htm)
- počet rund: 8
- postupně zpracovává každý bajt bloku
- XOR bajtů bloku s bajty klíče
- složitý proces generování klíče
- 8 key-dependent S-boxů: 8bitů -> 8bitů
##### Matematika
- [[GF(2)]]
- [[permutace závislé na klíči]]
- [[S-box závislý na klíči]]
- [[nelineární transformace]]

##### Útoky
- lineární a diferenční útoky v krátkém čase (slabé klíče) [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-frog.pdf)

### Poznámky
- záleží jak vypadají útoky na slabé klíče a kolik těch klíčů je - slabé klíče ~ potenciální strukturální problém


