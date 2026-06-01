# PowerPoint-struktur - Spørgsmål 10: Blockchain

## Slide 1 - Titel og disposition

**Titel:** Blockchain og proof-of-work  
**Pointe:** Blockchain er en append-only historik, hvor kryptografiske links og konsensus gør manipulation dyrt.  
**Indhold:** Blokke, hashing, mining, proof-of-work, problemfelt, begrænsninger og øvelser.  
**Visual:** Kæde af blokke.

## Slide 2 - Hvad er en blockchain?

**Pointe:** En blockchain er en linked list af blokke, hvor hver blok peger på forrige hash.  
**Indhold:** Block data, previous hash, timestamp, nonce, block hash.  
**Visual:** Block 1 -> Block 2 -> Block 3 med previous hash.

## Slide 3 - Hashing og tamper evidence

**Pointe:** Hvis gamle data ændres, brydes hashkæden.  
**Indhold:** Hash som fingerprint, ændring i én blok ændrer alle efterfølgende hashes.  
**Visual:** Ændret blok markeret rød, efterfølgende links brudt.

## Slide 4 - Det generelle problem blockchain løser

**Pointe:** Blockchain kan skabe fælles historik uden én central betroet database.  
**Indhold:** Distribueret konsensus, tamper-resistant record, tillid mellem parter der ikke fuldt stoler på hinanden.  
**Visual:** Flere nodes med samme ledger.

## Slide 5 - Forudsætninger

**Pointe:** Blockchain giver kun mening under særlige tekniske og organisatoriske forudsætninger.  
**Indhold:** Mange uafhængige deltagere, ingen kontrollerer flertallet, netværkspropagation, incitamenter, behov for decentral trust.  
**Visual:** Checkliste: "Hvornår giver blockchain mening?"

## Slide 6 - Proof-of-work

**Pointe:** PoW gør det dyrt at skrive historikken, men billigt at verificere den.  
**Indhold:** Mine nonce indtil hash opfylder difficulty; leading zeros; difficulty styrer sandsynlighed/tid.  
**Visual:** Miner prøver nonce 1, 2, 3 ... valid hash.

## Slide 7 - Konsensus og længste/tungeste kæde

**Pointe:** Netværket accepterer den kæde, der repræsenterer mest arbejde.  
**Indhold:** Competing blocks, confirmations, reorgs, hvorfor ældre blocks bliver sværere at ændre.  
**Visual:** Fork med en længere/tungere kæde.

## Slide 8 - Problemer ved proof-of-work

**Pointe:** Sikkerheden købes med omkostninger og begrænsninger.  
**Indhold:** Energiforbrug, lav throughput, latency, mining centralisering, 51%-angreb, double spend.  
**Visual:** Problemkort eller risikotabel.

## Slide 9 - Øvelse fra undervisningen

**Pointe:** C++-øvelsen viser sammenhængen mellem difficulty og beregningstid.  
**Indhold:** Byg blockchain, mine blocks, juster difficulty, fortæl hvilken difficulty der var realistisk på egen computer.  
**Visual:** Tabel: difficulty -> tid/oplevelse.

## Slide 10 - Perspektiv og afrunding

**Pointe:** Blockchain minder om chain of trust, men med distribueret konsensus i stedet for en central root.  
**Indhold:** Sammenlign med Secure Boot/certifikater; hvornår blockchain er relevant og hvornår en almindelig database er bedre.  
**Visual:** Sammenligning: Central database vs blockchain.

