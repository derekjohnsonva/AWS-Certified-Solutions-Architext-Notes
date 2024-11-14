HSM = Hardware Security Model

An alternative to [[Key Management Service|KMS]]

Used when you need to achieve compliance with certain security standards such as [FIPS 140-2 Level 3](https://en.wikipedia.org/wiki/FIPS_140-2)

AWS provisions the keys but they don't have any way to access them

Uses Industry Standard APIs
* **PKCS#11, Java Cryptography Extensions, Microsoft CryptoNG**

KMS can use CloudHSM as a custom key store

![[Pasted image 20241003161045.png]]

Use Cases
* Does not have native integrations with AWS services. You have to do client side encryption
* Offloads SSL/TLS Processing
* Enable transparent data encryption for oracle databases
* protect the private keys for an issuing certificate authority
