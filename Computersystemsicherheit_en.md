# Computer Security

**Security** means both Safety and Security in English:

- Safety: protection against accidental errors  
- Security: protection against malicious actions  

There are 5 **security properties** (extended):

1. Confidentiality of data/messages  
2. Integrity of data/computations  
3. Availability of services  
   (CIA Triad)  
5. Authenticity of files  
6. Anonymity of users  

Cryptography provides 4 **goals**:

1. **Confidentiality**: An attacker cannot learn the content of messages  
2. **Integrity**: An attacker cannot modify a message without the modification being detected  
3. **Authenticity**: An attacker cannot claim that a message originated from someone who did not send it  
4. **Non-repudiation**: An attacker cannot later deny having sent a message  

There are 2 types of cryptography: symmetric (same key for encryption and decryption) and asymmetric (two keys for encryption and decryption).

---

## Symmetric Cryptosystems

A **symmetric cryptosystem** is a 5-tuple $(M,K,C,e,d)$ such that for all plaintexts $m \in \mathcal{M}$ and $k \in \mathcal{K}$ it holds that:

$$
d(e(m,k), k) = m.
$$

**Kerckhoffs’ Principle**:  
A cryptosystem must remain secure even if everything about it is publicly known — except the key.

---

There are also 2 types of ciphers:

### Classical ciphers  
(e.g., Shift cipher: Caesar cipher, Substitution cipher, Vigenère cipher, OTP)

### Modern ciphers  

Modern ciphers contain 3 important aspects:

- Formal definitions  
- Systematic design  
- Very secure cryptographic constructions with security proofs  
  (Security proofs rely on cryptographic assumptions; if an assumption is false, the scheme is no longer secure.)

The security of **classical ciphers** often relied on keeping the algorithm secret (*security by obscurity*) and used mechanical or manual methods.

The security of **modern ciphers** is based on mathematics and complexity theory and relies exclusively on the secrecy of the key.
---

## Cryptographic Primitives

|                     | **Symmetric Cryptographic Primitives** | **Asymmetric Cryptographic Primitives** |
|---------------------|----------------------------------------|------------------------------------------|
| **Confidentiality** | <ul><li>Symmetric ciphers</li><li>Block ciphers</li></ul> | <ul><li>Public Key Encryption (PKE)</li></ul> |
| **Integrity & Authenticity** | <ul><li>Message Authentication Codes (MAC)</li></ul> | <ul><li>Digital Signatures</li></ul> |

---

## Cryptographic Constructions (Examples)

|                     | **Symmetric Constructions** | **Asymmetric Constructions** |
|---------------------|----------------------------|------------------------------|
| **Confidentiality** | <ul><li>One-Time Pad</li><li>DES (3DES), AES</li></ul> | <ul><li>RSA Encryption</li><li>ElGamal Encryption</li></ul> |
| **Integrity & Authenticity** | <ul><li>CBC-MAC</li><li>HMAC</li></ul> | <ul><li>RSA Signatures</li><li>Schnorr Signatures</li></ul> |

---

## Symmetric Cryptography

Algorithms: (Gen, Enc, Dec)

<img width="586" height="109" alt="Bildschirmfoto 2025-10-07 um 14 17 00" src="https://github.com/user-attachments/assets/18b9a3d1-06f9-422a-8850-2fb72e37cf7d" />

---

### Security Games

1. **IND-COA (Indistinguishability under Ciphertext-Only Attack)**  
   The attacker only sees ciphertexts.  
   The game: the attacker must distinguish between two possible plaintexts.  
   The attacker’s success probability must be at most negligibly better than $\frac{1}{2}$.

2. **IND-KPA (Known Plaintext Attack)**  
   The attacker knows pairs $(m,c)$ and may derive statistics and patterns  
   (e.g., fixed formats, email signatures/footers).  
   The attacker must distinguish between two possible plaintexts.  
   The attacker’s success probability must be at most negligibly better than $\frac{1}{2}$.

3. **IND-CPA (Chosen Plaintext Attack)**  
   The attacker may request encryptions of arbitrarily chosen messages.  
   The attacker’s success probability must be at most negligibly better than $\frac{1}{2}$.

   - Danger: Chosen Ciphertext Attacks (e.g., Padding Oracle Attack)

4. **IND-CCA (Chosen Ciphertext Attack)**  
   The attacker has access to a decryption oracle for chosen ciphertexts.  
   The attacker’s success probability must be at most negligibly better than $\frac{1}{2}$.

---

### Perfect Security

Formally, perfect security holds if for all plaintexts $m$ and all ciphertexts $c$:

$$
P[m \mid c] = P[m].
$$

---

## One-Time Pad (OTP)

The OTP is also known as the Vernam cipher.

- OTP encrypts bit strings of length $n$.

**Formal definition:**

- Gen: output random key  
  $$
  k \overset{\mathrm{R}}{\gets} \{0,1\}^n
  $$

- Enc: for $m \in \mathcal{M}$  
  $$
  \mathrm{Enc}(k,m) = k \oplus m
  $$

- Dec: for $c \in \mathcal{C}$  
  $$
  \mathrm{Dec}(k,c) = k \oplus c
  $$

**Security requirements:**

- The key must only be used once.
- The key must be truly random.
- The key must be at least as long as the message.
- The key must remain absolutely secret and be securely exchanged.

---

## Block Ciphers

- Block ciphers are cryptosystems that can only encrypt fixed-length blocks.
- Encryption and decryption operate on message/ciphertext blocks of fixed size.
- Block length $n = |m| = |c|$: typically 64–128 bits.
- Key length $k$: typically 128–256 bits.
- The same key can be reused for multiple different blocks.

Here, $\mathrm{Enc}(\cdot)$ plays the role of a pseudorandom permutation (PRP).  
The security of a block cipher depends on whether an attacker can distinguish $\mathrm{Enc}(\cdot)$ from a truly random permutation.

Examples of block ciphers: AES, DES, 3DES, Serpent, Twofish, Blowfish.

<img width="648" height="156" alt="Bildschirmfoto 2025-10-07 um 14 15 11" src="https://github.com/user-attachments/assets/f40499c1-899e-4104-9f1f-b229eb8fc96e" />

DES, 3DES, AES, Serpent, Twofish, Blowfish are concrete algorithms implementing a PRP on fixed block sizes.

---

### Data Encryption Standard (DES)

- Block length $n = 64$ bits  
- Key length $k = 56$ bits  
- Ciphertext length $c = 64$ bits  
- Main weakness: short key

---

### Triple DES (3DES)

- Key length: $3 \cdot 56 = 168$ bits

<img width="610" height="70" alt="Bildschirmfoto 2025-10-07 um 14 15 38" src="https://github.com/user-attachments/assets/c481110b-55c0-44cc-945a-62e95857bc89" />

- Vulnerable to Meet-in-the-Middle attack (effective security ≈ 112 bits).

---

### Advanced Encryption Standard (AES)

- Block size: 128 bits  
- Key length: 128, 192, or 256 bits  

AES can be attacked via side-channel attacks or implementation flaws.

**Problems of AES (in practice):**

- Secure only if implementation and surrounding systems are correctly configured.
- Weak key or IV generation can compromise security.
- Side-channel attacks can reveal the key.

Countermeasures:

- Constant-time implementations (against timing attacks)
- Masking techniques (against power analysis)
- AES-NI (hardware support in Intel/AMD CPUs for secure and fast AES)

---

### General Problems of Block Ciphers

- Not IND-CPA secure by themselves (deterministic).
- Cannot encrypt messages of arbitrary length directly.

---

## Modes of Operation

ECB, CBC, and CTR are **modes of operation** that use a block cipher to encrypt and decrypt long messages (multiple blocks).

---

### Electronic Code Book (ECB) Mode

<img width="370" height="273" alt="Bildschirmfoto 2025-10-06 um 21 33 11" src="https://github.com/user-attachments/assets/19370868-6fb7-4a9b-be48-7d88b2212405" />

- If $|m|$ is not a multiple of the block length, padding must be applied.
- Randomizing the input can help prevent certain attacks.

**Advantages:**

- Simple implementation (each block processed independently)
- Encryption and decryption are parallelizable
- Error tolerance: corruption in one block does not affect others

**Disadvantages:**

- Deterministic
- No diffusion: small changes in plaintext cause localized changes in ciphertext
- Identical plaintext blocks produce identical ciphertext blocks

---

### Cipher Block Chaining (CBC) Mode

<img width="545" height="252" alt="Bildschirmfoto 2025-10-06 um 21 41 01" src="https://github.com/user-attachments/assets/1a67ac63-42f3-4923-b7fd-f71abdd309e6" />

<img width="545" height="253" alt="Bildschirmfoto 2025-10-06 um 21 40 06" src="https://github.com/user-attachments/assets/3b4bfe0b-3291-47b5-b880-587670711b3b" />

To formalize CBC, we use **randomized cryptosystems**:

A randomized symmetric cryptosystem is a 6-tuple $(M,K,C,R,e,d)$ such that for all plaintexts $m \in \mathcal{M}$ and $k \in \mathcal{K}$:

$$
d(e(m,k,r), k, r) = m.
$$

For security:

- The value from $R$ must be chosen uniformly at random.
- It must be unpredictable.
- It must never be reused.

Encryption is not parallelizable.  
Decryption is parallelizable.  

A corrupted ciphertext block affects decryption of:
- the current block
- the immediately following block

CBC is **IND-CPA secure** if:

- The Initialization Vector (IV) is random and unpredictable.
- The IV is not reused.

However, CBC often suffers from padding-related problems in practice.

---

### Padding Attacks on CBC

Assumptions:

1. The attacker has ciphertext and access to a padding oracle.
2. The attacker does not know the plaintext or the key.
3. The server uses a verifiable padding scheme (e.g., PKCS#7).

Attack idea:

- The attacker manipulates ciphertext blocks.
- The server reveals (via error messages or side channels) whether padding is valid.
- From this information, the attacker can recover plaintext bytes.

---

### Counter (CTR) Mode

<img width="541" height="257" alt="Bildschirmfoto 2025-10-07 um 10 53 53" src="https://github.com/user-attachments/assets/ef318ba2-ac8b-4ea3-bd4a-108dff4852ab" />

<img width="539" height="247" alt="Bildschirmfoto 2025-10-07 um 10 55 29" src="https://github.com/user-attachments/assets/ff798999-8976-4fa0-8841-f81628158493" />

CTR uses a **randomized counter function** that maps:

- a random value (Nonce)
- and a natural number (Counter)

to a fixed-length bit string.

A simple implementation uses the binary representation of the natural number with zero-padding (LSB or MSB encoding).

**Important problem:**

- The counter must never repeat.
- Because the block size is fixed, the counter space is finite.
- Overflows and reuse must be prevented.

The total length of (Nonce || Counter) depends on the block size.

Encryption and decryption are parallelizable.

CTR is essentially an OTP construction using a block cipher as a pseudorandom generator.

---

### Nonce vs. IV

- A **Nonce** only needs to be unique.
- An **IV** emphasizes unpredictability.

Nonce → prevents reuse of keystreams.  
IV → prevents leakage under chosen plaintext attacks.

CTR only requires uniqueness (not unpredictability).

---

## Stream Ciphers

- Stream ciphers can encrypt bit strings of arbitrary length.
  - Plaintext and ciphertext are bit strings of arbitrary length.
  - Key length is fixed.
  - A pseudorandom keystream is generated from the key.
  - Encryption and decryption are bitwise XOR with the keystream.

A cryptosystem is called a stream cipher if there exists a function (keystream generator)

$$
\mathrm{keystream}(x,z)
$$

that outputs a keystream of length $|x|$, such that:

$$
e(x,z) = d(x,z) = x \oplus \mathrm{keystream}(x,z).
$$

---

### ChaCha20

ChaCha20 is a modern stream cipher developed as an alternative to AES.

- Block size: 512 bits  
- Key length: 256 bits  
- Faster than AES without hardware support (e.g., AES-NI)  
- Suitable for low-power devices  
- Suitable for high-throughput and low-latency protocols  
- Not vulnerable to timing and cache attacks  
- Vulnerable to power/EM analysis attacks  
- Frequently used in TLS 1.3, WireGuard VPN, etc.

---

## Cryptographic Hash Functions

A cryptographic hash function:

$$
H : \{0,1\}^* \to \{0,1\}^n
$$

- Input: message of arbitrary length  
- Output: fixed-length value  

### Basic Properties

- Deterministic  
- Efficient to compute  
- Small changes in input produce different hashes (integrity property)

### Security Definitions

1. **Preimage resistance**  
   Given $h$, it is hard to find $m$ such that:

   $$
   H(m) = h
   $$

2. **Second preimage resistance**  
   Given $m$, it is hard to find $m' \neq m$ such that:

   $$
   H(m) = H(m')
   $$

3. **Collision resistance**  
   It is hard to find $m, m'$ such that:

   $$
   H(m) = H(m')
   $$

---

### Common Hash Functions

| Hash Function | Output | Security | Application |
|---------------|--------|----------|------------|
| MD5 | 128 bits | Insecure | X |
| SHA-1 | 160 bits | Insecure since 2017 | X |
| SHA-256 | 256 bits | Secure | TLS/SSL, hashing, blockchain |
| SHA-3 / Keccak | 224/256/384/512 bits | Secure | Similar to SHA-2 (but slower without hardware support) |

---

## Message Authentication Codes (MACs)

Used to ensure **integrity** and **authenticity** of messages.

Algorithms: (Gen, Mac, Vrfy)

<img width="480" height="85" alt="Bildschirmfoto 2025-10-07 um 14 44 57" src="https://github.com/user-attachments/assets/3368d58e-15f5-4168-8562-8bcd25d2c91e" />

---

### CBC-MAC

<img width="386" height="169" alt="Bildschirmfoto 2025-10-07 um 14 46 42" src="https://github.com/user-attachments/assets/5a14d656-cc3a-4ea1-ad13-36b37bd92b93" />

Problem with messages of different length:

If

$$
\mathrm{MAC}(M) = t
$$

and

$$
\mathrm{MAC}(B) = s
$$

then the new message

$$
M' = M \parallel (t \oplus B)
$$

has valid tag $s$.

<img width="548" height="173" alt="Bildschirmfoto 2025-10-07 um 14 48 11" src="https://github.com/user-attachments/assets/d0133b39-9acc-439b-9cd9-122da1ca955c" />

---

### HMAC

We use **HMAC** for messages of arbitrary length:

$$
\mathrm{HMAC}_K(m) =
H\bigl((K' \oplus \mathrm{opad}) \parallel
H((K' \oplus \mathrm{ipad}) \parallel m)\bigr)
$$

---

## Authenticated Encryption (AE)

Authenticated Encryption provides:

- Confidentiality  
- Integrity  
- Authenticity  

A secure construction must combine encryption and authentication properly.

---

### Generic Constructions

1. **Encrypt-then-MAC (EtM)**  
   - First encrypt the plaintext:
     $$
     c = \mathrm{Enc}_k(m)
     $$
   - Then compute a MAC over the ciphertext:
     $$
     t = \mathrm{MAC}_{k'}(c)
     $$
   - Send $(c, t)$

   ✔ Secure (if encryption and MAC are secure)

---

2. **MAC-then-Encrypt (MtE)**  
   - First compute MAC:
     $$
     t = \mathrm{MAC}_{k'}(m)
     $$
   - Then encrypt:
     $$
     c = \mathrm{Enc}_k(m \parallel t)
     $$

   ⚠ Used in older TLS versions  
   ⚠ Vulnerable to padding oracle attacks

---

3. **Encrypt-and-MAC (E&M)**  
   - Encrypt plaintext  
   - Compute MAC over plaintext separately  

   ❌ Not secure in general  

---

### Authenticated Encryption with Associated Data (AEAD)

- Encrypts message
- Authenticates message
- Authenticates additional metadata (e.g., headers)

Examples:

- AES-GCM  
- ChaCha20-Poly1305  

---

## Asymmetric Cryptography

In asymmetric cryptography:

- There is a public key $pk$
- There is a private key $sk$

Encryption:

$$
c = \mathrm{Enc}(pk, m)
$$

Decryption:

$$
m = \mathrm{Dec}(sk, c)
$$

Security requirement:

$$
\mathrm{Dec}(sk, \mathrm{Enc}(pk, m)) = m
$$

---

### Public Key Encryption (PKE)

Algorithms: (Gen, Enc, Dec)

- $\mathrm{Gen}(1^\lambda) \to (pk, sk)$  
- $\mathrm{Enc}(pk, m) \to c$  
- $\mathrm{Dec}(sk, c) \to m$

Security notion: **IND-CPA / IND-CCA**

---

## RSA

### Key Generation

1. Choose two large primes $p, q$
2. Compute:
   $$
   N = p \cdot q
   $$
3. Compute Euler's totient:
   $$
   \varphi(N) = (p-1)(q-1)
   $$
4. Choose public exponent $e$ such that:
   $$
   \gcd(e, \varphi(N)) = 1
   $$
5. Compute private exponent $d$ such that:
   $$
   e \cdot d \equiv 1 \pmod{\varphi(N)}
   $$

Public key: $(N, e)$  
Private key: $d$

---

### Encryption

$$
c = m^e \bmod N
$$

---

### Decryption

$$
m = c^d \bmod N
$$

---

### Security of RSA

Security is based on:

- Hardness of factoring large integers
- If $N$ can be factored, $d$ can be computed

Important:

Raw RSA is **not secure** (deterministic).  
It must be combined with padding schemes like:

- RSA-OAEP (encryption)
- RSA-PSS (signatures)

---

## Digital Signatures

Digital signatures provide:

- Integrity  
- Authenticity  
- Non-repudiation  

Algorithms: (Gen, Sign, Vrfy)

- $\mathrm{Gen}(1^\lambda) \to (pk, sk)$  
- $\mathrm{Sign}(sk, m) \to \sigma$  
- $\mathrm{Vrfy}(pk, m, \sigma) \to \{0,1\}$  

Correctness:

$$
\mathrm{Vrfy}(pk, m, \mathrm{Sign}(sk, m)) = 1
$$

Security notion:

- **EUF-CMA (Existential Unforgeability under Chosen Message Attack)**  
  An attacker cannot forge a valid signature for a new message, even after requesting signatures on chosen messages.

---

## RSA Signatures

Basic idea:

$$
\sigma = m^d \bmod N
$$

Verification:

$$
m \stackrel{?}{=} \sigma^e \bmod N
$$

In practice, RSA signatures must use padding:

- RSA-PSS (recommended)

Raw RSA signatures are insecure.

---

## Schnorr Signatures

Based on the discrete logarithm problem.

Parameters:

- Prime $p$
- Generator $g$
- Secret key $x$
- Public key:
  $$
  y = g^x \bmod p
  $$

Signature generation:

1. Choose random $k$
2. Compute:
   $$
   r = g^k \bmod p
   $$
3. Compute challenge:
   $$
   e = H(m \parallel r)
   $$
4. Compute:
   $$
   s = k - x \cdot e \pmod{p}
   $$

Signature: $(e, s)$

Verification:

Check whether:

$$
g^s \cdot y^e \equiv r \pmod{p}
$$

Security is based on the hardness of the discrete logarithm problem.

---

## Diffie–Hellman Key Exchange

Goal:

- Establish a shared secret over an insecure channel.

Setup:

- Prime $p$
- Generator $g$

Alice:

- Choose secret $a$
- Send:
  $$
  A = g^a \bmod p
  $$

Bob:

- Choose secret $b$
- Send:
  $$
  B = g^b \bmod p
  $$

Shared secret:

$$
K = g^{ab} \bmod p
$$

Security assumption:

- Computational Diffie–Hellman (CDH)
- Discrete Logarithm Problem (DLP)

---

### Man-in-the-Middle Problem

Basic Diffie–Hellman does not provide authentication.

An attacker can:

- Intercept $A$
- Replace it
- Intercept $B$
- Replace it

Solution:

- Combine DH with digital signatures or certificates
- Use authenticated key exchange (e.g., TLS)

---

## Public Key Infrastructure (PKI)

Problem:

How do we know that a public key belongs to a specific entity?

Solution:

Certificates issued by a Certificate Authority (CA).

A certificate contains:

- Public key
- Identity information
- Validity period
- Signature of CA

Verification:

1. Verify CA signature
2. Check certificate chain
3. Check revocation status

---

### Certificate Chain

- Root CA (trusted)
- Intermediate CA
- End-entity certificate

Trust model:

- Root CAs are pre-installed in operating systems and browsers.

---

### Certificate Revocation

If a key is compromised:

- Certificate must be revoked.

Mechanisms:

- CRL (Certificate Revocation List)
- OCSP (Online Certificate Status Protocol)

---

## Transport Layer Security (TLS)

TLS provides:

- Confidentiality  
- Integrity  
- Authentication  

TLS uses a combination of:

- Asymmetric cryptography (for key exchange and authentication)
- Symmetric cryptography (for data encryption)
- Hash functions (for integrity)

---

## TLS Handshake (Simplified)

1. **ClientHello**
   - Supported TLS versions
   - Supported cipher suites
   - Random value

2. **ServerHello**
   - Selected TLS version
   - Selected cipher suite
   - Random value
   - Certificate

3. **Key Exchange**
   - Diffie–Hellman (or ECDHE)
   - Shared secret is established

4. **Finished Messages**
   - Both parties verify handshake integrity

After the handshake:

- Symmetric session keys are used for encryption.

---

## Forward Secrecy

Forward Secrecy means:

> Compromise of long-term private key does not compromise past session keys.

Achieved using:

- Ephemeral Diffie–Hellman (DHE, ECDHE)

Without Forward Secrecy:

- If private key is leaked, past traffic can be decrypted.

---

## Cipher Suites

A TLS cipher suite defines:

- Key exchange algorithm
- Authentication algorithm
- Symmetric cipher
- Hash/MAC algorithm

Example:

```
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
```

Meaning:

- ECDHE: Key exchange
- RSA: Authentication
- AES_128_GCM: Encryption
- SHA256: Hash

---

## Downgrade Attacks

Attacker forces client and server to use:

- Older TLS versions
- Weaker cipher suites

Example:

- Version rollback
- Cipher suite rollback

Modern TLS versions (1.3) include downgrade protection.

---

## Padding Oracle Attack (TLS Context)

Applies to:

- CBC mode in TLS

If server reveals padding errors:

- Attacker can decrypt ciphertext block by block.

Mitigation:

- Use AEAD modes (AES-GCM, ChaCha20-Poly1305)
- Use constant-time implementations

---

## Man-in-the-Middle (MitM)

Attacker:

- Intercepts communication
- Modifies messages

Mitigation:

- Certificate validation
- PKI
- HSTS

---

## Man-on-the-Side (MotS)

Attacker:

- Can observe traffic
- Can inject packets
- Cannot block or modify packets

Typical attack:

- DNS injection
- TCP RST injection

---

## DNS Manipulation

### DNS Injection

- Attacker injects fake DNS response.
- Race condition: client accepts first valid response.

### DNS Filtering

- DNS requests or responses are blocked.
- Requires blocking capability (not pure MotS).

---

## IP Blocking

- Blocking traffic to specific IP addresses.
- Can occur at:
  - End device
  - ISP
  - Firewall
  - State-level filtering

Limitation:

- One IP can host multiple domains.



