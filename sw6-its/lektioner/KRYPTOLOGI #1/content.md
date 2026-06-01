- Symmetrisk og asymmetrisk kryptering
- Hashing
- Sikker opbevaring af data

# Øvelse

1. Vi implementerer simple krypterings- og hashing-eksempler i C# i Visual Studio: Fra System.Security.Cryptography afprøv Aes, SHA256 og RSACryptoServiceProvider classes.
2. Vi implementerer simple krypterings- og hashing-eksempler i open-source C++ i Visual Studio (fra Crypto++ library afprøv ECDSA og SHA256 HashFilter).

**Løsning SHA256**

using CryptoPP::SHA256;
using CryptoPP::ByteQueue;
using CryptoPP::StringSink;
using CryptoPP::StringSource;

string Hash(string stringin)
{
stringstream tohash;
string value;
SHA256 hash256;

    tohash << stringin;

    StringSource ss(tohash.str(), true /* PumpAll */,
    	new HashFilter(hash256,
    		new HexEncoder(
    			new StringSink(value)
    		) // HexEncoder
    	) // HashFilter
    ); // StringSource

    return value;

}

**Løsning ECDSA**

using std::exit;

using CryptoPP::AutoSeededRandomPool;

using CryptoPP::ECP;
using CryptoPP::ECDSA;

// Generate private key
ECDSA<ECP, SHA256>::PrivateKey privKey;
privKey.Initialize(prng, secp160r1());
privKey.Save(StringSink(privateKey));

// Create public key
ECDSA<ECP, SHA256>::PublicKey pubKey;
privKey.MakePublicKey(pubKey);
pubKey.Save(StringSink(publicKey));

string Sign(string message)
{
// Load private key (in ByteQueue, PKCS#8 format)
ECDSA<ECP, SHA1>::Signer signer(StringSource(privateKey,true));

    // Determine maximum size, allocate a string with that size
    size_t siglen = signer.MaxSignatureLength();
    string signature(siglen, 0x00);

    // Sign, and trim signature to actual size
    siglen = signer.SignMessage(prng, (const unsigned char*)message.data(), message.size(), (unsigned char*)signature.data());
    signature.resize(siglen);
    return signature;

}

bool Verify(string message, string signature, string publicKey)
{
ECDSA<ECP, SHA1>::Verifier verifier(StringSource(publicKey,true));

    bool result = verifier.VerifyMessage((const unsigned char*)message.data(), message.size(), (const unsigned char*)signature.data(), signature.size());

    if (result)
    {

    	return true;
    }
    else
    {


    	return false;
    }

}

## Optional:

1. Send og modtag en krypteret RSA besked til/fra 'sidemanden', hvor du benytter følgende nøglepar.
   Off. nøgle (e = 17, n = 86609)
   Priv. nøgle (d = 65777, n= 86609)

2. Kan I udlede den private nøgle ud fra e og n

3. Kan I udlede den private 128bit nøgle ud fra e = 65537 og n = 265887809417461548369618742468095418981

Løsningsforslag vedhæftet.
