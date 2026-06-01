# Læringsmål

- Beskrive de vigtigste sikkerhedsrisici inden for sikre it-systemer
- Anvende kodebiblioteker og værktøjer til at sikre fortrolighed, integritet og tilgængelighed af data
- Analysere konkrete brugsscenarier og identificere de vigtigste sikkerhedsrisici

## Indhold

- Introduktion (HTTP/S, DOM, Browser Politikker, Autentificering, Cookies, Local Storage og Sessioner)
- Authentication
- Authorization
- JWT
- OAuth2

# Øvelse

- a) Denne kode til at hashe et password kommer fra et bachelorprojekt. Kan du finde nogen fejl?

```c
    public string HashPassword(string password)

    {

        byte[] salt = new byte[16];

        using (var rng = RandomNumberGenerator.Create())

        {

            rng.GetBytes(salt);

        }

        string saltString = Convert.ToBase64String(salt);

        byte[] saltedPassword = Encoding.UTF8.GetBytes(password + saltString);

        byte[] hash = SHA256.HashData(saltedPassword);

        string hashString = Convert.ToBase64String(hash);

Er

        return $"{hashString}${saltString}";

    }
```

- b) What algorithms are recommended for hashing of passwords?

- c) Er anbefalingerne fulgt her?

```c
const iterations = 90000;

const keylen = 32;

const saltBytes= 16;

const digest = 'sha512';


userSchema.methods.setPassword = function (password) {

  this.salt = crypto.randomBytes(saltBytes).toString('hex');

  this.hash = crypto.pbkdf2Sync(password, this.salt, iterations, keylen,

              digest).toString('hex');

};
```

- d) Kan du finde nogen fejl?

```c
private string GenerateToken(string username)

{

    var claims = new Claim[]

    {

        new Claim(ClaimTypes.Name, username),

        new Claim(JwtRegisteredClaimNames.Nbf, new

                  DateTimeOffset(DateTime.Now).ToUnixTimeSeconds().ToString()),

        new Claim(JwtRegisteredClaimNames.Exp, new

                  DateTimeOffset(DateTime.Now.AddDays(1)).ToUnixTimeSeconds().ToString()),

    };

    var token = new JwtSecurityToken(

         new JwtHeader(new SigningCredentials(

              new SymmetricSecurityKey(Encoding.UTF8.GetBytes("the secret that needs to be at least 16 characeters long")), SecurityAlgorithms.Sha256)),

              new JwtPayload(claims));

    return new JwtSecurityTokenHandler().WriteToken(token);

}
```

e)
What is OAuth2?

f)
What are the basic elements in OAuth2?

g)
Why are there different grant types (flows) in OAuth2?

h)
What is OpenIDConnect?
