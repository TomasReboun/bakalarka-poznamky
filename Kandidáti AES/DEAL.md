---
tags:
  - Feistel
  - MaláBezpečnost
---
DEAL = Data Encryption Algorithm with Larger blocks
##### Struktura
- používá DES jako rundovní funkci
- **S-boxy:** 8 × DES S-box, 6bitů → 4bity
- každý DEAL round tedy obsahuje celých 16 DES rund
- počet rund: 6 pro 128/192 bitový klíč, 8 pro 256 bitový klíč
- key schedule také využívá DES
##### Matematika
- [[GF(2)]]
- [[bitové permutace]]
- [[DES]]

##### Útoky
- DEAL-192 není bezpečnější než DEAL-128 [zde](https://scispace.com/pdf/on-security-of-the-128-bit-block-cipher-deal-40awze57c5.pdf)
- analýza key schedulu (slabé klíče) [zde](https://www.schneier.com/wp-content/uploads/2016/02/paper-deal.pdf)


### Poznámky
- nuda
