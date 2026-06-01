# Talking points - Spørgsmål 6: OWASP Web Top 10 A1 og A2

## Slide 1 - Titel og disposition

- Start med at sige, at OWASP Top 10 ikke er en komplet liste over alle webproblemer, men en vigtig prioritering af typiske og alvorlige risici.
- Præsenter de to kategorier:
  - A1 Broken Access Control: brugere får adgang til noget, de ikke burde.
  - A2 Security Misconfiguration: systemet er sat forkert op.
- Sig at du også vil dække CSRF og automatiske sårbarhedsscannere.
- God åbningssætning: "Mange webangreb skyldes ikke avanceret kryptografi, men simple fejl i adgangskontrol og konfiguration."

## Slide 2 - Hvad er OWASP?

- Forklar OWASP som en åben organisation/community for web application security.
- Nævn relevante OWASP-projekter:
  - OWASP Top 10.
  - OWASP Cheat Sheet Series.
  - OWASP Juice Shop som træningsmiljø.
  - OWASP ZAP som proxy/scanner.
- Forklar at Top 10 bruges som fælles sprog mellem udviklere, sikkerhedsfolk og ledelse.
- Understreg at Top 10 ikke er en testmetode i sig selv. Man skal stadig lave threat modeling, code review, scanning og manuel test.

## Slide 3 - A1 Broken Access Control

- Forklar access control:
  - Når systemet afgør, om en autentificeret bruger må udføre en handling eller tilgå en ressource.
- Broken Access Control opstår, når checks mangler, er forkerte eller kun sker client-side.
- Eksempler:
  - IDOR: bruger ændrer `userId=123` til `userId=124`.
  - Almindelig bruger kan kalde admin endpoint direkte.
  - UI skjuler en knap, men API'et kontrollerer ikke rollen.
  - En bruger kan ændre andres data ved at gætte objekt-id'er.
- Pointe: Man må aldrig stole på, at clienten kun sender lovlige requests.

## Slide 4 - Eksempler på Broken Access Control

- Gå dybere i et konkret eksempel:
  - En bruger logger ind og ser sin ordre `/orders/1001`.
  - Brugeren ændrer URL'en til `/orders/1002`.
  - Hvis serveren kun tjekker, at brugeren er logget ind, men ikke at ordren tilhører brugeren, er det Broken Access Control.
- Forklar forskel på authentication og authorization:
  - Brugeren er autentificeret korrekt.
  - Fejlen er, at brugeren ikke burde være autoriseret til objektet.
- Nævn privilege escalation:
  - Horisontal: adgang til andre brugeres data.
  - Vertikal: almindelig bruger får adminrettigheder.
- Relater til API'er: moderne webapps har mange endpoints, og hvert endpoint skal håndhæve authorization.

## Slide 5 - CSRF som adgangskontrolproblem

- Forklar CSRF med browserens cookie-adfærd:
  - Når en bruger er logget ind, sender browseren cookies automatisk til det domæne.
  - En angriber kan lokke browseren til at sende en state-changing request.
  - Serveren tror requesten er legitim, fordi auth-cookien følger med.
- Giv eksempel:
  - Offer er logget ind på Juice Shop.
  - Offer besøger angribers HTML-side.
  - Siden sender en POST-request, der ændrer brugerens email/adresse.
- Forklar hvorfor CSRF især rammer cookie-baseret auth.
- Pointe: CSRF handler ikke om at stjæle passwordet, men om at misbruge brugerens eksisterende login.

## Slide 6 - Mitigation mod A1/CSRF

- Broken Access Control:
  - Deny by default.
  - Server-side checks på alle følsomme handlinger.
  - Object-level authorization: må denne bruger tilgå netop dette objekt?
  - Least privilege.
  - Centraliser adgangskontrol, så logik ikke duplikeres inkonsistent.
  - Logging og alerting på adgangsbrud.
- CSRF:
  - CSRF tokens knytter requesten til en legitim session og side.
  - `SameSite` cookies reducerer cross-site cookie-send.
  - `Origin`/`Referer` checks kan bruges som supplement.
  - Undgå state-changing GET requests.
- Understreg at skjulte UI-elementer ikke er en sikkerhedskontrol. Serveren skal håndhæve reglerne.

## Slide 7 - A2 Security Misconfiguration

- Forklar at security misconfiguration betyder, at systemets opsætning skaber sårbarheder.
- Eksempler:
  - Default credentials.
  - Debug mode i produktion.
  - Stack traces med secrets eller interne paths.
  - Åbne admin interfaces.
  - Unødvendige services eller ports.
  - Fejlkonfigureret CORS, fx `Access-Control-Allow-Origin: *` med credentials.
  - Manglende security headers.
  - Dårlig TLS-konfiguration.
- Pointe: Selv en ellers sikker applikation kan blive usikker af deployment- og konfigurationsfejl.

## Slide 8 - Mitigation mod A2

- Forklar principper:
  - Minimal attack surface: slå alt unødvendigt fra.
  - Hardened baseline: sikre standardkonfigurationer.
  - Automatiseret deployment, så konfiguration er reproducerbar.
  - Environment separation: dev/test/prod må ikke blandes.
  - Secrets management: secrets skal ikke ligge i kode eller config-filer i repo.
  - Regelmæssig patching.
  - Security headers: HSTS, CSP, X-Content-Type-Options, frame-ancestors/X-Frame-Options.
- Nævn at IaC og CI/CD checks kan gøre konfiguration mere kontrollerbar.
- Knyt til ISO/risk: konfiguration er også en del af styring og governance.

## Slide 9 - Automatiske sårbarhedsscannere

- Forklar hvad en scanner gør:
  - Crawler applikationen.
  - Sender testpayloads.
  - Leder efter kendte fejl, headers, versioner, mønstre og responses.
- Fordele:
  - Hurtig baseline.
  - Finder kendte og simple fejl.
  - God til regression og CI.
  - Kan dække mange sider/endpoints.
- Ulemper:
  - False positives kræver manuel vurdering.
  - False negatives: scanner overser fejl.
  - Forstår sjældent forretningslogik.
  - Kan overse Broken Access Control, hvis den ikke tester med flere roller.
  - Kan give støj eller påvirke systemet, hvis den køres ukritisk.
- Pointe: Scannere er værktøjer, ikke dommere.

## Slide 10 - Øvelser og afrunding

- Juice Shop CSRF:
  - Viser hvordan en angribers HTML/JS kan få en logget ind bruger til at udføre handlinger.
- OWASP ZAP:
  - Viser automatiseret scanning og proxy-baseret test.
- Sucuri SiteCheck:
  - Viser ekstern scanning og sammenligning af resultater.
- Charles Proxy:
  - Viser hvordan trafik kan inspiceres, og giver perspektiv til WAF/proxy.
- Afrund med:
  - A1 løses ved konsekvent server-side authorization.
  - A2 løses ved sikker, minimal og reproducerbar konfiguration.
  - Scannere hjælper, men manuel forståelse er nødvendig.

