# Talking points - Spørgsmål 9: Secure Boot

## Slide 1 - Titel og disposition

- Start med hovedpointe: Secure Boot skal sikre, at systemet kun starter kode, der er verificeret og betroet.
- Forklar at det handler om integritet tidligt i bootprocessen, før operativsystemets normale sikkerhedsmekanismer er aktive.
- Disposition: formål, chain of trust, kryptografi, fejl/recovery, udfordringer, iPhone-eksempel, bredere perspektiv og øvelser.

## Slide 2 - Hvorfor Secure Boot?

- Forklar problemet:
  - Hvis en angriber kan ændre bootloader eller firmware, kan angriberen få kontrol før OS'et starter.
  - Så kan malware gemme sig for antivirus, logging og OS-beskyttelse.
- Bootkits:
  - Malware i bootprocessen, der starter før OS.
- Evil maid:
  - Angriber får fysisk adgang til en maskine, fx hotelværelse, og ændrer bootloader eller installerer keylogger.
- Fysisk adgang:
  - Angriberen kan ændre storage, tilslutte USB, påvirke hardware eller forsøge at boote fra eksternt medie.
- Pointe: Disk encryption alene kan være utilstrækkeligt, hvis bootkæden kan manipuleres til at stjæle nøglen.

## Slide 3 - Chain of Trust

- Forklar chain of trust:
  - Tillid starter i et lille, svært manipulerbart komponent: hardware root of trust eller Boot ROM.
  - Første komponent verificerer næste komponent.
  - Næste komponent verificerer den næste osv.
- Eksempel:
  - Hardware/Boot ROM verificerer firmware.
  - Firmware verificerer bootloader.
  - Bootloader verificerer kernel.
  - Kernel starter resten af systemet.
- Hvis ét led kompromitteres, kan resten af kæden ikke nødvendigvis stoles på.
- Derfor skal det første led være meget lille, simpelt og beskyttet.
- Pointe: Man stoler ikke blindt på hele systemet; man bygger tillid trinvis.

## Slide 4 - Kryptografi i Secure Boot

- Hashing:
  - Bruges til at beregne fingerprint af kode/firmware.
  - Hvis koden ændres, ændres hashen.
- Digitale signaturer:
  - Producenten signerer bootkomponenter med private key.
  - Enheden verificerer med public key, der er indlejret eller lagret sikkert.
- Public key/certifikater:
  - Enheden behøver ikke kende private key.
  - Den skal kun kunne verificere signaturen.
- Private signing keys:
  - Skal beskyttes ekstremt godt.
  - Hvis de lækkes, kan angribere signere ondsindet firmware.
- Pointe: Secure Boot beskytter integritet og autenticitet, ikke nødvendigvis fortrolighed.

## Slide 5 - Hvad sker der ved fejl?

- Forklar beslutningspunktet:
  - Hvis signaturen er gyldig, fortsætter boot.
  - Hvis signaturen er ugyldig, skal boot stoppes eller recovery aktiveres.
- Recovery:
  - Skal være sikker, ellers bliver recovery-vejen en bypass.
- Rollback prevention:
  - Angriber kan forsøge at installere en gammel, signeret men sårbar version.
  - Systemet skal kunne forhindre downgrade til kendt sårbar firmware.
- Updates:
  - Opdateringer skal selv være signerede og verificerede.
- Pointe: Det er ikke nok at verificere første installation; hele livscyklussen skal være sikker.

## Slide 6 - Implementeringsudfordringer

- Key management:
  - Hvem må signere firmware?
  - Hvordan roteres keys?
  - Hvordan tilbagekaldes kompromitterede keys?
- Supply chain:
  - Firmware og hardware kan kompromitteres før levering.
- Debug interfaces:
  - JTAG, recovery mode eller service interfaces kan give bypass, hvis de ikke sikres.
- Fysisk adgang:
  - Angriber kan prøve fault injection, chip-off, boot fra eksternt medie eller manipulere storage.
- Usability/recovery:
  - Hvis Secure Boot fejler forkert, kan legitime brugere låses ude.
- Scope:
  - Secure Boot beskytter bootkæden, men ikke nødvendigvis runtime-angreb, phishing eller sårbare apps.
- Pointe: Secure Boot er stærkt, men kun som del af et større sikkerhedsdesign.

## Slide 7 - iPhone som eksempel

- Forklar iPhone som et godt eksempel, fordi Apple kontrollerer hardware, boot chain og software signing.
- Boot ROM:
  - Immutable kode i hardware.
  - Root of trust.
- Næste led:
  - Boot ROM verificerer næste bootloader-stage.
  - iBoot/kernel verificeres trin for trin.
- Apple-signaturer:
  - Kun software signeret af Apple kan normalt boote.
- Jailbreaking:
  - Forsøger at udnytte fejl i et led for at bryde kæden og køre uautoriseret kode.
- Pointe: iPhone viser både styrken ved en kontrolleret chain of trust og hvorfor fejl i tidlige boot-led er så alvorlige.

## Slide 8 - Chain of Trust bredere i IT-sikkerhed

- Sammenlign med TLS:
  - Browseren stoler på root CA.
  - Certifikatkæden verificeres ned til servercertifikatet.
- Sammenlign med software updates:
  - Update packages signeres.
  - Client verificerer signatur før installation.
- Sammenlign med package signing:
  - Dependencies/artifacts kan verificeres.
- Sammenlign med blockchain:
  - Også kæde af hashes, men tilliden kommer fra distribueret konsensus og proof-of-work/stake, ikke en central root key.
- Pointe: Chain of trust er et generelt princip: start fra et trust anchor og verificer næste led.

## Slide 9 - Øvelser fra undervisningen

- Crypto chip-øvelsen:
  - Sign og verify et stykke kode.
  - Viser principperne bag firmware signing og Secure Boot i lille skala.
- Rubber Ducky:
  - Viser hvorfor fysisk adgang er farlig.
  - Et HID-device kan sende tastetryk hurtigt og udføre kommandoer.
  - Defense kan være låst computer, USB-restriktioner, detektion af keystroke speed.
- Evil Maid:
  - God case til at forklare hvorfor bootkæden skal beskyttes, især sammen med disk encryption.
- Knyt øvelserne til CIA:
  - Secure Boot beskytter især integrity.
  - Fysisk adgang kan true confidentiality, integrity og availability.

## Slide 10 - Afrunding

- Opsummer:
  - Secure Boot sikrer, at kun verificeret kode starter.
  - Det bygger på chain of trust fra hardware root.
  - Kryptografien er primært hash og digitale signaturer.
  - Implementering er vanskelig på grund af keys, updates, rollback, recovery og fysisk adgang.
- Nævn begrænsning:
  - Når OS'et kører, skal runtime security stadig håndtere sårbarheder, malware, brugere og netværksangreb.
- Afslut med en stærk sætning: "Secure Boot er ikke hele sikkerheden, men det er fundamentet for at kunne stole på resten af systemet."

