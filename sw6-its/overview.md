# Eksamensoverblik - IT-sikkerhed

Formålet med dette dokument er at give et hurtigt overblik over, hvilket kursusmateriale der især skal bruges til hvert af de 10 eksamensspørgsmål. Brug det som læse- og dispositionsliste: start med de primære lektioner, og brug øvelserne som konkrete eksempler til mundtlig eksamen.

## 1. Grundbegreber inden for IT-sikkerhed

**Primært materiale**

- `lektioner/INTRO og GRUNDBEGREBER/content.md`
- `lektioner/INTRO og GRUNDBEGREBER/SWTITS_GRUNDBEGREBER.pptx`
- Evt. også `SWTITS_INTRO.pptx` og `SWTITS_LOVGIVNING.pptx` fra samme mappe.

**Det skal du kunne**

- Forklare asset, vulnerability, threat, attack, harm og control/countermeasure.
- Forklare CIA-triaden: confidentiality, integrity og availability.
- Koble CIA til konkrete angreb fra resten af kurset: XSS/SQLi, passwords, TLS, secure boot, buffer overflow, blockchain osv.
- Forklare threat-control-paradigmet: en trussel udnytter en sårbarhed, og controls reducerer risikoen.
- Skelne mellem control-typer: physical, procedural/administrative og technical.
- Forklare defense in depth og hvorfor overlappende controls er bedre end ét enkelt sikkerhedslag.

**Risk management / ISO 27000**

- Best practice steps fra ISO 27001/27005-sporet:
  1. Definer risk assessment methodology.
  2. Identificer assets, threats og vulnerabilities.
  3. Vurder likelihood og impact.
  4. Beregn/vurder risk level.
  5. Behandl uacceptable risici: reduce/apply controls, transfer, avoid eller accept.
  6. Dokumenter i risk assessment report, Statement of Applicability og risk treatment plan.
- Perspektiver til ISO 27000-familien:
  - ISO 27000: begreber og ISMS-overblik.
  - ISO 27001: krav til ISMS og certificering.
  - ISO 27002: katalog over sikkerhedskontroller.
  - ISO 27005: risk management.

**Gode eksempler**

- Password hashing som technical control.
- Låst kontor/USB-beskyttelse som physical control.
- Security policy, awareness og change management som administrative controls.

## 2. Asymmetrisk nøglekryptering og digitale certifikater

**Primært materiale**

- `lektioner/KRYPTOLOGI #1/content.md`
- `lektioner/KRYPTOLOGI #1/SWTITS_Crypto_1.pptx`
- `lektioner/KRYPTOLOGI #2/content.md`
- `lektioner/KRYPTOLOGI #2/SWTITS_Crypto_2.pptx`
- `lektioner/WEB #1 A&A/OpenID Connect.pdf`, `OAuth 2.pdf` og webmateriale kan bruges som internet-perspektiv.

**Det skal du kunne**

- Forklare forskellen på symmetrisk og asymmetrisk kryptering.
- Forklare public/private key: public key kan deles, private key skal holdes hemmelig.
- Vise et simpelt RSA-eksempel: kryptering med modtagers public key og dekryptering med modtagers private key.
- Forklare hvad asymmetrisk kryptografi bruges til på internettet:
  - TLS-handshake og etablering af sikre sessioner.
  - Certifikater til server-identitet.
  - Key exchange og signering.

**Digitale certifikater / PKI**

- Forklar certifikatets rolle: binder en public key til et domæne/en identitet.
- Forklar CA, root CA, intermediate CA og chain of trust.
- Forklar hvordan et certifikat udstedes:
  - Generer key pair.
  - Lav CSR/certifikatdata med Common Name/SAN.
  - CA validerer identitet/domæne.
  - CA signerer certifikatet.
- Forklar hvordan browseren verificerer:
  - Tjekker signaturkæde til trusted root.
  - Tjekker domænenavn/SAN.
  - Tjekker gyldighedsperiode og evt. revocation.
  - Tjekker at private key matcher serverens public certifikat gennem TLS.

**Øvelser**

- OpenSSL-øvelsen i `KRYPTOLOGI #2/content.md`: udsted selvsigneret certifikat, importer i Windows MMC, bind til HTTPS-port med `netsh`, ret `hosts`, inspicer certifikat i browser.
- Crypto-øvelser i `KRYPTOLOGI #1`: RSA, AES, SHA256 og Crypto++/ECDSA.

## 3. Symmetrisk/asymmetrisk kryptering og digitale signaturer

**Primært materiale**

- `lektioner/KRYPTOLOGI #1/content.md`
- `lektioner/KRYPTOLOGI #1/SWTITS_Crypto_1.pptx`
- `lektioner/KRYPTOLOGI #2/content.md`
- `lektioner/(U)SIKRE MENNESKER, NETVÆRK OG SYSTEMER/SWTITS_USIKRE_SYSTEMER.pptx` til blockchain/signering-perspektiv.
- `lektioner/FYSISK (U)SIKKERHED/content.md` til crypto chip / firmware signing.

**Det skal du kunne**

- Symmetrisk kryptering:
  - Samme nøgle bruges til kryptering og dekryptering.
  - Hurtigt og velegnet til større datamængder.
  - Eksempel: AES fra øvelsen.
- Asymmetrisk kryptering:
  - Public/private key pair.
  - Langsommere, men løser key distribution og muliggør signaturer.
  - Eksempel: RSA/ECDSA fra øvelsen.
- Hashing:
  - Envejsfunktion, bruges som digest/fingerprint.
  - Eksempel: SHA256.

**Digitale signaturer**

- Signering i praksis:
  1. Hash beskeden.
  2. Signer hashen med private key.
  3. Modtager verificerer signaturen med public key.
  4. Hvis hash/signatur matcher, har man integritet og autenticitet.
- Forklar non-repudiation/accountability: afsender kan vanskeligere nægte at have signeret.
- Forklar hvad man faktisk stoler på:
  - At private key er hemmelig.
  - At public key er korrekt bundet til identiteten via certifikat/PKI eller anden trust model.
  - At algoritmer og parametre er sikre.

**Øvelser**

- Crypto++ ECDSA sign/verify i `KRYPTOLOGI #1/content.md`.
- Crypto chip-øvelsen fra fysisk sikkerhed: sign og verify kode som proof of concept for secure boot/firmware signing.
- Blockchain-øvelsen: linked list/Satoshi-figur med signering ved overdragelse.

## 4. Autentifikation på hjemmesider

**Primært materiale**

- `lektioner/WEB #1 A&A/content.md`
- `lektioner/WEB #1 A&A/Introduktion til sikre Web apps.pdf`
- `lektioner/WEB #1 A&A/Password hashing and storage.pdf`
- `lektioner/WEB #1 A&A/JSON Web Token.pdf`
- `lektioner/WEB #2 OWASP, XSRF og XSS/content.md`
- `lektioner/WEB #2 OWASP, XSRF og XSS/OWASP.pdf`

**Det skal du kunne**

- Skelne mellem authentication og authorization.
- Forklare Basic Authentication:
  - Credentials sendes med requests, typisk Base64 i `Authorization` header.
  - Skal kun bruges over HTTPS.
  - Ingen indbygget session/logout-model.
- Forklare cookie-baseret login:
  - Server opretter session eller udsteder auth-cookie efter login.
  - Browser sender cookie automatisk på samme site.
  - Relevante flags: `HttpOnly`, `Secure`, `SameSite`.
- Forklare bearer tokens:
  - Client sender `Authorization: Bearer <token>`.
  - Den der har tokenet, kan bruge det.
  - Kræver TLS, kort levetid, korrekt opbevaring og evt. refresh token-strategi.

**Sårbarheder**

- OWASP authentication failures:
  - Svage passwords og manglende rate limiting.
  - Dårlig password storage.
  - Session fixation/hijacking.
  - Læk af tokens/cookies via XSS eller usikker storage.
  - Manglende TLS.
- Password hashing:
  - Brug password hashing-algoritmer som Argon2, bcrypt, scrypt eller PBKDF2.
  - Brug unik salt, passende cost/iterations og ingen almindelig hurtig SHA256 alene.
- Web-relaterede risici:
  - XSS kan stjæle tokens/cookies eller udføre handlinger.
  - CSRF rammer cookie-baseret auth, fordi cookies sendes automatisk.

**Øvelser**

- Password hashing-kodegennemgang i `WEB #1 A&A/content.md`.
- JWT-kodegennemgang i samme fil.
- Juice Shop-øvelser om browser storage, cookies, CSRF og XSS.

## 5. OAuth2 og JWT

**Primært materiale**

- `lektioner/WEB #1 A&A/content.md`
- `lektioner/WEB #1 A&A/OAuth 2.pdf`
- `lektioner/WEB #1 A&A/OpenID Connect.pdf`
- `lektioner/WEB #1 A&A/JSON Web Token.pdf`
- `lektioner/WEB #1 A&A/Password hashing and storage.pdf` til auth-baggrund.

**Det skal du kunne**

- Forklare OAuth2 som authorization framework: en client kan få begrænset adgang til en resource owner’s ressourcer uden at få brugerens password.
- Grundelementer:
  - Resource owner.
  - Client.
  - Authorization server.
  - Resource server.
  - Access token, refresh token, scope, redirect URI.
- Grant types/flows:
  - Authorization Code Flow: server-side apps; i moderne brug ofte med PKCE.
  - Authorization Code + PKCE: public clients/mobile/SPAs.
  - Client Credentials: machine-to-machine.
  - Device Code: devices uden god browser/input.
  - Refresh Token: forny access uden nyt login.
  - Resource Owner Password Credentials og Implicit Flow bør omtales som legacy/frarådet i moderne setup.

**OpenID Connect**

- OIDC bygger oven på OAuth2 og tilføjer authentication.
- Introducerer ID token, userinfo endpoint og standardiserede claims.
- OAuth2 svarer primært på "må denne client få adgang?", OIDC svarer også på "hvem er brugeren?".

**JWT**

- Opbygning: `header.payload.signature`.
- Header: typisk `alg` og `typ`.
- Payload: claims som `sub`, `iss`, `aud`, `exp`, `nbf`, roller/scopes.
- Signature:
  - HMAC/HS\* bruger delt secret.
  - RSA/ECDSA/RS*/ES* bruger asymmetriske nøgler.
- Fordele:
  - Selvstændig tokenstruktur.
  - Kan verificeres uden databaseopslag, hvis nøgler/claims er kendt.
- Ulemper:
  - Sværere revocation.
  - Læk er alvorligt indtil expiry.
  - For store tokens kan give overhead.

**JWT-sårbarheder**

- Acceptere `alg=none`.
- Algorithm confusion: blande HS* og RS* forkert.
- Svage secrets.
- Manglende validering af `iss`, `aud`, `exp`, `nbf`.
- For lang levetid.
- Usikker opbevaring i browseren, især ved XSS.

**Øvelser**

- JWT-token-kodegennemgangen i `WEB #1 A&A/content.md`.
- OAuth2/OIDC spørgsmålene e-h i samme fil.

## 6. OWASP Web Top 10: A1 og A2

**Primært materiale**

- `lektioner/WEB #2 OWASP, XSRF og XSS/content.md`
- `lektioner/WEB #2 OWASP, XSRF og XSS/OWASP.pdf`
- `lektioner/WEB #2 OWASP, XSRF og XSS/Cross-Site Request Forgery.pdf`
- `lektioner/Web #4 Opsamling og snak om eksamen/content.md`
- `lektioner/Web #4 Opsamling og snak om eksamen/Web vulnerabilities - Tools and Strategies.pdf`
- `lektioner/Web #4 Opsamling og snak om eksamen/Secure Web Apps 3 Recap.pdf`

**Det skal du kunne**

- Forklare hvad OWASP er: community/organisation med guides, Top 10, cheat sheets og testprojekter som Juice Shop.
- A1 Broken Access Control:
  - Brugere kan tilgå data/funktioner de ikke må.
  - Eksempler: IDOR, privilege escalation, manglende server-side checks, omgåelse af URL-baserede restriktioner.
  - CSRF passer her som angreb hvor browseren udfører uønskede handlinger for en autentificeret bruger.
- Beskyttelse mod Broken Access Control:
  - Deny by default.
  - Server-side authorization på hver relevant handling.
  - Objekt-/record-level access checks.
  - Least privilege.
  - CSRF tokens, `SameSite` cookies og checks af origin/referer hvor relevant.

**A2 Security Misconfiguration**

- Typiske eksempler:
  - Default credentials.
  - Debug endpoints eller stack traces i produktion.
  - Unødvendige services/features.
  - Manglende sikkerhedsheaders.
  - Fejlkonfigureret CORS.
  - Forkert TLS/certifikatopsætning.
- Beskyttelse:
  - Hardened baseline.
  - Automatiseret deployment og konfigurationskontrol.
  - Secrets management.
  - Sikkerhedsheaders som CSP, HSTS, X-Frame-Options/frame-ancestors, X-Content-Type-Options.
  - Regelmæssig scanning og review.

**Automatiske sårbarhedsscannere**

- Fordele:
  - Finder kendte fejl hurtigt.
  - God regression/sanity check.
  - Kan dække mange endpoints.
  - Nyttige i CI/CD og audit.
- Ulemper:
  - False positives/false negatives.
  - Forstår ofte ikke forretningslogik og authorization-regler.
  - Kan overse kædede angreb.
  - Kræver manuel vurdering.
- Relevante værktøjer fra kurset: OWASP ZAP, Sucuri SiteCheck, Charles Proxy.

**Øvelser**

- Juice Shop CSRF-øvelse.
- ZAP/Sucuri-scanning fra Web #4.
- Charles Proxy til at inspicere HTTPS-trafik.

## 7. OWASP Web Top 10: A3 og A5

**Primært materiale**

- `lektioner/WEB #2 OWASP, XSRF og XSS/content.md`
- `lektioner/WEB #2 OWASP, XSRF og XSS/Cross Site Scripting.pdf`
- `lektioner/WEB #3 XXE SQL Injection mv/content.md`
- `lektioner/WEB #3 XXE SQL Injection mv/XML and SQL Injection.pdf`
- `lektioner/WEB #3 XXE SQL Injection mv/Clickjacking and DNS rebinding.pdf`
- `lektioner/Web #4 Opsamling og snak om eksamen/content.md`

**Det skal du kunne**

- A3 Software Supply Chain Failures:
  - Sårbarheder i dependencies, build pipeline, package managers, tredjepartsservices og transitive afhængigheder.
  - Eksempler fra kurset kan kobles til dependency confusion fra `(U)SIKRE MENNESKER, NETVÆRK OG SYSTEMER`.
  - Beskyttelse: dependency pinning/lockfiles, SCA-scanning, SBOM, trusted registries, code signing, review af updates, minimal dependency surface.
- A5 Injection:
  - SQL Injection: user input bliver en del af query.
  - XPath/XXE fra Web #3.
  - XSS: user input bliver eksekveret som JavaScript/HTML i browseren.
- Beskyttelse mod injection:
  - Parameterized queries/prepared statements.
  - Output encoding.
  - Inputvalidering som supplement.
  - CSP mod XSS-impact.
  - Slå XML external entities fra.
  - Least privilege på database/service-konti.

**Clickjacking og DNS rebinding**

- Clickjacking:
  - Offer lokkes til at klikke på skjult/overlejret side i iframe.
  - Beskyttelse: `X-Frame-Options` eller CSP `frame-ancestors`.
- DNS rebinding:
  - Angriber får browserens same-origin-model til at tale med interne/private services via DNS-skift.
  - Beskyttelse: host header validation, bind kun services til nødvendige interfaces, DNS rebinding protection i routere, CORS/origin-checks hvor relevant.

**Web Application Firewalls**

- WAF filtrerer/observerer HTTP-trafik og kan blokere kendte angrebsmønstre.
- Bruges til virtual patching, logging, rate limiting og ekstra kontrol foran webapps.
- Begrænsninger: kan omgås, kan give false positives, løser ikke rodårsagen i applikationen.

**Øvelser**

- Juice Shop: XSS, SQLi, XXE.
- Clickjacking-test af Juice Shop/offentlige sider.
- DNS rebinding-test via hosts-fil.
- Charles Proxy og WAF-perspektivet fra Web #4.

## 8. (U)sikker kode #1/2 - buffer overflow og code injection

**Primært materiale**

- `lektioner/(U)SIKKER KODE #1/content.md`
- `lektioner/(U)SIKKER KODE #1/SWTITS_(U)SIKKER_KODE_1.pptx`
- `lektioner/(U)SIKKER KODE #1/dll.zip`
- `lektioner/(U)SIKKER KODE #1/R4ndoms_OllyDBG(1).zip`
- `lektioner/(U)SIKKER KODE #1/mona.py`
- `lektioner/(U)SIKKER KODE #2/content.md`
- `lektioner/(U)SIKKER KODE #2/SWTITS_(U)SIKKER_KODE_2.pptx`

**Det skal du kunne**

- Forklare stack-princippet:
  - Local variables/buffer.
  - Saved frame pointer.
  - Return address.
  - Function arguments.
- Buffer overflow:
  - Program skriver mere data end bufferens størrelse.
  - Angriber overskriver kontrol-flow, fx return address.
- Code injection:
  - Angriber placerer shellcode i hukommelsen og får programmet til at hoppe dertil.
  - Brug evt. shellcode-calc eksemplet fra `content.md`.

**To metoder mod code injection på stacken**

- Stack canaries / GS cookies:
  - Værdi placeres før return address og kontrolleres før return.
  - Overwrite afsløres, hvis canary ændres.
- NX/DEP:
  - Stack markeres non-executable.
  - Indsprøjtet shellcode kan ikke bare eksekveres fra stacken.

**ROP**

- Return-Oriented Programming omgår NX/DEP ved ikke at køre ny kode på stacken.
- Angriberen kæder eksisterende små instruction sequences/gadgets sammen.
- Kan bruges til at kalde systemfunktioner eller ændre memory permissions.
- ASLR gør ROP sværere, men info leaks kan hjælpe angriberen.

**Fuzzing og anti-fuzzing**

- Fuzzing:
  - Automatisk generering/mutation af inputs for at finde crashes og fejl.
  - Relevant til at finde buffer overflows, parser bugs og edge cases.
- Anti-fuzzing:
  - Teknikker der gør fuzzing mindre effektivt, fx checks, delays, path explosion eller inputkrav der stopper tilfældige inputs.
  - Brug NCC Group-linket i `content.md` som litteraturreference.

**Øvelser**

- ImmunityDebugger, mona.py og R4ndoms_OllyDBG.
- dll.zip / debugging og shellcode.
- Tutorial-link i `(U)SIKKER KODE #2/content.md`.

## 9. Fysisk (u)sikkerhed og (u)sikre OS - Secure Boot

**Primært materiale**

- `lektioner/FYSISK (U)SIKKERHED/content.md`
- `lektioner/FYSISK (U)SIKKERHED/SWTITS_FYSISK_(U)SIKKERHED.pptx`
- `lektioner/(U)SIKRE OPERATIV SYSTEMER/SWTITS_USIKRE_OPERATIV_SYSTEMER.pptx`
- `lektioner/FYSISK (U)SIKKERHED/WindowsHookExample.zip`
- `lektioner/FYSISK (U)SIKKERHED/AntibIoTic - Protecting IoT Devices Against DDoS Attacks.pdf`

**Det skal du kunne**

- Forklare formålet med Secure Boot:
  - Sikre at systemet kun starter betroet og signeret kode.
  - Beskytte mod bootkits, evil maid-angreb og kompromitteret firmware/bootloader.
- Forklare chain of trust:
  - Hardware root of trust starter kæden.
  - Hvert boot-led verificerer signaturen/hash på næste led, før det køres.
  - Hvis et led ikke verificerer, stoppes boot eller systemet går i recovery.
- Kryptografi i Secure Boot:
  - Hashing til integritet.
  - Digitale signaturer til autenticitet.
  - Public keys/certifikater indlejret eller lagret i hardware/firmware.
  - Private signing keys skal beskyttes ekstremt godt.

**Implementeringsudfordringer**

- Key management: hvem må signere, rotere og tilbagekalde keys?
- Opdateringer: hvordan opdateres firmware sikkert uden at åbne for rollback?
- Fysisk adgang: angriberen kan manipulere hardware, storage eller bootmedier.
- Supply chain og hardware backdoors.
- Recovery/debug interfaces kan blive angrebsflader.
- Secure Boot beskytter bootkæden, men ikke nødvendigvis alt efter OS’et er startet.

**iPhone / mobile perspektiv**

- Brug iPhone boot sequence som eksempel fra slides:
  - Boot ROM som immutable root of trust.
  - LLB/iBoot/kernel verificeres trin for trin.
  - Signering og Apple-kontrollerede keys binder software til platformen.
- Perspektiver til jailbreaking: angreb forsøger at bryde et led i chain of trust.

**Øvelser**

- Crypto chip-øvelsen: sign og verify kode som proof of concept for secure boot/firmware signing.
- Rubber Ducky defense i `WindowsHookExample.zip`: fysisk adgang og HID-angreb.
- Evil maid-scenariet fra slides er godt som mundtligt eksempel.

## 10. (U)sikre mennesker, netværk og systemer - blockchain

**Primært materiale**

- `lektioner/(U)SIKRE MENNESKER, NETVÆRK OG SYSTEMER/content.md`
- `lektioner/(U)SIKRE MENNESKER, NETVÆRK OG SYSTEMER/SWTITS_USIKRE_SYSTEMER.pptx`
- `lektioner/(U)SIKRE MENNESKER, NETVÆRK OG SYSTEMER/QuickAndDirty_signed_linked_list.zip`

**Det skal du kunne**

- Forklare blockchain som en kæde af blokke:
  - Hver blok indeholder data/transaktioner, timestamp, previous hash, nonce og egen hash.
  - Hvis en gammel blok ændres, ændres dens hash og alle efterfølgende links brydes.
- Tegn gerne:
  - `Block 1 -> Block 2 -> Block 3`
  - Hver blok peger på forrige hash.
  - Mining finder en nonce så hash opfylder difficulty.
- Forklar hvilket problem blockchain løser:
  - Distribueret konsensus om en historik uden én central betroet part.
  - Tamper-resistant record under særlige forudsætninger.
- Forudsætninger:
  - Mange uafhængige deltagere.
  - Ingen angriber kontrollerer flertallet af hashpower/stake/consensus-magt.
  - Netværket kan udbrede blocks nogenlunde stabilt.
  - Incitamenter får deltagere til at følge protokollen.

**Proof-of-work**

- Mineren prøver nonces indtil block hash opfylder difficulty, fx et antal førende nuller.
- Det er svært at finde en gyldig nonce, men let at verificere.
- Difficulty kan justeres så blocks findes med ønsket tempo.
- Problemer:
  - Energiforbrug.
  - Lav throughput/latency.
  - 51%-angreb/double spend.
  - Mining centralisering.
  - Spildt arbejde hvis kæder konkurrerer.

**Øvelser**

- Byg blockchain med C++ fra `content.md` og slide-tutorial.
- Mine nogle blocks og vær klar til at fortælle, hvilken difficulty der var realistisk på egen computer.
- `QuickAndDirty_signed_linked_list.zip`: brug som perspektiv til Satoshi-lignende linked list med signering ved overdragelse.
