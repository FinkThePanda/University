# Talking points - Spørgsmål 8: Buffer overflow og code injection

## Slide 1 - Titel og disposition

- Start med at sige, at dette spørgsmål handler om lavniveau-sårbarheder, især i sprog som C/C++, hvor programmet selv håndterer memory.
- Hovedpointe: Hvis et program skriver uden for en buffer, kan angriberen i nogle tilfælde ændre programflowet og få sin egen kode eller eksisterende kode kørt.
- Disposition: stack, overflow, code injection, mitigations, ROP, fuzzing, anti-fuzzing og øvelser.

## Slide 2 - Stackens opbygning

- Tegn eller forklar en stack frame:
  - Lokale variabler, fx en char buffer.
  - Saved frame pointer/base pointer.
  - Return address.
  - Function arguments afhængigt af calling convention.
- Forklar return address:
  - Når en funktion er færdig, bruger CPU'en return address til at vide, hvor den skal fortsætte.
- Forklar hvorfor return address er interessant:
  - Hvis angriberen kan overskrive den, kan programmet hoppe til en adresse valgt af angriberen.
- Nævn at stacken typisk vokser i en bestemt retning, og lokale buffers kan ligge tæt på kontrolinformation.

## Slide 3 - Buffer overflow

- Forklar buffer overflow:
  - Programmet reserverer en buffer med fast størrelse.
  - Input er større end bufferen.
  - Programmet skriver videre ind i tilstødende memory.
- Brug eksempel: `char buf[64]`, men programmet kopierer 200 bytes uden bounds check.
- Konsekvenser:
  - Crash.
  - Overskrivning af variabler.
  - Overskrivning af return address.
  - Potentiel code execution.
- Forklar at ikke alle overflows giver udnyttelse, men de er farlige, fordi de kan korrumpere memory.

## Slide 4 - Code injection og shellcode

- Forklar code injection:
  - Angriberen placerer maskinkode i memory, fx i inputbufferen.
  - Angriberen ændrer return address til at pege på den kode.
- Shellcode:
  - Lille stykke kode, traditionelt for at åbne shell, men i øvelsen fx calculator.
- NOP sled:
  - En række ufarlige instruktioner før shellcode, så springadressen ikke behøver være helt præcis.
- Brug calc-shellcode fra undervisningen som eksempel på, at payloaden er rå bytes, ikke almindelig kildekode.
- Pointe: Sårbarheden er ikke kun crash; den kan blive kontrol over instruction pointer.

## Slide 5 - Stack canaries / GS cookies

- Forklar stack canary:
  - Compiler placerer en hemmelig eller tilfældig værdi mellem buffer og return address.
  - Før funktionen returnerer, kontrolleres om canary stadig er intakt.
  - Hvis den er ændret, stoppes programmet.
- GS cookies er Microsofts variant.
- Hvad beskytter de mod?
  - Simple stack overflows, der overskriver return address.
- Begrænsninger:
  - Hvis angriberen kan læse canary via info leak, kan den genskabes.
  - Ikke alle memory corruption bugs rammer canary.
  - Kan omgås med andre teknikker eller non-control-data attacks.
- Pointe: Canaries opdager mange angreb, men fjerner ikke sårbarheden.

## Slide 6 - NX/DEP

- Forklar NX/DEP:
  - Memory pages kan markeres som non-executable.
  - Stack og heap bør ikke kunne eksekvere kode.
- Hvad forhindrer det?
  - Klassisk code injection, hvor shellcode ligger på stacken.
- Forklar at programmet stadig kan have kontrol-flow-sårbarhed, men angriber kan ikke bare køre ny kode fra dataområdet.
- Begrænsninger:
  - Hvis angriberen kan kalde eksisterende kode, kan NX omgås.
  - Hvis memory permissions kan ændres, kan angriber prøve at gøre stack executable.
- Overgang: ROP opstod som en måde at udnytte eksisterende executable code på.

## Slide 7 - ROP

- Forklar Return-Oriented Programming:
  - Angriberen bruger små stykker eksisterende kode, kaldet gadgets.
  - Gadgets slutter typisk med `ret`.
  - Ved at styre stacken kan angriberen kæde gadgets sammen.
- Hvorfor omgår det NX?
  - Angriberen injicerer ikke ny kode.
  - Den genbruger kode, der allerede ligger i executable memory.
- Hvad kan ROP bruges til?
  - Kalde systemfunktioner.
  - Ændre memory permissions.
  - Bygge et angrebsprogram af eksisterende instruktioner.
- ASLR:
  - Randomiserer adresser og gør gadgets sværere at finde.
  - Info leaks kan dog afsløre adresser.
- Pointe: Mitigations hæver sværhedsgraden, men angrebsteknikker udvikler sig.

## Slide 8 - Fuzzing

- Forklar fuzzing:
  - Automatisk test hvor man genererer eller muterer input for at finde crashes og fejl.
- Hvorfor virker det?
  - Mange memory bugs ligger i edge cases, parserfejl eller uventede inputlængder.
- Typer:
  - Random fuzzing.
  - Mutation-based fuzzing.
  - Coverage-guided fuzzing, hvor værktøjet prøver at ramme nye programstier.
- Output:
  - Crashes.
  - Hangs.
  - Sanitizer findings.
  - Inputs der reproducerer fejlen.
- Relevans:
  - Særligt godt til parsere, filformater, netværksprotokoller og C/C++ kode.
- Pointe: Fuzzing finder ikke alle fejl, men er stærkt til at finde memory corruption automatisk.

## Slide 9 - Anti-fuzzing

- Forklar anti-fuzzing som teknikker, der gør fuzzing mindre effektivt.
- Eksempler:
  - Magic values/checksums, der stopper de fleste tilfældige inputs.
  - Delays/sleeps, der gør test langsom.
  - Path explosion, hvor fuzzer spilder tid.
  - Anti-debugging eller miljøchecks.
  - Inputformater der kræver kompleks struktur.
- Forsvarsperspektiv:
  - Anti-fuzzing kan diskuteres som defense-in-depth, men kan også gøre legitim sikkerhedstest sværere.
- Testperspektiv:
  - Man kan forbedre fuzzing med seed corpus, dictionaries, struktur-aware fuzzing og harnesses.
- Pointe: Fuzzing er stærkt, men kræver god opsætning for komplekse programmer.

## Slide 10 - Øvelser og afrunding

- Knyt til øvelser:
  - ImmunityDebugger: se registers, stack og crash.
  - mona.py: hjælpe med offset, gadgets og exploit-udvikling.
  - R4ndoms_OllyDBG/dll.zip: praktisk reversing/debugging.
- Forklar typisk exploit workflow:
  1. Find crash.
  2. Find offset til return address.
  3. Kontroller instruction pointer.
  4. Find plads til payload eller ROP chain.
  5. Håndter mitigations.
- Afrund:
  - Buffer overflow er en memory safety-fejl.
  - Code injection udnytter kontrol over memory og flow.
  - Canaries og NX/DEP beskytter mod klassiske angreb.
  - ROP viser hvordan eksisterende kode kan misbruges.
  - Fuzzing er en praktisk metode til at finde fejlene.

