# PowerPoint-struktur - Spørgsmål 5: OAuth2 og JWT

## Slide 1 - Titel og disposition

**Titel:** OAuth2, OpenID Connect og JWT  
**Pointe:** OAuth2 handler om authorization; OpenID Connect tilføjer authentication; JWT er et tokenformat.  
**Indhold:** Roller, flows, OIDC, JWT-opbygning, signering og sårbarheder.  
**Visual:** Authorization server i midten mellem client og resource server.

## Slide 2 - Hvad problem løser OAuth2?

**Pointe:** En client kan få begrænset adgang uden at kende brugerens password.  
**Indhold:** Delegated authorization, scopes, access tokens.  
**Visual:** "Give app access to photos" flow.

## Slide 3 - OAuth2 roller og elementer

**Pointe:** OAuth2 bliver forståeligt, når rollerne holdes adskilt.  
**Indhold:** Resource owner, client, authorization server, resource server, access token, refresh token, scope, redirect URI.  
**Visual:** Rolle-diagram.

## Slide 4 - Authorization Code Flow

**Pointe:** Authorization Code Flow er standardflowet for mange webapps.  
**Indhold:** Redirect til login, authorization code, token exchange, access token. Nævn PKCE.  
**Visual:** Sekvensdiagram med 5-6 trin.

## Slide 5 - Andre grant types

**Pointe:** Forskellige klienttyper kræver forskellige flows.  
**Indhold:** Client Credentials, Device Code, Refresh Token, legacy/frarådet Implicit og ROPC.  
**Visual:** Tabel: Flow -> Bruges til -> Risiko/noter.

## Slide 6 - OpenID Connect

**Pointe:** OIDC bygger oven på OAuth2 og standardiserer login/identitet.  
**Indhold:** ID token, userinfo endpoint, claims som `sub`, `email`, `name`, forskel på access token og ID token.  
**Visual:** OAuth2-lag med OIDC ovenpå.

## Slide 7 - JWT-opbygning

**Pointe:** JWT består af header, payload og signature.  
**Indhold:** `header.payload.signature`, claims, Base64URL, ikke krypteret som udgangspunkt.  
**Visual:** Token delt i tre farvede sektioner.

## Slide 8 - JWT signering og algoritmer

**Pointe:** Signaturen beskytter integritet, men algoritmevalget betyder meget.  
**Indhold:** HS256 delt secret, RS256/ES256 public-private key, fordele/ulemper.  
**Visual:** HMAC vs RSA/ECDSA sammenligning.

## Slide 9 - Kendte JWT-sårbarheder

**Pointe:** JWT-fejl skyldes ofte dårlig validering eller key management.  
**Indhold:** `alg=none`, algorithm confusion, svage secrets, manglende `aud`/`iss`/`exp`, for lang levetid, usikker browser storage.  
**Visual:** Angrebs-checkliste.

## Slide 10 - Øvelser og best practices

**Pointe:** Korrekt tokenbrug kræver validering, kort levetid og sikre flows.  
**Indhold:** JWT-kodegennemgang fra WEB #1, OAuth2/OIDC spørgsmål, anbefalinger: PKCE, TLS, claim validation, key rotation.  
**Visual:** "Do / Don't" tabel.

