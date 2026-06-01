# PowerPoint-struktur - Spørgsmål 4: Autentifikation på hjemmesider

## Slide 1 - Titel og disposition

**Titel:** Autentifikation på hjemmesider  
**Pointe:** Webautentifikation handler både om login, sessions, transport og korrekt opbevaring af credentials.  
**Indhold:** Authentication vs authorization, Basic Auth, cookies, bearer tokens, password storage og OWASP-risici.  
**Visual:** Bruger -> browser -> webapp -> database.

## Slide 2 - Authentication vs authorization

**Pointe:** Authentication handler om hvem du er; authorization handler om hvad du må.  
**Indhold:** Login, identity, roles/claims, access control.  
**Visual:** To-trins flow: identify -> allow/deny.

## Slide 3 - Basic Authentication

**Pointe:** Basic Auth er simpelt, men kræver HTTPS og omtanke.  
**Indhold:** `Authorization: Basic ...`, Base64, credentials sendes med requests, ingen stærk sessionmodel.  
**Visual:** HTTP request med Authorization header.

## Slide 4 - Cookies og sessions

**Pointe:** Cookies gør sessioner praktiske, men browseren sender dem automatisk.  
**Indhold:** Session ID, server-side session, auth cookie, `HttpOnly`, `Secure`, `SameSite`.  
**Visual:** Login -> Set-Cookie -> efterfølgende requests.

## Slide 5 - Bearer tokens

**Pointe:** Bearer tokens giver API-venlig auth, men tokenet er selve adgangsbeviset.  
**Indhold:** `Authorization: Bearer <token>`, access token, refresh token, kort levetid.  
**Visual:** API request med bearer token.

## Slide 6 - Sikker kommunikation

**Pointe:** Credentials og tokens skal beskyttes under transport.  
**Indhold:** HTTPS/TLS, certifikatvalidering, man-in-the-middle, mixed content.  
**Visual:** Usikker HTTP vs sikker HTTPS.

## Slide 7 - Password hashing og storage

**Pointe:** Passwords må ikke gemmes i klartekst eller med hurtig hash alene.  
**Indhold:** Salt, cost/iterations, Argon2/bcrypt/scrypt/PBKDF2, hvorfor SHA256 alene ikke er nok.  
**Visual:** Password -> salt + password hashing -> stored hash.

## Slide 8 - OWASP Authentication Failures

**Pointe:** Authentication fejler ofte i detaljerne omkring sessions, reset og rate limiting.  
**Indhold:** Svage passwords, credential stuffing, manglende lockout/rate limiting, dårlig session invalidation, læk af tokens.  
**Visual:** Risiko-checkliste.

## Slide 9 - XSS/CSRF som auth-problemer

**Pointe:** Angreb mod browseren kan kompromittere autentificerede brugere.  
**Indhold:** XSS kan stjæle tokens eller udføre handlinger; CSRF udnytter automatisk cookie-send.  
**Visual:** Browser med cookie/token og angribers script/form.

## Slide 10 - Øvelser og afrunding

**Pointe:** Juice Shop og kodegennemgangene viser typiske fejl i praksis.  
**Indhold:** Password hashing review, JWT review, Juice Shop storage/cookies, CSRF og XSS.  
**Visual:** Tabel: Fejl -> Konsekvens -> Mitigation.

