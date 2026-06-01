# PowerPoint-struktur - Spørgsmål 3: Symmetrisk/asymmetrisk kryptering og digitale signaturer

## Slide 1 - Titel og disposition

**Titel:** Kryptering og digitale signaturer  
**Pointe:** Kryptering beskytter fortrolighed; signaturer beskytter integritet og autenticitet.  
**Indhold:** Symmetrisk krypto, asymmetrisk krypto, hashing, digitale signaturer, tillid i praksis og øvelser.  
**Visual:** Tre blokke: Encrypt, Hash, Sign.

## Slide 2 - Symmetrisk kryptering

**Pointe:** Samme nøgle bruges til kryptering og dekryptering.  
**Indhold:** AES som eksempel, hurtig behandling af store datamængder, key distribution som problem.  
**Visual:** Plaintext -> AES + shared key -> ciphertext.

## Slide 3 - Asymmetrisk kryptering

**Pointe:** Public/private key løser dele af nøglefordelingsproblemet.  
**Indhold:** Public key, private key, RSA/ECC, langsommere men nyttig til key exchange og signering.  
**Visual:** Public/private key pair.

## Slide 4 - Hybridkryptografi

**Pointe:** I praksis kombineres asymmetrisk og symmetrisk kryptografi.  
**Indhold:** TLS: asymmetrisk etablering af session key, derefter symmetrisk kryptering af data.  
**Visual:** Handshake øverst, krypteret datastrøm nederst.

## Slide 5 - Hashing

**Pointe:** Hashing skaber et fingerprint af data.  
**Indhold:** SHA256, deterministisk, envejs, collision resistance, ikke det samme som kryptering.  
**Visual:** Dokument -> hash digest.

## Slide 6 - Digital signatur: mekanismen

**Pointe:** Man signerer typisk en hash, ikke hele beskeden direkte.  
**Indhold:** Hash message -> signer med private key -> verificer med public key.  
**Visual:** To-delt diagram: signering hos afsender og verificering hos modtager.

## Slide 7 - Hvad opnår signaturer?

**Pointe:** Digitale signaturer giver integritet, autenticitet og non-repudiation.  
**Indhold:** Hvad signaturen beviser, og hvad den ikke beviser. Public key skal stadig være trusted.  
**Visual:** Tre checkmarks: integrity, authenticity, accountability.

## Slide 8 - Tillid i praksis

**Pointe:** Signaturen er kun så troværdig som key management og trust model.  
**Indhold:** PKI/certifikater, trusted roots, private key secrecy, algoritmevalg og revocation.  
**Visual:** Signatur + certifikatkæde.

## Slide 9 - Øvelser fra undervisningen

**Pointe:** Øvelserne viser signering både i software og som systemprincip.  
**Indhold:** Crypto++ ECDSA sign/verify, SHA256, RSA-besked, crypto chip/firmware signing, blockchain signed linked list.  
**Visual:** Mini-matrix: Øvelse -> Begreb -> Hvad demonstrerer den?

## Slide 10 - Afrunding

**Pointe:** Kryptering og signering løser forskellige sikkerhedsmål og bruges ofte sammen.  
**Indhold:** Sammenfat forskel på confidentiality, integrity og authenticity.  
**Visual:** CIA-kobling til kryptering/signering.

