# PowerPoint-struktur - Spørgsmål 6: OWASP Web Top 10 A1 og A2

## Slide 1 - Titel og disposition

**Titel:** OWASP Web Top 10: Broken Access Control og Security Misconfiguration  
**Pointe:** Mange webbrud skyldes manglende adgangskontrol eller forkert konfiguration.  
**Indhold:** OWASP, A1, CSRF, A2, mitigations og automatiske scannere.  
**Visual:** OWASP Top 10 som risikoliste.

## Slide 2 - Hvad er OWASP?

**Pointe:** OWASP giver fælles sprog, vejledninger og testmiljøer for web security.  
**Indhold:** Open community, Top 10, cheat sheets, Juice Shop, ZAP.  
**Visual:** OWASP-økosystem: Top 10, Juice Shop, ZAP, Cheat Sheets.

## Slide 3 - A1 Broken Access Control

**Pointe:** Brugere må aldrig kunne tilgå funktioner eller data uden korrekt server-side check.  
**Indhold:** IDOR, privilege escalation, bypass af URL-checks, manglende object-level authorization.  
**Visual:** User A forsøger at læse User B's resource.

## Slide 4 - Eksempler på Broken Access Control

**Pointe:** Fejlen opstår ofte, når systemet stoler på clienten.  
**Indhold:** Ændring af `userId`, skjulte admin-knapper, direkte API-kald, manglende rollecheck.  
**Visual:** Request med manipuleret parameter.

## Slide 5 - CSRF som adgangskontrolproblem

**Pointe:** CSRF får browseren til at udføre handlinger som en allerede logget ind bruger.  
**Indhold:** Cookie sendes automatisk, angribers form/link/script, effekt på state-changing actions.  
**Visual:** Victim browser -> target site med cookie, trigget fra attacker site.

## Slide 6 - Mitigation mod A1/CSRF

**Pointe:** Adgang skal håndhæves centralt og server-side.  
**Indhold:** Deny by default, least privilege, per-object checks, CSRF tokens, `SameSite`, origin/referer checks, audit logging.  
**Visual:** Kontrol-lag foran API.

## Slide 7 - A2 Security Misconfiguration

**Pointe:** Sikker software kan blive usikker af dårlig konfiguration.  
**Indhold:** Default credentials, debug mode, åbne services, fejlkonfigureret CORS, manglende headers, dårligt TLS.  
**Visual:** Server med åbne/fejlkonfigurerede porte og settings.

## Slide 8 - Mitigation mod A2

**Pointe:** Konfiguration skal være reproducerbar, minimal og kontrolleret.  
**Indhold:** Hardened baseline, infrastructure as code, secrets management, patching, security headers, environment separation.  
**Visual:** Deployment pipeline med config checks.

## Slide 9 - Automatiske sårbarhedsscannere

**Pointe:** Scannere er nyttige, men kan ikke erstatte forståelse og manuel test.  
**Indhold:** Fordele: hurtige kendte checks, regression, CI. Ulemper: false positives/negatives, forretningslogik overses.  
**Visual:** Vægt: scanner-output vs manuel vurdering.

## Slide 10 - Øvelser og afrunding

**Pointe:** Juice Shop, ZAP, Sucuri og Charles Proxy giver konkrete eksempler.  
**Indhold:** CSRF-angreb, ZAP scanning, Sucuri sammenligning, trafikinspektion.  
**Visual:** Tabel: Øvelse -> OWASP-kategori -> Læring.

