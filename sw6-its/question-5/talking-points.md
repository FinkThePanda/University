# Talking points - Spørgsmål 5: OAuth2 og JWT

## Slide 1 - Titel og disposition

- Start med en tydelig sondring: OAuth2 er primært authorization, OpenID Connect er authentication oven på OAuth2, og JWT er et tokenformat.
- Sig at mange blander begreberne, så din besvarelse vil holde dem adskilt.
- Disposition: OAuth2-problemet, roller, flows, OIDC, JWT-struktur, signering, sårbarheder og best practices.

## Slide 2 - Hvad problem løser OAuth2?

- Forklar delegated authorization:
  - En bruger vil give en applikation begrænset adgang til en ressource uden at dele sit password med applikationen.
- Eksempel: En kalenderapp får adgang til brugerens Google Calendar, men ikke brugerens Google password.
- OAuth2 introducerer access tokens og scopes.
- Scopes begrænser hvad klienten må, fx `read:profile` eller `write:calendar`.
- Pointe: OAuth2 handler ikke nødvendigvis om at logge brugeren ind i klassisk forstand; det handler om adgangsdelegering.

## Slide 3 - OAuth2 roller og elementer

- Gennemgå rollerne:
  - Resource owner: typisk brugeren.
  - Client: applikationen der ønsker adgang.
  - Authorization server: udsteder tokens efter login/consent.
  - Resource server: API'et der beskytter ressourcen.
- Gennemgå tokens:
  - Access token bruges mod resource server.
  - Refresh token kan bruges til at få nye access tokens.
- Redirect URI:
  - Skal være registreret og valideret, fordi authorization code sendes tilbage dertil.
- Scope:
  - Definerer rettigheder og bør være så begrænset som muligt.

## Slide 4 - Authorization Code Flow

- Forklar flowet trinvis:
  1. Client sender brugeren til authorization server.
  2. Brugeren logger ind og giver consent.
  3. Authorization server redirecter tilbage med authorization code.
  4. Client bytter code til access token ved token endpoint.
  5. Client bruger access token mod resource server.
- Forklar hvorfor authorization code er bedre end at sende token direkte via browseren:
  - Token exchange sker server-to-server eller med PKCE-beskyttelse.
  - Mindre eksponering i URL/browser.
- PKCE:
  - Public clients kan ikke holde client secret hemmelig.
  - PKCE binder authorization code til den klient, der startede flowet.

## Slide 5 - Andre grant types

- Client Credentials:
  - Bruges machine-to-machine uden bruger.
  - Client autentificerer sig selv og får token til egne rettigheder.
- Device Code:
  - Bruges til devices med begrænset input, fx TV/CLI.
  - Brugeren logger ind på en anden enhed med kode.
- Refresh Token:
  - Bruges til at få nyt access token uden nyt login.
  - Skal beskyttes ekstra godt, fordi det lever længere.
- Implicit Flow:
  - Historisk brugt til browserapps, men frarådes i moderne setup.
- Resource Owner Password Credentials:
  - Client får brugerens password direkte.
  - Frarådes, fordi det bryder idéen om ikke at dele credentials med client.
- Pointe: Grant types findes, fordi klienter har forskellige evner til at holde secrets og håndtere redirects.

## Slide 6 - OpenID Connect

- Forklar at OIDC udvider OAuth2 med et standardiseret loginlag.
- OAuth2 giver access tokens til ressourcer.
- OIDC giver ID token, som siger noget om brugerens identitet.
- ID token er typisk en JWT med claims:
  - `sub`: stabil brugeridentifikator.
  - `iss`: issuer.
  - `aud`: audience/client.
  - `exp`: udløb.
  - eventuelt email, name osv.
- UserInfo endpoint kan bruges til at hente profiloplysninger.
- Stærk pointe: Access token er til API'et; ID token er til clienten. Man skal ikke blande deres formål.

## Slide 7 - JWT-opbygning

- Forklar formatet: `header.payload.signature`.
- Header:
  - Indeholder typisk token type og algoritme, fx `alg: RS256`.
- Payload:
  - Indeholder claims, fx subject, issuer, audience, expiry, scopes/roles.
- Signature:
  - Beskytter header og payload mod manipulation.
- Forklar Base64URL:
  - JWT er læsbart/enkodet, ikke nødvendigvis krypteret.
  - Man må ikke putte hemmelige data i payload, medmindre tokenet også er krypteret.
- Pointe: Signering giver integritet, ikke fortrolighed.

## Slide 8 - JWT signering og algoritmer

- HS256/HMAC:
  - Samme secret bruges til signering og verificering.
  - Simpelt, men alle der kan verificere kan også signere, hvis de har secret.
- RS256/ES256:
  - Private key signerer.
  - Public key verificerer.
  - Bedre når mange services skal kunne verificere uden at kunne udstede tokens.
- Fordele ved asymmetrisk signering i distribuerede systemer:
  - Authorization server holder private key.
  - Resource servers får public key/JWKS og kan verificere.
- Nævn key rotation og `kid` i header som praktisk aspekt.

## Slide 9 - Kendte JWT-sårbarheder

- `alg=none`:
  - Dårlige biblioteker/konfigurationer accepterer unsigned tokens.
- Algorithm confusion:
  - Systemet blander HMAC og RSA og kan komme til at bruge public key som HMAC secret.
- Svage secrets:
  - HMAC secrets kan brute forces, hvis de er korte eller menneskelige.
- Manglende claim validation:
  - Man skal validere `iss`, `aud`, `exp`, `nbf` og eventuelt scopes/roles.
- For lang levetid:
  - Stateless tokens er svære at tilbagekalde.
- Usikker storage:
  - LocalStorage er sårbart ved XSS.
  - Cookies kræver CSRF-beskyttelse, men kan bruge `HttpOnly`.
- Pointe: JWT er ikke usikkert i sig selv; fejlene opstår ved dårlig validering, opbevaring og key management.

## Slide 10 - Øvelser og best practices

- Knyt til WEB #1 JWT-koden:
  - Spørg om secret er stærk nok.
  - Tjek om algoritmen er korrekt.
  - Tjek `exp`, `nbf`, issuer, audience.
  - Tænk på key storage og rotation.
- Best practices:
  - Brug Authorization Code Flow med PKCE.
  - Brug TLS.
  - Valider alle relevante claims.
  - Brug korte access token lifetimes.
  - Beskyt refresh tokens.
  - Brug velafprøvede biblioteker.
  - Undgå legacy flows.
- Afslut med sondringen igen: OAuth2 styrer adgang, OIDC standardiserer identitet, JWT kan være formatet tokens udtrykkes i.

