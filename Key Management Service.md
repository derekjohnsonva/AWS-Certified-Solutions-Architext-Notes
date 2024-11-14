---
aliases:
  - KMS
---

used by lots of other services
**Regional**
**Public** zone service

used to manage cryptographic keys
Capable of using symmetric and asymmetric keys ([[Symmetric Vs Asymmetric encryption]])

Keys never leave KMS
	Compliant with **FIPS 140-2 level 2** (a security standard)

KMS keys are logical and backed by physical key material
Keys can be generated or imported
**Can only encrypt/decrypt 4kb of data**
To get around this we use...
## Data Encryption Keys
work on more than 4kb of data
**DEK encryption**
* User asks for a DEK and gives a standard KMS key
* KMS gives it to the user in a plaintext and a ciphertext version
* The user then uses the plaintext key to encrypt their own data
* The user should discard their plaintext key
* The user stores the encrypted key with their newly encrypted data
**DEK Decryption**
* Pass the encrypted DEK back to KMS with the KMS key user used to generate it
* KMS gives user a decrypted version of the DEK
* Use the decrypted key to decrypt your data
The difference between DEK and normal KMS keys is that in DEK, the work (encryption/decryption of data) is done by the user or the service using KMS.

## Key concepts
kms keys are isolated to a region
	keys can be replicated to other regions however
Either AWS Owned or customer owned 
	Sometimes aws will create the the keys for you
	Both types, keys will rotate once every year

## Permissions
Key policies - a type of [[Resource Policies]]
	every key has one
```json
{
"Sid": "Enable IAM User Permissions",
"Effect": "Allow",
"Principal": {"AWS": "arn:aws:iam :: 111122223333:root"},
"Action": "kms :* ",
"Resource": "*"!
}
```
In high security situations it may be best to only use Key policies instead of IAM policies
