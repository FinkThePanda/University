- SSL/TLS
- Certifikater
- Public Key Infrastructure

# Øvelse

Målet er at I bliver bekendt med OpenSSL, Windows MMC'en, certifikat-håndtering i Windows samt binding af certifikater.

Udsted et certifikat i OpenSSL:

1. Download OpenSSL: https://wiki.openssl.org/index.php/Binaries -> https://slproweb.com/products/Win32OpenSSL.html

2. Installer OpenSSL.

3. Kør i en CMD: openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -sha256 -subj "/C=DK/CN=DIT_COMMON_NAME" -addext "subjectAltName = DNS:DIT_COMMON_NAME"

4. Kør i en CMD: openssl pkcs12 -export -out certificate.pfx -inkey key.pem -in cert.pem (DIT_COMMON_NAME kan fx være swtits.google.com)

Installer certifikatet:

1. Kør VS som admin. Lav en ASP.NET Core Web Application. Slå SSL til i web-projektet i Visual Studio (project properties->Debug).

Se at det fungerer i browseren - dog med en fejl.

2. Importer det udstedte certifikat (certificate.pfx) i "mmc" snap-in'et "Local Machine/Certificates " i "Personal" og "Trusted Root Certification Authorities".

3. Bind det til porten med "netsh" i Windows (start en CMD som admin):

netsh http show sslcert ipport=IP:PORT (fx. 0.0.0.0:44345) (notér appid) (Brug PORT fra VS under Enable SSL)

netsh http delete sslcert ipport=IP:PORT

netsh http add sslcert ipport=IP:PORT certhash=CERT_THUMBPRINT_UDEN_MELLEMRUM appid={appid} (hent Thumbprint i mmc i Details under certifikatet)

4. Tilføj 127.0.0.1 DIT_COMMON_NAME til hosts filen (Windows/System32/drivers/etc/hosts).

5. Ænder applicationhost.config (find "binding protocol='https'" og erstat localhost med DIT_COMMON_NAME. (applicationhost.config ligger typisk under ..\Projects\WebApplication2\.vs\config)

6. Åbn https://DIT_COMMON_NAME:PORT i browseren - nu uden certifikatfejl.

7. Inspicer certifikatet i browseren.
