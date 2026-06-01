# Talking points - Spørgsmål 10: Blockchain

## Slide 1 - Titel og disposition

- Start med en enkel definition: en blockchain er en kæde af blokke, hvor hver blok kryptografisk peger på den forrige.
- Hovedpointe: Blockchain forsøger at skabe en fælles, manipulationsresistent historik uden én central betroet part.
- Disposition: blokstruktur, hashing, tamper evidence, distribueret konsensus, proof-of-work, problemer, øvelser og perspektiv.

## Slide 2 - Hvad er en blockchain?

- Forklar blokindhold:
  - Data eller transaktioner.
  - Timestamp.
  - Previous hash.
  - Nonce.
  - Egen hash.
- Previous hash binder blokken til den forrige blok.
- Hvis blok 2 indeholder hash af blok 1, og blok 3 indeholder hash af blok 2, opstår en kæde.
- Brug linked list-analogien:
  - Som en linked list, men pointeren er kryptografisk.
- Pointe: Kæden gør historikken struktureret og verificerbar.

## Slide 3 - Hashing og tamper evidence

- Forklar hash som fingerprint:
  - Samme input giver samme hash.
  - Lille ændring giver helt anden hash.
- Hvis nogen ændrer en gammel blok:
  - Blokkens hash ændres.
  - Næste bloks previous hash matcher ikke længere.
  - Alle efterfølgende blokke skal genberegnes.
- Det betyder ikke, at ændring er fysisk umulig, men at manipulation bliver synlig og dyr at skjule.
- Brug begrebet tamper-evident: man kan opdage manipulation.
- Pointe: Integriteten kommer af hashlinkene mellem blokke.

## Slide 4 - Det generelle problem blockchain løser

- Forklar problemet: Hvordan kan flere parter blive enige om en fælles historik uden at have en central databaseadministrator, alle stoler på?
- Blockchain kan være relevant, når:
  - Parter ikke fuldt stoler på hinanden.
  - Man ønsker en fælles append-only historik.
  - Man kan acceptere omkostningerne ved decentral konsensus.
- Eksempel: Kryptovaluta, hvor man skal forhindre double spending uden central bank.
- Understreg begrænsning:
  - Hvis alle parter allerede stoler på én central aktør, er en almindelig database ofte enklere, hurtigere og billigere.
- Pointe: Blockchain er ikke "bedre database"; det er et tradeoff for decentral trust.

## Slide 5 - Forudsætninger

- Blockchain-sikkerhed afhænger af antagelser.
- Uafhængige deltagere:
  - Hvis én aktør kontrollerer det meste, svækkes konsensus.
- Flertal:
  - I proof-of-work må angriberen ikke kontrollere flertallet af hashpower.
- Netværk:
  - Blocks skal kunne spredes til resten af netværket.
  - Store netværksforsinkelser kan give forks.
- Incitamenter:
  - Miners/validators skal have økonomisk grund til at følge protokollen.
- Kryptografi:
  - Hashfunktioner og signaturer skal være sikre.
- Pointe: Blockchain er sikker under bestemte forudsætninger, ikke magisk sikker.

## Slide 6 - Proof-of-work

- Forklar proof-of-work:
  - Mineren prøver forskellige nonces.
  - For hver nonce beregnes block hash.
  - Målet er en hash, der opfylder difficulty, fx starter med et antal nuller.
- Det er svært at finde en gyldig nonce, fordi man må prøve mange muligheder.
- Det er let at verificere, fordi andre bare beregner hashen én gang.
- Difficulty:
  - Justeres for at styre hvor ofte blocks findes.
- Vigtigt begreb:
  - Sikkerheden bygger på, at det kræver reelt arbejde/energi at omskrive historikken.
- Knyt til øvelsen: Når difficulty øges, vokser mining-tiden hurtigt.

## Slide 7 - Konsensus og længste/tungeste kæde

- Forklar at netværket kan få konkurrerende blocks, hvis to miners finder block næsten samtidig.
- Nodes vælger typisk den kæde, der repræsenterer mest samlet arbejde.
- Confirmations:
  - Jo flere blocks der bygges oven på en transaktion, jo dyrere bliver det at ændre den.
- Reorg:
  - Hvis en anden kæde bliver tungere, kan netværket skifte til den.
- Double spend:
  - Angriber forsøger at bruge samme værdi to gange ved at skabe alternativ historik.
- Pointe: Konsensus er probabilistisk i PoW; sikkerheden stiger med confirmations, men finalitet er ikke øjeblikkelig på samme måde som i en central database.

## Slide 8 - Problemer ved proof-of-work

- Energiforbrug:
  - Arbejdet er bevidst dyrt, hvilket giver højt strømforbrug.
- Throughput:
  - Blocks har begrænset størrelse/frekvens, så transaktioner per sekund er lave sammenlignet med centrale systemer.
- Latency:
  - Man venter på confirmations.
- 51%-angreb:
  - Hvis angriber kontrollerer flertallet af hashpower, kan de skabe tungere alternativ kæde.
- Mining centralisering:
  - Mining pools og specialiseret hardware kan samle magt.
- Spildt arbejde:
  - Competing blocks/orphans repræsenterer arbejde, der ikke ender i hovedkæden.
- Pointe: PoW bytter performance og energi for decentral sikkerhed.

## Slide 9 - Øvelse fra undervisningen

- Fortæl C++-øvelsen:
  - I byggede en simpel blockchain.
  - Hver block indeholdt previous hash.
  - Mining bestod i at finde nonce, så hash opfyldte difficulty.
- Forklar hvad øvelsen demonstrerer:
  - Hashkæden gør ændringer synlige.
  - Difficulty påvirker mining-tid kraftigt.
  - Verificering er meget lettere end mining.
- Hvis du selv kan huske tal:
  - Nævn hvilken difficulty der var realistisk på din computer.
  - Hvis ikke, sig kvalitativt at lav difficulty gik hurtigt, mens højere difficulty hurtigt blev upraktisk.
- QuickAndDirty signed linked list:
  - Brug som perspektiv til Satoshis figur med signering ved overdragelse.

## Slide 10 - Perspektiv og afrunding

- Sammenlign med Secure Boot:
  - Begge bruger kæder og kryptografisk integritet.
  - Secure Boot har central root of trust.
  - Blockchain bruger distribueret konsensus.
- Sammenlign med certifikater:
  - Certifikater bygger på CA-tillid.
  - Blockchain prøver at minimere behovet for en central CA-lignende part.
- Hvornår giver blockchain mening?
  - Når man har behov for fælles historik mellem parter uden central tillid.
- Hvornår giver det mindre mening?
  - Når én organisation ejer data og kan drive en almindelig database.
  - Når performance, privacy og enkelhed er vigtigere end decentral konsensus.
- Afslut: Blockchain er et sikkerheds- og distribueret-system-design med klare tradeoffs, ikke en universalløsning.

