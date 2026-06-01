# Talking points - Spørgsmål 4: Autentifikation på hjemmesider

## Slide 1 - Titel og disposition

- Start med at definere autentifikation: processen hvor systemet afgør, hvem brugeren eller klienten er.
- Skel fra authorization: efter login skal systemet stadig afgøre, hvad brugeren må.
- Fortæl at du vil gennemgå Basic Auth, cookies/sessions, bearer tokens, sikker transport, password storage og typiske OWASP-fejl.
- Sæt rammen: webauth er svært, fordi browser, server, netværk, tokens, cookies og brugeradfærd spiller sammen.

## Slide 2 - Authentication vs authorization

- Authentication: "Hvem er du?" Eksempel: brugernavn/password, MFA, certifikat, login via OIDC.
- Authorization: "Hvad må du?" Eksempel: må brugeren læse denne ordre, ændre denne konto eller kalde admin-API?
- Forklar at en bruger godt kan være korrekt autentificeret, men stadig ikke autoriseret til en bestemt handling.
- Giv webeksempel:
  - Login lykkes.
  - Brugeren får session.
  - Hver API-handling skal stadig kontrollere rolle og objektadgang.
- Knyt til OWASP: Broken Access Control er ofte authorization-fejl, ikke login-fejl.

## Slide 3 - Basic Authentication

- Forklar mekanismen:
  - Browser/client sender `Authorization: Basic <base64(username:password)>`.
  - Base64 er encoding, ikke kryptering.
- Basic Auth er enkel og kan være brugbar til simple APIs eller interne systemer.
- Men den har begrænsninger:
  - Credentials sendes med hver request.
  - Kræver HTTPS, ellers kan credentials opsnappes.
  - Ingen god indbygget logout/session invalidation.
  - Ikke velegnet til moderne brugeroplevelser uden ekstra mekanismer.
- Pointe: Basic Auth er ikke automatisk usikkert, men det er let at bruge dårligt.

## Slide 4 - Cookies og sessions

- Forklar typisk loginflow:
  1. Bruger sender credentials.
  2. Server validerer.
  3. Server opretter session eller auth cookie.
  4. Browser sender cookie automatisk på senere requests.
- Server-side session:
  - Cookie indeholder session ID.
  - Server slår session op i database/memory.
- Cookie flags:
  - `HttpOnly`: JavaScript kan ikke læse cookien, reducerer skade ved XSS.
  - `Secure`: sendes kun over HTTPS.
  - `SameSite`: reducerer CSRF-risiko.
- Forklar risiko: fordi cookies sendes automatisk, kan CSRF være relevant.

## Slide 5 - Bearer tokens

- Forklar bearer token-princippet: den der bærer tokenet, får adgang.
- Typisk sendes det som `Authorization: Bearer <token>`.
- Bruges ofte i APIs, SPAs, mobile apps og OAuth2.
- Fordele:
  - API-venligt.
  - Kan indeholde scopes/claims.
  - Kan være stateless, hvis JWT.
- Risici:
  - Hvis token lækkes, kan angriber bruge det.
  - Skal beskyttes i transport og storage.
  - Kort levetid og refresh-strategi er vigtigt.
- Nævn at bearer tokens ikke automatisk er bedre end cookies; sikkerheden afhænger af kontekst og opbevaring.

## Slide 6 - Sikker kommunikation

- Forklar at autentifikation er meningsløs, hvis credentials eller tokens kan opsnappes.
- HTTPS/TLS beskytter mod eavesdropping og manipulation under transport.
- Certifikater hjælper browseren med at verificere serverens identitet.
- Uden TLS kan Basic Auth, cookies og bearer tokens lækkes.
- Nævn også mixed content og forkert certifikatvalidering som problemer.
- Pointe: Alle auth-mekanismer skal antages kompromitterede, hvis transportlaget er usikkert.

## Slide 7 - Password hashing og storage

- Forklar at passwords aldrig bør gemmes i klartekst.
- Almindelige hurtige hashes som SHA256 alene er ikke nok til passwords, fordi angribere kan prøve enorme mængder passwords hurtigt.
- Krav til password storage:
  - Unik salt per password.
  - Langsom password hashing-algoritme.
  - Justerbar cost/iterations.
  - Gerne memory-hard algoritme.
- Nævn anbefalede algoritmer: Argon2, bcrypt, scrypt, PBKDF2.
- Knyt til øvelsen:
  - Koden med SHA256(password + salt) er bedre end klartekst, men ikke god nok som password hashing.
  - PBKDF2-eksemplet er tættere på anbefalingerne, men iterations skal vurderes efter nutidig standard og trusselsmodel.

## Slide 8 - OWASP Authentication Failures

- Forklar at authentication failures ofte handler om svagheder omkring loginprocessen.
- Eksempler:
  - Svage passwords accepteres.
  - Ingen MFA på følsomme konti.
  - Ingen rate limiting eller lockout mod brute force/credential stuffing.
  - Sessioner udløber ikke korrekt.
  - Password reset er svagt.
  - Tokens har for lang levetid eller valideres forkert.
  - Fejlmeddelelser afslører om brugernavn findes.
- Controls:
  - MFA.
  - Rate limiting.
  - Sikker password hashing.
  - Session timeout og rotation efter login.
  - Logging og detection.

## Slide 9 - XSS/CSRF som auth-problemer

- Forklar XSS:
  - Angriber får JavaScript til at køre i offerets browser på det legitime site.
  - Det kan bruges til at stjæle tokens, lave handlinger eller vise falsk UI.
  - `HttpOnly` kan beskytte cookies mod direkte læsning, men XSS kan stadig udføre handlinger i browseren.
- Forklar CSRF:
  - Angriber får offerets browser til at sende en request til et site, hvor offeret allerede er logget ind.
  - Cookies sendes automatisk, så serveren tror requesten kommer legitimt fra brugeren.
- Mitigations:
  - CSRF tokens.
  - `SameSite` cookies.
  - Origin/referer checks.
  - Brug af bearer token i Authorization header kan reducere klassisk CSRF, men introducerer storage-risiko.

## Slide 10 - Øvelser og afrunding

- Knyt til WEB #1:
  - Password hashing review viste typiske fejl i hjemmelavet password storage.
  - JWT review viste problemer ved token-generering og signering.
- Knyt til Juice Shop:
  - Browser storage og cookies viser, hvor auth-data ligger.
  - CSRF-øvelsen viser risikoen ved automatisk cookie-send.
  - XSS-øvelsen viser hvordan client-side sårbarheder kan kompromittere autentificerede sessions.
- Afslut:
  - God webauth kræver sikker transport, stærk password storage, fornuftige sessions/tokens og beskyttelse mod browser-angreb.
  - Authentication og authorization skal begge håndhæves server-side.

