# PowerPoint-struktur - Spørgsmål 2: Asymmetrisk nøglekryptering og digitale certifikater

## Slide 1 - Titel og disposition

**Titel:** Asymmetrisk nøglekryptering og digitale certifikater  
**Pointe:** Asymmetrisk kryptografi gør det muligt at kommunikere sikkert med parter, man ikke på forhånd deler en hemmelig nøgle med.  
**Indhold:** Public/private keys, internetbrug, certifikater, PKI, verificering og øvelser.  
**Visual:** Browser -> HTTPS -> Server med certifikat.

## Slide 2 - Problemet: sikker kommunikation på internettet

**Pointe:** Uden kryptografi kan data læses, ændres eller forfalskes under transport.  
**Indhold:** Eavesdropping, man-in-the-middle, identitet og key exchange.  
**Visual:** Client og server med angriber i midten.

## Slide 3 - Public/private key-princippet

**Pointe:** Public key kan deles frit; private key skal holdes hemmelig.  
**Indhold:** Kryptering med public key og dekryptering med private key. Kort RSA-eksempel.  
**Visual:** To nøgler med envejs-flow.

## Slide 4 - Asymmetrisk kryptografi i praksis

**Pointe:** Asymmetrisk krypto bruges især til nøgleudveksling, signering og identitet.  
**Indhold:** TLS, certifikater, digitale signaturer og hybridkryptografi.  
**Visual:** TLS-forløb: handshake -> session key -> symmetrisk krypteret trafik.

## Slide 5 - Digitale certifikater

**Pointe:** Et certifikat binder en public key til en identitet eller et domæne.  
**Indhold:** Subject, Subject Alternative Name, issuer, validity, public key, signature.  
**Visual:** Certifikatkort med felter.

## Slide 6 - PKI og chain of trust

**Pointe:** Tillid skabes gennem en signaturkæde fra servercertifikat til trusted root CA.  
**Indhold:** Root CA, intermediate CA, server certificate, trust store.  
**Visual:** Root -> Intermediate -> Server cert.

## Slide 7 - Udstedelse af certifikat

**Pointe:** CA'en signerer først, når identitet/domæne er valideret.  
**Indhold:** Key pair, CSR, domænevalidering, CA-signatur, installation.  
**Visual:** Procesdiagram fra OpenSSL/CSR til browser.

## Slide 8 - Browserens verificering

**Pointe:** Browseren tjekker både kæde, navn, tid og kryptografisk bevis.  
**Indhold:** Signaturkæde, hostname/SAN, udløbsdato, revocation, TLS proof-of-possession.  
**Visual:** Checkliste.

## Slide 9 - Øvelse fra undervisningen

**Pointe:** OpenSSL-øvelsen viser hele livscyklussen for et certifikat.  
**Indhold:** Selvsigneret certifikat, MMC trust store, `netsh` binding, hosts-fil, browserinspektion.  
**Visual:** Skærmbilledepladsholdere eller trinvis flow.

## Slide 10 - Afrunding og faldgruber

**Pointe:** Certifikater giver ikke sikkerhed alene; de kræver korrekt trust og key management.  
**Indhold:** Private key-beskyttelse, forkert domæne, udløb, selvsignerede certifikater, kompromitterede CA'er.  
**Visual:** "Hvad kan gå galt?"-liste.

