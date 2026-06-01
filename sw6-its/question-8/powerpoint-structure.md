# PowerPoint-struktur - Spørgsmål 8: Buffer overflow og code injection

## Slide 1 - Titel og disposition

**Titel:** Buffer overflow, code injection og ROP  
**Pointe:** Usikker memory-håndtering kan give angriberen kontrol over programflowet.  
**Indhold:** Stack, overflow, shellcode, mitigations, ROP, fuzzing og øvelser.  
**Visual:** Stack som lodret hukommelsesdiagram.

## Slide 2 - Stackens opbygning

**Pointe:** For at forstå overflow skal man kunne tegne stack frame.  
**Indhold:** Local buffer, saved frame pointer, return address, arguments.  
**Visual:** Stack frame med labels og pile.

## Slide 3 - Buffer overflow

**Pointe:** Overflow opstår, når input overskrider bufferens grænse.  
**Indhold:** Manglende bounds checking, overwrite af return address, crash eller kontrol-flow hijack.  
**Visual:** Før/efter stack hvor input flyder over buffer.

## Slide 4 - Code injection og shellcode

**Pointe:** Angriberen kan placere kode i hukommelsen og hoppe til den.  
**Indhold:** Shellcode, calc-eksempel fra undervisningen, return address peger på shellcode.  
**Visual:** Buffer med NOP sled/shellcode og return address.

## Slide 5 - Stack canaries / GS cookies

**Pointe:** Canaries opdager mange simple stack overflows før return address bruges.  
**Indhold:** Canary placeres mellem buffer og control data; check før return; begrænsninger.  
**Visual:** Stack med canary-marker.

## Slide 6 - NX/DEP

**Pointe:** Non-executable stack forhindrer direkte eksekvering af injected code.  
**Indhold:** Memory pages som executable/non-executable; shellcode på stack fejler.  
**Visual:** Stack markeret "no execute".

## Slide 7 - ROP

**Pointe:** ROP omgår NX ved at genbruge eksisterende kode i programmet/biblioteker.  
**Indhold:** Gadgets, return chains, system calls/API calls, ASLR som ekstra mitigation.  
**Visual:** Kæde af gadgets: gadget 1 -> gadget 2 -> gadget 3.

## Slide 8 - Fuzzing

**Pointe:** Fuzzing finder memory bugs ved automatisk at teste mange inputs.  
**Indhold:** Generation/mutation, crash detection, corpus, coverage-guided fuzzing, relevance for parsere og protokoller.  
**Visual:** Fuzzer -> program -> crash reports.

## Slide 9 - Anti-fuzzing

**Pointe:** Anti-fuzzing forsøger at gøre automatiseret test mindre effektivt.  
**Indhold:** Delays, checksums, magic values, path explosion, input constraints. Perspektiver til defense-in-depth og teststrategi.  
**Visual:** Fuzzer der rammer "gate checks".

## Slide 10 - Øvelser og afrunding

**Pointe:** Debugger-øvelserne viser hvordan teorien bliver konkret i memory.  
**Indhold:** ImmunityDebugger, mona.py, R4ndoms_OllyDBG, dll.zip, tutorial fra KODE #2.  
**Visual:** Øvelsesflow: crash -> find offset -> control EIP/RIP -> payload -> mitigation.

