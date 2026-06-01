# Talking points - Spørgsmål 1: Grundbegreber inden for IT-sikkerhed

Brug noterne som et mundtligt manuskript. Ideen er ikke at læse dem op ordret, men at have et klart spor gennem hvert slide.

## Slide 1 - Titel og disposition

- Start med at definere IT-sikkerhed bredt: det handler ikke kun om hackere og tekniske angreb, men om at beskytte værdier mod hændelser, der kan skade organisationen.
- Sig at du vil bruge grundbegreberne som en ramme for resten af kurset: webangreb, kryptografi, secure boot, usikker kode og blockchain kan alle beskrives med de samme byggesten.
- Forklar din disposition: først de centrale begreber, derefter CIA-triaden, så risk management, ISO 27000 og til sidst perspektivering.
- God åbningssætning: "Hvis man skal analysere sikkerhed professionelt, skal man kunne svare på: hvad beskytter vi, mod hvem, hvad kan gå galt, og hvilke kontroller reducerer risikoen?"

## Slide 2 - Centrale begreber

- Forklar `asset`: noget af værdi. Det kan være data, systemer, penge, omdømme, drift, personoplysninger, kildekode eller fysisk udstyr.
- Forklar `vulnerability`: en svaghed, som kan udnyttes. Eksempel: manglende inputvalidering, svage passwords, åben USB-port, forkert CORS-konfiguration.
- Forklar `threat`: en potentiel årsag til skade. Det kan være en angriber, en fejlkonfiguration, en brand, en insider eller malware.
- Forklar `attack`: når en threat aktivt udnytter en vulnerability.
- Forklar `harm`: konsekvensen, fx datalæk, nedetid, tab af integritet eller økonomisk skade.
- Forklar `control`: en modforanstaltning, der reducerer sandsynlighed eller konsekvens. Fx TLS, adgangskontrol, awareness, logging eller fysisk lås.
- Bind det sammen med en enkel kæde: "Et asset har en vulnerability; en threat kan udnytte den gennem et attack; det giver harm; controls forsøger at bryde kæden."

## Slide 3 - Vulnerability-Threat-Control paradigmet

- Forklar at paradigmet hjælper med at undgå løse sikkerhedsudsagn. Man skal ikke bare sige "det er usikkert"; man skal kunne sige hvilken sårbarhed, hvilken trussel og hvilken skade.
- Gennemgå angriberens tre forudsætninger: metode, mulighed og motiv.
- Metode: angriberen skal have en teknik, fx SQL injection eller phishing.
- Mulighed: systemet skal være eksponeret eller sårbart, fx et endpoint uden adgangskontrol.
- Motiv: angriberen skal have en grund, fx økonomisk gevinst, prestige, politisk motiv eller nysgerrighed.
- Forklar control-effekter:
  - Prevent: forhindre angreb, fx prepared statements mod SQL injection.
  - Deter: gøre angreb mindre attraktivt, fx logging og juridiske konsekvenser.
  - Detect: opdage angreb, fx IDS, alarmer og audit logs.
  - Mitigate: reducere skade, fx rate limiting eller segmentering.
  - Recover: komme tilbage efter skade, fx backup og incident response.
- Perspektiver til defense in depth: man vil helst have flere kontroller, fordi én kontrol ofte kan fejle.

## Slide 4 - CIA-triaden

- Forklar at CIA-triaden er den klassiske model for sikkerhedsmål.
- Confidentiality: kun autoriserede må læse data. Eksempler: kryptering, TLS, adgangskontrol, password hashing. Trusler: datalæk, eavesdropping, stjålne credentials.
- Integrity: data må kun ændres af autoriserede og på korrekt måde. Eksempler: digitale signaturer, hashes, inputvalidering, database constraints. Trusler: SQL injection, manipulation af transaktioner, ændret firmware.
- Availability: systemer og data skal være tilgængelige for autoriserede brugere. Eksempler: redundans, DDoS-beskyttelse, backup, capacity management. Trusler: DDoS, ransomware, nedbrud.
- Nævn at nogle angreb rammer flere mål samtidig. Fx ransomware rammer availability, men kan også true confidentiality hvis data eksfiltreres.
- Knyt til kurset: XSS kan true confidentiality via cookie theft; Secure Boot beskytter integrity i bootkæden; blockchain forsøger at beskytte integrity i en historik.

## Slide 5 - Typer af kontroller

- Forklar at sikkerhed ikke kun er tekniske mekanismer.
- Physical controls: låse, adgangskort, vagter, kameraer, USB-port-beskyttelse, Faraday-beskyttelse. Knyt til fysisk sikkerhed/Rubber Ducky.
- Administrative/procedural controls: politikker, processer, risk assessments, awareness, change management, ansvarsfordeling, lovkrav.
- Technical controls: kryptering, passwords, firewalls, access control, WAF, logging, scanning, Secure Boot.
- Forklar defense in depth med eksempel: En webapp bruger TLS, sikre cookies, CSRF tokens, server-side authorization, logging og rate limiting. Hvis XSS opstår, kan `HttpOnly` og CSP stadig reducere skade.
- Pointe: en god sikkerhedsplan kombinerer controls, fordi mennesker, processer og teknologi alle kan fejle.

## Slide 6 - Risk management proces

- Forklar at risk management handler om prioritering. Man kan ikke fjerne al risiko, så man skal vælge rationelt.
- Første trin: identificer assets. Hvad er vigtigt for organisationen?
- Andet trin: identificer threats og vulnerabilities. Hvad kan gå galt, og hvor er systemet svagt?
- Tredje trin: vurder likelihood og impact. Hvor sandsynligt er det, og hvor alvorligt bliver det?
- Fjerde trin: beregn eller kategoriser risiko. Det kan være kvalitativt, fx low/medium/high, eller kvantitativt, hvis man har data.
- Femte trin: vælg behandling af risikoen.
- Sjette trin: dokumenter og review. Risiko ændrer sig, når systemer, trusler og organisationen ændrer sig.
- Sig at risk management ikke er en engangsaktivitet, men en løbende proces.

## Slide 7 - Risk treatment

- Forklar de fire hovedmuligheder:
- Reduce/mitigate: indfør kontroller. Fx brug MFA for at reducere risikoen ved stjålne passwords.
- Transfer: flyt noget af risikoen, fx cyber insurance eller outsourcing med kontraktkrav. Understreg at ansvar sjældent forsvinder helt.
- Avoid: stop aktiviteten. Fx luk et usikkert legacy endpoint, hvis det ikke er nødvendigt.
- Accept: accepter risikoen bevidst, hvis omkostningen ved kontrol er større end risikoen, eller risikoen er lav.
- Giv et konkret eksempel: Hvis en offentlig login-side har credential stuffing-risiko, kan man reducere med rate limiting og MFA, overvåge logs, og acceptere en rest-risiko.
- Forklar risk matrix: høj likelihood og høj impact skal prioriteres først; lav impact/lav likelihood kan ofte accepteres.

## Slide 8 - ISO 27000-familien

- Forklar ISO 27000-familien som en standardiseret ramme for informationssikkerhed og ISMS.
- ISO 27000: begreber, definitioner og introduktion til ISMS.
- ISO 27001: kravstandarden. Den kan man certificeres efter, og den beskriver hvordan en organisation styrer informationssikkerhed.
- ISO 27002: katalog med kontroller og vejledning.
- ISO 27005: risk management for informationssikkerhed.
- Forklar ISMS: Information Security Management System. Det handler om ledelse, ansvar, processer, dokumentation og kontinuerlig forbedring.
- Nævn centrale dokumenter: scope, information security policy, risk assessment methodology, Statement of Applicability, risk treatment plan.
- Pointe: ISO 27001 handler ikke om at installere ét bestemt værktøj, men om at have en systematisk, dokumenteret og ledelsesforankret måde at styre sikkerhed på.

## Slide 9 - Perspektiv til resten af kurset

- Brug dette slide til at vise, at grundbegreberne kan anvendes på alle emner.
- Web: SQL injection er en vulnerability; threat er angriber; harm er datalæk; control er prepared statements.
- Auth: svage passwords er vulnerability; credential stuffing er threat/attack; controls er password hashing, rate limiting og MFA.
- Krypto: TLS beskytter confidentiality og integrity under transport.
- Secure Boot: beskytter integrity af bootkæden gennem signaturer og chain of trust.
- Buffer overflow: sårbarhed i memory handling; attack kan give code execution; controls er canaries, NX/DEP, ASLR og fuzzing.
- Blockchain: forsøger at beskytte integrity i en distribueret historik.
- Pointe: En eksamensbesvarelse bliver stærkere, hvis man hele tiden kan koble teknik til risiko og sikkerhedsmål.

## Slide 10 - Afrunding

- Saml op med én sætning: "IT-sikkerhed handler om at identificere værdier, forstå trusler og sårbarheder, vurdere risiko og vælge passende kontroller."
- Gentag de vigtigste begreber: asset, vulnerability, threat, attack, harm, control.
- Gentag CIA som grundmodel for hvad man beskytter.
- Afslut med ISO/risk management: organisationer skal arbejde systematisk, dokumenteret og løbende med risiko.
- Hvis eksaminator spørger videre, er gode retninger: eksempler på controls, forskel på threat/vulnerability, eller hvordan ISO 27001 bruger risk assessment til at vælge kontroller.

