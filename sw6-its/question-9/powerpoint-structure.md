# PowerPoint-struktur - Spørgsmål 9: Secure Boot

## Slide 1 - Titel og disposition

**Titel:** Secure Boot og Chain of Trust  
**Pointe:** Secure Boot forsøger at sikre, at kun betroet og signeret kode får lov at starte systemet.  
**Indhold:** Formål, chain of trust, kryptografi, implementeringsudfordringer, iPhone og øvelser.  
**Visual:** Bootkæde fra hardware til OS.

## Slide 2 - Hvorfor Secure Boot?

**Pointe:** Angreb før OS-start kan omgå mange normale sikkerhedsmekanismer.  
**Indhold:** Bootkits, evil maid, kompromitteret firmware/bootloader, fysisk adgang.  
**Visual:** Angriber manipulerer bootloader før OS.

## Slide 3 - Chain of Trust

**Pointe:** Tillid bygges trin for trin fra en hardware root of trust.  
**Indhold:** Boot ROM/firmware verifierer næste komponent; hvert led verifierer det næste.  
**Visual:** Hardware root -> firmware -> bootloader -> kernel -> OS.

## Slide 4 - Kryptografi i Secure Boot

**Pointe:** Hashes og digitale signaturer bruges til integritet og autenticitet.  
**Indhold:** Hash af kode, signatur med private key, verificering med public key, certifikater/keys i hardware/firmware.  
**Visual:** Code image + signature -> verify -> boot/stop.

## Slide 5 - Hvad sker der ved fejl?

**Pointe:** Hvis et led ikke kan verificeres, skal systemet stoppe eller gå i recovery.  
**Indhold:** Tamper detection, rollback prevention, recovery path, update policy.  
**Visual:** Decision diamond: valid signature? yes/no.

## Slide 6 - Implementeringsudfordringer

**Pointe:** Secure Boot er svært, fordi keys, updates og recovery også skal være sikre.  
**Indhold:** Key management, revocation, firmware updates, rollback attacks, debugging interfaces, supply chain.  
**Visual:** Risiko-matrix for implementeringsfejl.

## Slide 7 - iPhone som eksempel

**Pointe:** iPhone bruger en stærk boot chain med Apple-kontrollerede signaturer.  
**Indhold:** Boot ROM som immutable root, LLB/iBoot/kernel, signeret boot chain, jailbreak forsøger at bryde et led.  
**Visual:** iPhone boot sequence.

## Slide 8 - Chain of Trust bredere i IT-sikkerhed

**Pointe:** Samme princip findes i TLS, certifikater, software updates og blockchain-lignende kæder.  
**Indhold:** Trust anchors, signaturkæder, firmware signing, package signing.  
**Visual:** Sammenlignende tabel.

## Slide 9 - Øvelser fra undervisningen

**Pointe:** Crypto chip-øvelsen viser Secure Boot-princippet i miniature.  
**Indhold:** Sign og verify kode med crypto chip; Rubber Ducky defense som fysisk adgangsperspektiv; Evil Maid som case.  
**Visual:** Øvelse -> Secure Boot-begreb.

## Slide 10 - Afrunding

**Pointe:** Secure Boot reducerer risikoen for tidlig kompromittering, men er ikke en komplet sikkerhedsløsning.  
**Indhold:** Beskytter bootkæden, men ikke nødvendigvis runtime, brugerfejl eller kompromitterede keys.  
**Visual:** "Styrker / begrænsninger" split-slide.

