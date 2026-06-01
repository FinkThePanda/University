# Talking points - Spørgsmål 7: OWASP Web Top 10 A3 og A5

## Slide 1 - Titel og disposition

- Start med at sige, at spørgsmålet dækker to meget forskellige risikoområder:
  - Supply chain: risiko fra den kode og infrastruktur, vi afhænger af.
  - Injection: risiko fra input, der bliver fortolket som kode/kommandoer.
- Sig at du også vil dække XSS, SQLi, XXE, clickjacking, DNS rebinding og WAF.
- God framing: "Moderne webapps er både afhængige af meget tredjepartskode og eksponeret for mange inputflader."

## Slide 2 - OWASP-kontekst

- Forklar kort OWASP igen: fælles ramme og sprog for web application security.
- Top 10 er ikke kun tekniske bugs, men risikokategorier.
- A3 og A5 viser to retninger:
  - A3 handler om det, man importerer, bygger og deployer.
  - A5 handler om det, man modtager som input og sender videre til interpreters.
- Understreg at man bør forklare både angreb, konsekvens og mitigation for hver kategori.

## Slide 3 - A3 Software Supply Chain Failures

- Forklar supply chain i software:
  - Dependencies.
  - Transitive dependencies.
  - Package registries.
  - Build pipeline.
  - CI/CD.
  - Container images.
  - Tredjepartsservices.
- Supply chain failure kan være:
  - Sårbart bibliotek.
  - Ondsindet pakke.
  - Dependency confusion.
  - Kompromitteret build server.
  - Manglende signering/verificering af artifacts.
- Eksempel: En npm/pip/NuGet-pakke med samme navn i public registry får buildsystemet til at hente angriberens version.
- Pointe: Man kan skrive sin egen kode korrekt, men stadig blive kompromitteret gennem afhængigheder.

## Slide 4 - Mitigation mod supply chain failures

- Lockfiles og version pinning:
  - Gør builds reproducerbare.
  - Reducerer risiko for utilsigtede dependency changes.
- SCA-scanning:
  - Scanner dependencies for kendte CVE'er.
- SBOM:
  - Software Bill of Materials giver overblik over komponenter.
- Trusted registries:
  - Brug interne eller kontrollerede package feeds.
- Code signing:
  - Verificer at artifacts kommer fra den rigtige kilde.
- Review af updates:
  - Ikke blindt auto-merge alle dependency updates.
- Principle of least dependency:
  - Undgå unødvendige dependencies.
- Pointe: supply chain security handler både om teknik, proces og governance.

## Slide 5 - A5 Injection

- Forklar injection generelt: data fra brugeren bliver fortolket som kode eller kommandoer i en interpreter.
- Interpreters kan være:
  - SQL database.
  - Browser/JavaScript engine.
  - XML parser.
  - OS shell.
  - XPath engine.
- Eksempel på mønster:
  - Applikationen bygger en kommando ved string concatenation.
  - Angribers input ændrer kommandoens betydning.
- Konsekvenser:
  - Datalæk.
  - Dataændring.
  - Login bypass.
  - Remote code execution i værste fald.
- Pointe: Den grundlæggende mitigation er at adskille data fra kode.

## Slide 6 - SQL Injection og XXE

- SQL Injection:
  - Forklar med et login-query: `SELECT * FROM users WHERE name = '$input'`.
  - Hvis input bliver `' OR '1'='1`, ændres queryens logik.
  - Konsekvens kan være bypass, datadump, ændringer eller sletning.
- Mitigation:
  - Prepared statements/parameterized queries.
  - ORM korrekt brugt.
  - Least privilege for databaseuser.
  - Inputvalidering som supplement.
- XXE:
  - XML External Entity opstår, når XML parser tillader eksterne entities.
  - Angriber kan få serveren til at læse lokale filer eller lave SSRF-lignende requests.
- Mitigation:
  - Disable external entities.
  - Brug sikre parser defaults.
  - Undgå XML features man ikke bruger.

## Slide 7 - Cross-Site Scripting

- Forklar XSS som injection i browseren.
- Stored XSS:
  - Payload gemmes på serveren og rammer alle, der ser siden.
- Reflected XSS:
  - Payload kommer fra request og reflekteres i response.
- DOM-based XSS:
  - Client-side JavaScript håndterer data usikkert og skriver til DOM.
- Konsekvenser:
  - Cookie/token theft.
  - Handlinger på vegne af bruger.
  - Defacement.
  - Phishing UI på legitimt domæne.
- Mitigation:
  - Context-aware output encoding.
  - Sanitization hvor HTML er tilladt.
  - CSP som skadebegrænsning.
  - `HttpOnly` cookies.
  - Undgå farlige DOM sinks som `innerHTML` med usikkert input.

## Slide 8 - Mitigation mod injection

- Saml mitigations i principper:
  - Brug parameterized APIs i stedet for string concatenation.
  - Encode output i korrekt kontekst: HTML, attribute, JavaScript, URL.
  - Valider input med allowlists, især for format og type.
  - Brug least privilege, så en injection ikke får fuld adgang.
  - Brug sikre parserindstillinger.
  - Test med både code review, unit tests og dynamisk test.
- Gør det klart at inputvalidering alene ikke er nok mod SQLi/XSS. Den vigtigste kontrol er korrekt kontekstbehandling.
- Knyt til Juice Shop: øvelserne viser, hvordan payloads virker i en rigtig webapp.

## Slide 9 - Clickjacking og DNS rebinding

- Clickjacking:
  - Angriber lægger et legitimt site i en usynlig eller manipuleret iframe.
  - Offer tror de klikker på noget uskyldigt, men klikker på handling i det legitime site.
  - Mitigation: CSP `frame-ancestors` eller `X-Frame-Options`.
- DNS rebinding:
  - Angriber udnytter, at browserens same-origin er baseret på scheme/host/port.
  - Et domæne kan først pege på angribers server og derefter på en intern IP.
  - Browseren kan dermed bruges som bro til interne services.
  - Mitigation: Host header validation, bind services korrekt, DNS rebinding protection, auth på interne services.
- Pointe: Begge angriber browserens måde at forbinde bruger, origin og UI/netværk.

## Slide 10 - WAF og øvelser

- Forklar WAF:
  - Web Application Firewall sidder foran webappen og analyserer HTTP-trafik.
  - Kan blokere kendte payloads, rate limite, logge og give virtual patching.
- Fordele:
  - Hurtig beskyttelse mod kendte mønstre.
  - Ekstra synlighed.
  - Kan beskytte legacy apps midlertidigt.
- Begrænsninger:
  - Kan omgås.
  - False positives kan blokere legitime brugere.
  - Forstår ikke altid appens forretningslogik.
  - Løser ikke den sårbare kode.
- Øvelser:
  - Juice Shop XSS, SQLi og XXE.
  - Clickjacking-test.
  - DNS rebinding-test via hosts-fil.
  - Charles Proxy som analogi til trafikinspektion/WAF.
- Afslut: A3 kræver kontrol med afhængigheder; A5 kræver sikker håndtering af input.

