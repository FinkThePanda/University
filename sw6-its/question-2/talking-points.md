# Talking points - Spørgsmål 2: Asymmetrisk nøglekryptering og digitale certifikater

## Slide 1 - Titel og disposition

- Start med hovedideen: asymmetrisk kryptografi bruger et nøglepar, hvor den ene nøgle kan deles offentligt, mens den anden holdes privat.
- Sig at det især er vigtigt på internettet, fordi klienter og servere ofte ikke har en fælles hemmelighed på forhånd.
- Giv dispositionen: public/private key, anvendelse i TLS, certifikater, PKI, browser-verificering og øvelsen med OpenSSL.
- Gør rammen klar: "Kryptografien løser ikke kun kryptering, men også identitet og tillid."

## Slide 2 - Problemet: sikker kommunikation på internettet

- Forklar at når en browser taler med en server over et netværk, kan trafikken potentielt observeres eller manipuleres.
- Trusler:
  - Eavesdropping: nogen læser trafikken.
  - Tampering: nogen ændrer trafikken.
  - Man-in-the-middle: nogen udgiver sig for at være serveren.
- Uden en sikker identitetsmekanisme kan klienten ikke vide, om den taler med den rigtige server.
- Symmetrisk kryptering er effektiv, men kræver at begge parter allerede deler en hemmelig nøgle. Det er svært på åbent internet.
- Overgang: asymmetrisk kryptografi hjælper med at etablere tillid og nøgler.

## Slide 3 - Public/private key-princippet

- Forklar nøgleparret:
  - Public key må deles.
  - Private key skal holdes hemmelig.
- Ved kryptering til fortrolighed kan afsender kryptere med modtagers public key, og kun modtager kan dekryptere med private key.
- Ved signering bruges private key til at signere, og public key bruges til at verificere.
- Brug RSA som intuitivt eksempel, men nævn at moderne systemer ofte bruger elliptic curve-baserede algoritmer.
- Understreg at sikkerheden afhænger af, at private key ikke lækkes, og at algoritmen/parametrene er stærke nok.

## Slide 4 - Asymmetrisk kryptografi i praksis

- Forklar at asymmetrisk krypto sjældent bruges til at kryptere al trafik, fordi det er langsommere end symmetrisk krypto.
- I praksis bruges hybridkryptografi:
  - Asymmetrisk kryptografi bruges til identitet, signering og nøgleudveksling.
  - Symmetrisk kryptografi bruges derefter til selve datatrafikken.
- I TLS betyder det typisk, at browser og server etablerer en session key og bruger den til effektiv kryptering.
- Giv eksempel: Når man besøger en HTTPS-side, bruger browseren serverens certifikat til at afgøre, om serverens public key tilhører det domæne, man besøger.

## Slide 5 - Digitale certifikater

- Forklar at et certifikat er en datastruktur, der binder en public key til en identitet, typisk et domænenavn.
- Gennemgå de vigtigste felter:
  - Subject: hvem certifikatet handler om.
  - Subject Alternative Name: hvilke domæner certifikatet gælder for.
  - Issuer: hvem der har udstedt certifikatet.
  - Validity: gyldighedsperiode.
  - Public key: serverens offentlige nøgle.
  - Signature: CA'ens signatur over certifikatdata.
- Pointe: Browseren stoler ikke bare på certifikatet, fordi det findes. Den stoler på det, hvis det er signeret af en kæde, der ender i en trusted root.

## Slide 6 - PKI og chain of trust

- Forklar Public Key Infrastructure som systemet af CA'er, certifikater, trust stores, udstedelse og tilbagekaldelse.
- Root CA'er ligger i browserens/OS'ets trust store. De er trust anchors.
- Intermediate CA'er bruges typisk til at udstede servercertifikater, så root key kan holdes mere beskyttet.
- Chain of trust:
  - Servercertifikatet er signeret af intermediate.
  - Intermediate er signeret af root.
  - Root er trusted lokalt.
- Sig at dette er en form for delegeret tillid: browseren stoler på root CA, og root CA har autoriseret intermediate CA.
- Nævn at hvis en CA kompromitteres eller udsteder forkert, kan mange sites blive påvirket.

## Slide 7 - Udstedelse af certifikat

- Gennemgå processen i et klart flow:
  1. Serverejer genererer et key pair.
  2. Serverejer laver en CSR med public key og domæneoplysninger.
  3. CA validerer, at ansøgeren kontrollerer domænet.
  4. CA signerer certifikatet.
  5. Certifikatet installeres på serveren sammen med private key.
- Forklar forskellen på selvsigneret og CA-signeret:
  - Selvsigneret kan bruges i øvelser/lokale miljøer.
  - Browseren stoler ikke på det, medmindre man selv importerer det som trusted.
- Knyt til OpenSSL-øvelsen: I lavede selv certifikat, importerede det i Windows MMC og bandt det til en HTTPS-port.

## Slide 8 - Browserens verificering

- Forklar browserens checks:
  - Signaturkæden skal være kryptografisk korrekt.
  - Kæden skal ende i en trusted root.
  - Domænenavnet i URL'en skal matche SAN.
  - Certifikatet må ikke være udløbet eller endnu ikke gyldigt.
  - Certifikatet må ikke være tilbagekaldt, afhængigt af OCSP/CRL-checks.
  - Serveren skal bevise, at den har private key, typisk gennem TLS-handshake.
- Understreg at certifikatet alene ikke krypterer trafikken; det muliggør identitet og nøgleetablering.
- Giv eksempel: Hvis man får certifikatadvarsel i browseren, kan det skyldes forkert navn, udløb, self-signed cert eller ukendt CA.

## Slide 9 - Øvelse fra undervisningen

- Fortæl øvelsen som praktisk bevis på teorien:
  - OpenSSL genererede key og certifikat.
  - PFX gjorde det muligt at importere certifikatet inkl. private key.
  - MMC blev brugt til at placere certifikatet i Personal og Trusted Root.
  - `netsh` bandt certifikatet til en HTTPS-port.
  - `hosts`-filen blev ændret, så et lokalt domænenavn pegede på localhost.
  - Browseren kunne derefter inspicere og acceptere certifikatet.
- Forklar hvad man lærer:
  - Certifikater handler både om kryptografi og operativsystemets trust store.
  - Domænenavn/SAN er vigtigt.
  - Private key og certifikat skal passe sammen.

## Slide 10 - Afrunding og faldgruber

- Opsummer: asymmetrisk kryptografi gør secure key exchange, signering og identitet muligt på internettet.
- Certifikater binder public keys til identiteter gennem CA-signaturer.
- PKI giver en skalerbar trust model, men den kræver korrekt CA-praksis og key management.
- Typiske faldgruber:
  - Private key lækkes.
  - Certifikat udløber.
  - Forkert SAN/domæne.
  - Selvsigneret certifikat bruges i produktion uden korrekt trust.
  - Svage algoritmer eller deprecated TLS-versioner.
- Afslut med at TLS/HTTPS bygger på samspillet mellem asymmetrisk krypto, certifikater og symmetrisk sessionkryptering.

