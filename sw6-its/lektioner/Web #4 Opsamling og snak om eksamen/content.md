# Indhold

- Audit værktøjer og strategier
- Kode review/statisk kode analyse
- Automatiserede scannere
- Evaluering
- Snak om eksamen

# Øvelse 1

1. Download og installer OWASP ZAP scanneren her: https://www.zaproxy.org/download/
2. Start en scanning af jeres Juice-shop.
3. Start en scanning af http://testhtml5.vulnweb.com
4. Start en scanning af http://testphp.vulnweb.com
5. Start evt. en scanning af jeres egen Angular applikation, hvis I har én.
6. Gå til https://sitecheck.sucuri.net og start en scanning af 3), 4) og 5)
7. Sammenlign resultaterne.

# Øvelse 2

1. Installér Charles Proxy https://www.charlesproxy.com/.
   Opsæt Charles Proxy til at optage al trafik — også SSL/TLS vha et selvsigneret certifikat.
2. Udvælg en offentlig tilgængelig side der benytter SSL/TLS og inspicer trafikken, som en Web Application Firewall vil kunne gøre. Se hvad der sker hvis du tilføjer et # til URL'en.
