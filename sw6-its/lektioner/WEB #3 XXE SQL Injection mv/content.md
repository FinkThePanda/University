# Indhold

- XML External Entity (XXE) attack
- (Blind) SQL/XPath Injection
- Generelle sikkerheds anbefalinger
- Clickjacking
- DNS Rebinding
- Web Application Firewalls

# Øvelser til Webapplicationer 3

1. Find XML External Entity (XXE) sårbarhed i Juice-shoppen og prøv at hent en fil fra serveren.
2. Find SQL Injection sårbarheder på Juice-shoppen.
3. Undersøg om Juice Shoppen er sårbar overfor Clickjacking. Prøv gerne også med en anden offentlig hjemmeside efter eget valg (det er ikke et angreb).
4. Udvælg et par offentligt tilgængelige hjemmesider og undersøg om de er sårbare overfor DNS Rebinding (det er ikke et angreb)
   - a) Test ved at finde webserverens ip-adresse og derefter tilføjet en entry i din egen computers hosts-fil med denne ip-adresse men med et andet hostnavn.
   - b) Hvis du nu fra din browser kan tilgå sitet med det selvvalgte hosthavn, så er sitet sårbar for DNS rebinding.
