# Module 1 - Modern Cryptography

## Expected Results
- Correct symmetric key (hex): `54684020247570407220244063724074` (`Th@ $up@r $@cr@t`)
- Decrypted plaintext: `Hello Blockchain!`
- Asymmetric public key: see PEM block under **Key Pair Generation**
- Digital signature (Base64): `MEUCIQDeJBB0ZJDGS2WmBrPNUAwC/bncD5xB8GvPrluDNY//igIgcoKn8o8jcICfx2EYEgppuBgWTs15+RL/nIswedmzkAA=`

## Tools
- [CyberChef](https://gchq.github.io/CyberChef/) for encoding / decoding, hashing, and AES decryption.
- [EMN178 Online ECDSA Utilities](https://emn178.github.io/online-tools/) for elliptic-curve key generation, signing, and verification on curve secp256k1.

## 1. Hash Analysis of Candidate Keys
Three candidate keys were examined. Each hex-encoded value was converted to ASCII, and the SHA-256 digest was computed. CyberChef workflows are linked for reproducibility.

| Hex Encoded Key | ASCII Key | SHA-256 Digest | CyberChef Workflow |
| --- | --- | --- | --- |
| `68544020247570407220244063724074` | `hT@ $up@r $@cr@t` | `8f7c7aa61c742c533c1911f3bf15a62641f01e8fcaceef252bf26a5f7a53b046` | [Full CyberChef Workflow](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')SHA2('256',64,160)&input=Njg1NDQwMjAyNDc1NzA0MDcyMjAyNDQwNjM3MjQwNzQ&oeol=FF) |
| `54684020247570407220244063724074` | `Th@ $up@r $@cr@t` | `f28fe539655fd6f7275a09b7c3508a3f81573fc42827ce34ddf1ec8d5c2421c3` | [Full CyberChef Workflow](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')SHA2('256',64,160)&input=NTQ2ODQwMjAyNDc1NzA0MDcyMjAyNDQwNjM3MjQwNzQ&oeol=FF) |
| `54684020247570407220244063727440` | `Th@ $up@r $@crt@` | `c667de9c047a7481799b16d5c3f3547064f6cb7ac40b2145a02582b1c734c717` | [Full CyberChef Workflow](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')SHA2('256',64,160)&input=NTQ2ODQwMjAyNDc1NzA0MDcyMjAyNDQwNjM3Mjc0NDA&oeol=FF) |

The second candidate matches the provided SHA-256 hash (`f28fe5...`), so it is the correct symmetric key used for decryption.

## 2. AES-CBC Decryption of the Message
CyberChef was used to decrypt the provided ciphertext with AES-128 in CBC mode.

- AES encrypted message (hex): `876b4e970c3516f333bcf5f16d546a87aaeea5588ead29d213557efc1903997e`
- Initialization vector (hex): `656e6372797074696f6e496e74566563`
- Key (hex): `54684020247570407220244063724074`
- Workflow link: [AES decrypt -> From Hex](https://gchq.github.io/CyberChef/#recipe=AES_Decrypt(%7B'option':'Hex','string':'54684020247570407220244063724074'%7D,%7B'option':'Hex','string':'656e6372797074696f6e496e74566563'%7D,'CBC','Hex','Hex',%7B'option':'Hex','string':''%7D,%7B'option':'Hex','string':''%7D)From_Hex('None')&input=ODc2YjRlOTcwYzM1MTZmMzMzYmNmNWYxNmQ1NDZhODdhYWVlYTU1ODhlYWQyOWQyMTM1NTdlZmMxOTAzOTk3ZQ&oeol=FF)

**Decrypted plaintext:** `Hello Blockchain!`

## Step-by-Step (Tasks 1 & 2)
1. Loaded each of the three candidate keys into CyberChef, converted from Hex to Bytes, and calculated SHA-256 to compare against the provided digest `f28fe539655fd6f7275a09b7c3508a3f81573fc42827ce34ddf1ec8d5c2421c3`. Only `54684020247570407220244063724074` produced the matching hash, confirming it as the transmitted 128-bit key.
2. Used the confirmed key together with the supplied IV in CyberChef's AES-CBC decrypt workflow, fed in the ciphertext, and converted the output from Hex to UTF-8, revealing the plaintext `Hello Blockchain!`.

![Hello Blockchain!](images/image_1.png)

## 3. ECDSA Key Pair, Signature, and Verification

### Key Pair Generation
Using the EMN178 key generator with curve `secp256k1`, an asymmetric key pair was produced in PEM format:

```pem
-----BEGIN EC PRIVATE KEY-----
MHQCAQEEIN7u0QCOxeA/zDe/pHrV2JloDBcYIFCkPf8RRvqvAbrFoAcGBSuBBAAK
oUQDQgAEl7lLzXSrIwBgVGPE/35P4aU31gzSBFEavD6bFoqQZIBbHqcp9m7tdrSB
ZGacU2zDjwuJrTuihbrMw11hqk0EGA==
-----END EC PRIVATE KEY-----
```

```pem
-----BEGIN PUBLIC KEY-----
MFYwEAYHKoZIzj0CAQYFK4EEAAoDQgAEl7lLzXSrIwBgVGPE/35P4aU31gzSBFEa
vD6bFoqQZIBbHqcp9m7tdrSBZGacU2zDjwuJrTuihbrMw11hqk0EGA==
-----END PUBLIC KEY-----
```

### Signing the Plaintext
The plaintext message `Hello Blockchain!` was signed with SHA-256 as the hash function.  
Resulting signature (Base64):  
`MEUCIQDeJBB0ZJDGS2WmBrPNUAwC/bncD5xB8GvPrluDNY//igIgcoKn8o8jcICfx2EYEgppuBgWTs15+RL/nIswedmzkAA=`

Signing tool link: [EMN178 Sign Tool](https://emn178.github.io/online-tools/ecdsa/sign/?input=Hello%20Blockchain!&input_type=utf-8&output_type=base64&curve=secp256k1&algorithm=SHA256&private_key_input_type=pem_text&private_key=-----BEGIN%20EC%20PRIVATE%20KEY-----%0AMHQCAQEEIN7u0QCOxeA%2FzDe%2FpHrV2JloDBcYIFCkPf8RRvqvAbrFoAcGBSuBBAAK%0AoUQDQgAEl7lLzXSrIwBgVGPE%2F35P4aU31gzSBFEavD6bFoqQZIBbHqcp9m7tdrSB%0AZGacU2zDjwuJrTuihbrMw11hqk0EGA%3D%3D%0A-----END%20EC%20PRIVATE%20KEY-----)

### Signature Verification
The signature was verified with the corresponding public key and the same curve.

- Verification link: [EMN178 Verify](https://emn178.github.io/online-tools/ecdsa/verify/?input=Hello%20Blockchain!&input_type=utf-8&curve=secp256k1&algorithm=SHA256&public_key_input_type=pem_text&public_key=-----BEGIN%20PUBLIC%20KEY-----%0AMFYwEAYHKoZIzj0CAQYFK4EEAAoDQgAEl7lLzXSrIwBgVGPE%2F35P4aU31gzSBFEa%0AvD6bFoqQZIBbHqcp9m7tdrSBZGacU2zDjwuJrTuihbrMw11hqk0EGA%3D%3D%0A-----END%20PUBLIC%20KEY-----&signature_input_type=base64&signature=MEUCIQDeJBB0ZJDGS2WmBrPNUAwC%2FbncD5xB8GvPrluDNY%2F%2FigIgcoKn8o8jcICfx2EYEgppuBgWTs15%2BRL%2FnIswedmzkAA%3D)
- Result: Verification succeeded, confirming the signature's authenticity.

![Verification succeeded](images/iamge_2.png)








