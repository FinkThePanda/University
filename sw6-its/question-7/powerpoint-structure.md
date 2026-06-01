# PowerPoint-struktur - Spørgsmål 7: OWASP Web Top 10 A3 og A5

## Slide 1 - Titel og disposition

**Titel:** OWASP Web Top 10: Supply Chain og Injection  
**Pointe:** Moderne webapps fejler både gennem egne inputflader og gennem afhængigheder.  
**Indhold:** OWASP, A3, A5, XSS, SQLi, XXE, clickjacking, DNS rebinding og WAF.  
**Visual:** Webapp med dependencies på venstre side og brugerinput på højre.

## Slide 2 - OWASP-kontekst

**Pointe:** Top 10 er en prioriteret risikoramme, ikke en komplet testliste.  
**Indhold:** Brug OWASP til at strukturere forklaring, eksempler og mitigations.  
**Visual:** Top 10 som ramme omkring A3 og A5.

## Slide 3 - A3 Software Supply Chain Failures

**Pointe:** En applikation arver risiko fra sine dependencies og build-processer.  
**Indhold:** Tredjepartsbiblioteker, transitive dependencies, package registries, CI/CD, dependency confusion.  
**Visual:** Dependency tree med sårbar pakke.

## Slide 4 - Mitigation mod supply chain failures

**Pointe:** Supply chain security kræver kontrol over hvad man bygger og deployer.  
**Indhold:** Lockfiles, pinning, SCA-scanning, SBOM, trusted registries, code signing, review af updates.  
**Visual:** Pipeline med checks: scan, sign, approve, deploy.

## Slide 5 - A5 Injection

**Pointe:** Injection sker, når data bliver fortolket som kommandoer eller kode.  
**Indhold:** SQL Injection, XPath Injection, XXE, command injection, XSS som browser-side injection.  
**Visual:** User input -> interpreter/database/browser.

## Slide 6 - SQL Injection og XXE

**Pointe:** Backend injection kan lække eller ændre data og i nogle tilfælde læse filer.  
**Indhold:** SQLi via concatenated queries; XXE via XML parser med external entities.  
**Visual:** SQL query med farvet user input; XML entity der peger på fil.

## Slide 7 - Cross-Site Scripting

**Pointe:** XSS lader angriberen køre JavaScript i offerets browserkontekst.  
**Indhold:** Reflected, stored, DOM-based XSS; cookie/token theft, defacement, phishing.  
**Visual:** Angriberinput -> side -> offerbrowser kører script.

## Slide 8 - Mitigation mod injection

**Pointe:** Man skal adskille data fra kode/kommandoer.  
**Indhold:** Prepared statements, output encoding, input validation, CSP, slå XXE fra, least privilege.  
**Visual:** Kontroltabel: Sårbarhed -> Primær mitigation.

## Slide 9 - Clickjacking og DNS rebinding

**Pointe:** Browserens sikkerhedsmodel kan angribes via UI-lag og DNS/origin-tricks.  
**Indhold:** Clickjacking med iframe/overlay; DNS rebinding mod interne services. Mitigation: `frame-ancestors`, host validation, binding og network protections.  
**Visual:** To mini-diagrammer på samme slide.

## Slide 10 - WAF og øvelser

**Pointe:** WAF kan reducere risiko og give synlighed, men løser ikke rodårsagen.  
**Indhold:** Filtering, virtual patching, logging, false positives, bypass. Øvelser: Juice Shop XSS/SQLi/XXE, clickjacking, DNS rebinding, Charles Proxy.  
**Visual:** WAF foran webapp + tabel med øvelser.

