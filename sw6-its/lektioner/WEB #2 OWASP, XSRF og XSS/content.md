# Indhold

- OWASP
- Cross-Site Request Forgery
- Cross-Site Scripting
- Content Security Policy
- Sikre HTTP Headere

# WEB 2 Øvelse 1

- Installer Docker versionen af Juice Shop ved at følge denne guide: https://pwning.owasp-juice.shop/companion-guide/latest/part1/running.html

- Hvis du ikke kender til Docker, så kan du også bruge en hosted udgave:
  https://juice-shop.herokuapp.com/#/

**Opgaven**

- Undersøg hvordan Juice Shopen kommunikerer med API'et samt opbevarer data i browseren. Hvilke teknikker har vi i spil, som vi har talt om?

- Find Cross-Site Request Forgery sårbarheder. Brug evt. http://htmledit.squarefree.com/ til at designe angrebet (tip: sæt form target="\_blank").

- Lav Cross-Site Request Forgery angrebskode (HTML/JavaScript), der ændrer værdier på vegne af en indlogget bruger på Juice Shop.

Hint:
Find evt. hjælp her: https://pwning.owasp-juice.shop/

# Web 2 Øvelse 2

1. Find Cross-Site Scripting sårbarheder i Juice-shoppen.

2. Lav angrebskode der opsnapper cookies på Juice-shoppen og sender dem videre til en extern side (benyt evt et random domain).

3. Lav et lokalt deface af Juice shoppen der fx spørger brugeren efter kreditkort eller credentials oplysninger og videresender dem til en extern side.

Find evt. hjælp her: https://pwning.owasp-juice.shop/
