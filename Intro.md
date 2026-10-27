
[1. konference AES](https://nvlpubs.nist.gov/nistpubs/jres/104/1/j41ce-rob.pdf)
- od roku 1977 byl DES (NIST) hlavním standardem pro šifrování informací
- používala ho vláda, veřejnost, bankovní aplikace.
- po úspěšném key exhaustive útoku se blížil jeho  konec.
- DES používá 64-bitový klíč, efektivní je ale jen 56 bitů (nebezpečné)
- 1997 - NIST zahájil vývoj AES. Vládní a vědecké instituce posílali své návrhy. Požadavkem byla **symetrická bloková šifra** s délkou bloku 128 bitů a podpora klíčů délky 128/192/256 bitů.
- Rozhodovací kritéria byli (podle důležitosti):
	- Bezpečnost
	- Efektivita (výpočetní, paměťová, flexibilita)
	- Jiné vlastnosti (vhodnost pro hardware/software, podpora jiné délky klíče, atd.)
- cílem NIST bylo vyvinout algoritmus, který vydrží (podobně jako DES) alespoň 30 let (to se asi povede)
- bylo odesláno 21 návrhů šifer, z nich 15 splnilo požadavky přijetí
- některé šifry byli bezpečnější než 3DES a zároveň efektivnější než DES
- zbytek článku je prezentace jednotlivých šifer.

[2. konference AES](https://nvlpubs.nist.gov/nistpubs/jres/104/4/html/j44ce-dwo.htm)
- měření efektivity algoritmů implementovaných v různých jazycích, v různých procesorech a  čipových kartách
	--> to nás nezajímá
- kryptoanalýza: nalezeny slabinu u SAFER+, LOKI97, FROG, MAGENTA

[3. konference AES](https://www.google.com/search?q=THIRD+ADVANCED+ENCRYPTION+STANDARD+CANDIDATE+CONFERENCE&oq=thi&gs_lcrp=EgZjaHJvbWUqCAgAEEUYJxg7MggIABBFGCcYOzIGCAEQRRg5MgcIAhAAGIAEMhAIAxAuGK8BGMcBGIAEGI4FMgcIBBAAGIAEMgYIBRBFGD0yBggGEEUYPTIGCAcQRRg90gEIMTAwMmowajeoAgCwAgA&sourceid=chrome&source=chrome.ob&ie=UTF-8)
- zabývá se pouze pěticí finalistů: MARS, RC6, Rijndael, Serpent, Twofish
	--> to nás nezajímá

[Status Report](https://upload.wikimedia.org/wikipedia/commons/4/4c/Status_report_on_the_first_round_of_the_development_of_the_advanced_encryption_standard_%28IA_jresv104n5p435%29.pdf)
- shrnutí konferencí: popis struktury a slabin jednotlivých šifer
- dobrý odkazy, jinak nic moc
