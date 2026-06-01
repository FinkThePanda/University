# Talking points - Spørgsmål 3: Symmetrisk/asymmetrisk kryptering og digitale signaturer

## Slide 1 - Titel og disposition

- Start med at skelne mellem tre mål: fortrolighed, integritet og autenticitet.
- Kryptering beskytter primært fortrolighed: uvedkommende kan ikke læse data.
- Hashing og digitale signaturer beskytter integritet og autenticitet: man kan opdage ændringer og verificere afsender.
- Fortæl dispositionen: symmetrisk krypto, asymmetrisk krypto, hybridkrypto, hashing, signaturer, tillid og øvelser.

## Slide 2 - Symmetrisk kryptering

- Forklar at samme hemmelige nøgle bruges til kryptering og dekryptering.
- Brug AES som eksempel fra øvelsen.
- Fordele:
  - Meget hurtigt.
  - Velegnet til store datamængder.
  - Bruges i TLS efter session key er etableret.
- Ulemper:
  - Key distribution: hvordan deler man nøglen sikkert?
  - Hvis nøglen lækkes, kan alle med nøglen dekryptere og eventuelt forfalske data afhængigt af mode/protokol.
- Nævn at korrekt mode og autentificering betyder noget. Man bør bruge moderne authenticated encryption, fx AES-GCM, når relevant.

## Slide 3 - Asymmetrisk kryptering

- Forklar public/private key pair.
- Public key kan deles, private key skal beskyttes.
- Ved fortrolighed krypterer man med modtagers public key.
- Ved signering signerer man med sin private key.
- Fordele:
  - Løser noget af nøglefordelingsproblemet.
  - Muliggør digitale signaturer og certifikater.
- Ulemper:
  - Langsommere end symmetrisk kryptering.
  - Kræver trust model for public keys.
- Nævn RSA og ECC/ECDSA som eksempler fra undervisningen.

## Slide 4 - Hybridkryptografi

- Forklar at virkelige systemer kombinerer de to typer.
- TLS-eksempel:
  - Browseren verificerer serverens certifikat.
  - Parterne etablerer en session key.
  - Selve trafikken krypteres symmetrisk.
- Hvorfor hybrid?
  - Asymmetrisk krypto er god til nøgleetablering og identitet.
  - Symmetrisk krypto er god til store datamængder.
- Pointe: Man skal ikke se symmetrisk og asymmetrisk som konkurrenter, men som komplementære teknikker.

## Slide 5 - Hashing

- Forklar hashfunktion som en deterministisk envejsfunktion, der laver et fastlængde fingerprint af input.
- Egenskaber:
  - Samme input giver samme hash.
  - Lille ændring i input ændrer hash markant.
  - Det bør være svært at finde input ud fra hash.
  - Det bør være svært at finde to forskellige inputs med samme hash.
- Brug SHA256 fra øvelsen.
- Forklar forskel på hashing og kryptering:
  - Kryptering kan vendes med nøgle.
  - Hashing er ikke beregnet til at blive vendt.
- Nævn at almindelige hurtige hashes ikke er nok til passwords alene, fordi angribere kan brute force hurtigt. Password hashing kræver salt og cost.

## Slide 6 - Digital signatur: mekanismen

- Gennemgå signeringsprocessen:
  1. Afsender beregner hash af beskeden.
  2. Afsender signerer hashen med sin private key.
  3. Besked og signatur sendes.
  4. Modtager beregner selv hash af beskeden.
  5. Modtager verificerer signaturen med afsenders public key.
- Forklar hvorfor man signerer hashen:
  - Beskeden kan være stor.
  - Hashen er fast længde.
  - Signaturen binder sig til hele beskedens indhold gennem hashen.
- Hvis beskeden ændres, matcher hashen ikke længere, og verificeringen fejler.

## Slide 7 - Hvad opnår signaturer?

- Integritet: modtager kan se, om data er ændret efter signering.
- Autenticitet: modtager kan se, at signaturen passer til en bestemt private key.
- Non-repudiation/accountability: afsender kan vanskeligere nægte at have signeret, hvis private key kun kontrolleres af afsender.
- Vigtige begrænsninger:
  - Signaturen beviser ikke, at indholdet er sandt, kun at det er signeret.
  - Hvis private key er stjålet, kan angriberen signere.
  - Hvis public key ikke er trusted, ved man ikke hvem signaturen tilhører.
- Giv eksempel: Software update signing beskytter mod at installere manipuleret kode, hvis signeringsnøglen og verificeringsprocessen er sikre.

## Slide 8 - Tillid i praksis

- Forklar at signaturer kræver en trust model.
- PKI/certifikater: public key bindes til en identitet gennem CA-signatur.
- Web of trust eller manuelt key fingerprint kan også bruges, men skalerer anderledes.
- Key management er centralt:
  - Private keys skal opbevares sikkert.
  - Keys skal kunne roteres.
  - Kompromitterede keys skal kunne tilbagekaldes.
- Algoritmevalg betyder noget:
  - Svage eller forældede algoritmer underminerer sikkerheden.
  - Parametre og random number generation er vigtige, især for signaturalgoritmer.

## Slide 9 - Øvelser fra undervisningen

- Crypto++ ECDSA:
  - Generer private key.
  - Lav public key.
  - Signer besked.
  - Verificer signatur.
  - Det demonstrerer præcis signaturflowet fra teorien.
- SHA256:
  - Viser hashing som fingerprint.
- RSA-besked til sidemand:
  - Viser public/private key-princippet og hvorfor nøglestørrelser betyder noget.
- Crypto chip/firmware signing:
  - Viser at signaturer bruges i Secure Boot og embedded/IoT.
- Blockchain signed linked list:
  - Viser hvordan signering kan bruges til at dokumentere overdragelse og integritet i en kæde.

## Slide 10 - Afrunding

- Saml forskellene:
  - Symmetrisk krypto: hurtig fortrolighed med delt hemmelig nøgle.
  - Asymmetrisk krypto: nøglepar til key exchange, kryptering og signering.
  - Hashing: fingerprint/integritet, men ikke kryptering.
  - Signaturer: integritet, autenticitet og accountability.
- Giv en stærk afsluttende pointe: "Kryptografi er ikke bare algoritmer; sikkerheden afhænger også af nøgler, protokoller, trust og korrekt implementering."

