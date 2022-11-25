
```
NOTE: Currently in development. Please check back soon! 
```

# Cryptography Overview

## [Table of Contents]{.underline}

\[0\] History

-   Timeline

-   Early Cryptographic Systems

\[1\] Encryption Standards

-   Certificates & Digital Signatures

-   PKI

\[2\] Fundamentals - Recap

-   General Terms

-   Attacks / Threats

\[3\] Number Theory

\[4\] Symmetric Cryptography

-   Recap

-   Stream Ciphers (5)

-   Block Ciphers (12)

-   Block Cipher Modes (6)

\[5\] Asymmetric Cryptography (5)

\[6\] Hash Functions (8)

\[7\] Bitcoin

\[8\] WiFI Encryptions

\[9\] Tunneling

\[10\] Key Exchanges

\[11\] Secure Channel

\[12\] Random Number Generators

\[13\] Formulas

# \[0\] History

## [0a. Timeline]{.underline}

+------------+---------------------------------------------------------+
| Year       | Event                                                   |
+============+=========================================================+
| 1466 --    | Cipher disk → invented by Leon Alberti. The cipher disk |
|            | (like Scytale) is a physical device used to encrypt.    |
+------------+---------------------------------------------------------+
| 1553 --    | Vigenere Cipher → invented by Giovan Battista Bellaso.  |
|            | Widely-used cipher (Poly-alphabetic substitution) until |
|            | the 1900s.                                              |
+------------+---------------------------------------------------------+
| 1854 --    | Playfair Cipher → invented by Charles Wheatstone        |
+------------+---------------------------------------------------------+
| WWI --     | ADFGVX Cipher → invented by Colonel Fritz Nebel (1918). |
|            | Used by the German army in WWI.                         |
+------------+---------------------------------------------------------+
| WWII --    | Enigma Machine used by Nazi Germany. Cracked in 1932.   |
|            | invented by Arthur Scherbius (1918)                     |
+------------+---------------------------------------------------------+
| 1976 --    | DES → Block encryption, chosen by NIST as standard (til |
|            | cracked in 1997), 56-bit keys. Eventually replaced by   |
|            | AES (2000).                                             |
|            |                                                         |
|            | Previously named the 'Lucifer' algorithm.               |
+------------+---------------------------------------------------------+
| 1977 --    | DH → Public key encryption proposed by Hellman and      |
|            | Diffie                                                  |
+------------+---------------------------------------------------------+
| 1978 --    | RSA → invented by MIT researchers (Ron Rivest, Adi      |
|            | Shamir, and Len Aldeman)                                |
+------------+---------------------------------------------------------+
| 1987 --    | RC4 → Ron's Cipher (Ron Rivest). Most widely-used       |
|            | stream cipher. Key size of 1-256 bits.                  |
+------------+---------------------------------------------------------+
| 1988 --    | X.509 → (standard for digital signatures) first used    |
+------------+---------------------------------------------------------+
| 1991 --    | PGP → Phil Zimmermann releases the public key           |
|            | encryption program PGP along with its source code       |
+------------+---------------------------------------------------------+
| " --       | DSA → (Digital Signature Algorithm) filed by David      |
|            | Kravitz. US Patent 5,231,668. Adopted by US Gov in 1994 |
|            | (FIPS 186)                                              |
+------------+---------------------------------------------------------+
| 1993 --    | FISH → (Fibonacci Shrinking) published by Siemens.      |
|            | Using the lagged fibonacci generator.                   |
+------------+---------------------------------------------------------+
| 1995 --    | TIGER → designed by Ross Anderson                       |
+------------+---------------------------------------------------------+
| 2000 --    | AES → (Rijndael) announced as replacement for DES with  |
|            | FIPS 197. Key size of 128, 192, 256.                    |
+------------+---------------------------------------------------------+
| 2005 --    | ECC → advanced public-key crypto-scheme. Allows shorter |
|            | encryption keys. More challenging to break than RSA &   |
|            | DH.                                                     |
|            |                                                         |
|            | It's perfect for smart cards, smartphones, and IoT      |
|            | devices.                                                |
+------------+---------------------------------------------------------+

## [0b. Timeline]{.underline}

➢ **Historical cryptosystems** →

-   Based on symmetric key encryption schemes. The only security service
    > these systems provide is confidentiality of info.

-   These earlier cryptographic systems are also referred to as
    > [Ciphers]{.underline}.

    -   In general, a cipher is simply just a set of steps (*an
        > algorithm*) for performing both an encryption, and the
        > corresponding decryption.

-   2 properties → **Substitution** or **Transposition**

(1) [Substitution]{.underline} → Taking one variable, and swapping for
    > another. (*confusion is accomplished using substitution*)

(2) [Transposition]{.underline} → Scrambling. (*diffusion \[randomness\]
    > is accomplished using transposition*)

-   Confusion & Diffusion: create an Avalanche effect (*small plaintext
    > changes, result in large ciphertext effects*).

-   Diffusion - randomness. changes to one character in the plaintext
    > causes multiple changes in the ciphertext.

-   Confusion - attempts to make the relationship b/w the ciphertext and
    > key as complex as possible.

\[A\] **Mono-alphabetic** substitution ciphers →

-   a single mapping from our alphabet to a cipher alphabet. highly
    > susceptible to cryptanalysis.

1)  [Pigpen]{.underline} → mapping plaintext characters to [graphical
    > characters]{.underline} (*rather than to alphabetic ones*).

    -   i.e. A=(pick a symbol), vs A=(pick a letter).

    -   Disadvantage: once the mapping is known, it is difficult to keep
        > the message secret.

2)  [Caesar]{.underline} → known as \"shift\" cipher (*ex. Shift letter
    > 3 spaces*)

    -   i.e., shift of +3 would mean a plaintext letter A would result
        > in a ciphertext letter D.

3)  [ROT13]{.underline} →

    -   "Rotate 13". Simple letter substitution cipher, replaces a
        > letter with the 13th letter after it in the alphabet.

4)  [Atbash]{.underline} →

    -   [Reverses]{.underline} the alphabet (*A becomes Z, B becomes Y
        > \...* )

\[B\] **Poly-alphabetic** substitution ciphers →

-   The cipher alphabet for the plain alphabet may be different at
    > different places during the encryption process.

1)  [Vigenere]{.underline} →

    -   uses a text string as a key (*i.e a word like "point"*),\
        > which is then used for doing a number of shifts on the
        > plaintext.

        -   Each alphabet of the key is converted to its respective
            > numeric value: In this case,

        -   p → 16, o → 15, i → 9, n → 14, and t → 20.

        -   Thus, the key is: 16 15 9 14 20.

    -   This is a difficult cipher to break/guess.

2)  [Playfair]{.underline} →

    -   pairs of letters are encrypted (*simple substitution cipher*),
        > instead of single letters.

    -   This cipher uses a 5x5 matrix with non-repeating characters.

    -   A key table is created (5x5, using 25 letters).

        -   HI → QC (*the ciphertext*)

3)  [Enigma Machine]{.underline} →

    -   Used a polyalphabetic substitution cipher, which didn't repeat
        > w/in a reasonable time period, along w/ a secret key.

    -   For the cracking of the Enigma cipher, the challenge was thus to
        > determine both the algorithm used and the key.

    -   Enigma's main weakness was that none of the plain text letters
        > could be ciphered as itself.

\[C\] **Transposition Cipher** →

-   Rearrange/mutate the order of the letters (*ex. FADE is rearranged
    > to DFEA, with a key of 3142*).

-   Reading message from L-R (*and up-down if in a table*)

1)  [Rail Code]{.underline} → Employs a method to scramble text by
    > writing it in a sequence across a number of different rails

\[D\] **Square Ciphers** →

1)  [BIFID]{.underline} → uses a grid to map letters INTO numbers.

    -   25 letters, 5x5 grid.

2)  (*see above*) [Playfair]{.underline} →

3)  [Four-Square]{.underline} →

    -   Uses four 5 × 5 matrices arranged in a square, where each matrix
        > contains 25 letters for encoding and decoding operations.

    -   encrypts pairs of letters (like playfair)

    -   Locate the characters in the ciphertext at the corners of the
        > rectangle

    -   ATTACK AT DAWN \--\> **AT** **TA** **CK** **AT** **DA** **WN**\
        > ATTACKATDAWN → TIYBFHTIZBSY

4)  [ADFGVX Cipher]{.underline} →

    -   The key for this algorithm is a six-by-six square made up of the
        > letters ADFGVX forming the outer row and column, the rest of
        > the table is composed of the letters of the alphabet and the
        > numbers 0 through 9 distributed randomly in the square.

    -   Used by the German army in WWI. Invented by Colonel Nebel in
        > 1918.

\[E\] **Others** →

1)  [One-Time Pad]{.underline} →

    -   Cipher code mapping that is used only once.

    -   Advantage is it is essentially unbreakable,

    -   disadvantage is it takes lots of work as you\'d have to generate
        > the pad to be used, each time.

2)  [Morse Code]{.underline} →

    -   Encoding method, which translates characters into sequences of
        > dots (.) and dashes (-)

# \[1\] Encryption Standards

## [1a. Certificates & Digital Signatures]{.underline}

➢ **CA** (*Certificate Authority*) →

-   Q. A business wants to be trusted: The certificate issued to the
    > business should be signed by...

    -   A: **Root CA's private key**.

-   Q. A business wants to be trusted: Which key should the business
    > send to customers?

    -   A: **Public key of the business**.

➢ **Certificates** →

-   [CRL]{.underline} (*certificate revocation list*): contains revoked
    > certificates

-   [CA]{.underline} (*certificate authority*): component of PKI that
    > creates & maintains digital certificates throughout their life
    > cycles.

    -   [RA]{.underline} (*Registration Authority*): responsible for
        > accuracy of the info contained in a certificate request. User
        > validation.

-   [CP]{.underline}: (certificate policy) How a certificate may be
    > used.

-   [OCSP]{.underline} (*online certificate status protocol*):

    -   Protocol for verifying the status of certificates (*i.e.
        > revoked, valid, unknown*).

-   CLASSES →

    -   [Class 4 certificates]{.underline}: Government security

    -   [Class 3 certificates]{.underline}: servers & software signing,
        > for which independent verification and checking of identity
        > and authority is done by issuing CA.

    -   [Class 2 certificates]{.underline}: organizations for which
        > proof of identity is required.

    -   [Class 1 certificates]{.underline}: individuals, and intended
        > for email.

➢ **X.509** (*digital signature standard*) →

-   Q: What should an admin use to import & export all items (*written
    > using X.509*) that are part of the chain of trust?

    -   A: PKCS #12 (*Public Key Cryptography Standard*)

-   Q: In an X.509 certificate, which fields displays the hash (*or
    > digest*) of the certificate?

    -   A: Thumbprint (*note; SHA-1 is an algorithm that generates the
        > thumbprint of a certificate*)

## [1b. PKI (Public Key Infrastructure)]{.underline}

➢ **PKI** →

-   PKI performs encryption directly through the keys that it generates.
    > It works by using two different cryptographic keys:

    -   a public key and a private key. Whether these keys are public or
        > private, they encrypt and decrypt secure data.

-   Solutions for creating and managing public-key encryption.

-   PKI services: Confidentiality, Integrity, Availability,
    > Authentication, Non-repudiation.

-   A PKI is often set up w/ multiple levels of CAs. 'Root' is the top
    > level CA, and lower-level CAs verify the user keys.

    -   In PKI, Bob encrypts the message w/ Alice's Public key. Alice
        > then decrypts the message w/ her private key.

# \[2\] Fundamentals - Recap

## 2a. General Terms

➢ **Cryptography** →

-   The science of transforming information into unintelligible form
    > (*ciphertext*)

-   FIPS 140: covers cryptographic modules.

    -   [NOTE]{.underline}: *FIPS 186- Digital Signatures; FIPS 197-
        > AES; FIPS 201- ID;*)

➢ **Steganography** →

-   Process that puts a message into the least significant bits of a
    > binary file. Writing hidden messages.

➢ **Differential Cryptanalysis** →

-   Applicable to symmetric key algorithms. Invented by Biram & Shamir.
    > Examines the dif in an input AND the affects output.

-   Cryptanalysis → requires Time, Memory, Data.

➢ **Encryption** →

-   changing [plaintext into ciphertext]{.underline}; **decryption** is
    > the process of changing it back.

-   Encryption should be applied to [information you want to
    > protect]{.underline} → at-rest/in-transit.

    -   Encrypt [individual files]{.underline} → (*like EFS, Aescrypt*),

    -   Encrypt [full disks]{.underline} → (*Bitlocker/FileVault*).

➢ **Nonce** → a number used 1x, then discarded.

➢ **TGS** (*Ticket Generating Server*) → generages Kerberos tickets.

➢ **Kerchoff's principle** → only the key needs to be secret, not the
algorithm (*can be disclosed w/out damaging security*).

➢ **IPSec** → provides a method of setting up a secure channel for
protected data exchange between 2 devices.

➢ Random number generators →

(1) **Pseudo-Random Number Generators** (*PRNGs*) → FAST

    -   This method repeats the random numbers after a given time
        > (*periodic*).

    -   They are fast and useful in producing a repeatable set of random
        > numbers, but [deterministic]{.underline} (*predictable*).

(2) **True Random Number Generators** (*TRNGs*) → SLOW

    -   Generates a true random number and uses some form of random
        > process.

    -   One approach is to monitor the movements of a mouse pointer on a
        > screen or from the pauses between keystrokes.

    -   Overall, the method is generally slow, especially if it involves
        > human interaction, but is [non-deterministic and
        > aperiodic]{.underline}.

➢ Randomness →

-   **IV** → a fixed-size pseudo-random number, fed into a symmetric
    > cipher (*to increase randomness during encryption*).

    -   Q: What can XOR use as a pseudorandom number to create a unique
        > ciphertext? → **IV**

    -   Q: How does CBC create randomness in a second block after
        > encrypting the first block with an IV? → **Uses the results of
        > the IV to encrypt the next block.**

-   **Salt** → random bits intermixed w/ a hash (*to increase randomness
    > and reduce collisions*).

➢ **Frequency Analysis** → cipher cracking methodology

-   that involves identifying patterns and variations in the probability
    > of codes.

-   i.e. a three-letter ciphered text combination spotted at the
    > beginning of a string too often could tip us off that those three
    > letters correlate the letters THE in the English alphabet.

➢ **Entropy →** measures the amount of unpredictability;

-   in encryption, it relates to the degree of [uncertainty of the
    > encryption process]{.underline}.

➢ Two common binary to characters encoding methods

1.  **ASCII** (*8-bit values, up to 256 characters*)

2.  **UTF-16** (*16- bit values*, *up to 65,536 characters*).

-   Other encoding methods include hexadecimal, Base-64, and Base-58.

➢ Hardware vs Software encryption.

-   [Hardware encryption is more efficient]{.underline} than software
    > encryption.

➢ HSM & TPM →

-   **HSM** → is a tamper-evident and intrusion-resistant physical
    > device that safeguards and manages cryptographic keys and provides
    > cryptographic processing.

-   **TPM** → a dedicated processor/microchip that handles
    > hardware-level encryption; allows the use of full disk encryption
    > on a hard drive in a manner that minimizes the impact on system
    > performance. TPM contains the encryption keys.

➢ **Key Space** →

-   Total number of possible keys. The less the key space, the less
    > possible keys/pins available.

    -   4-digit PIN → max of 10,000 possible values.

    -   5-digit PIN → max of 100,000 possible values.

-   Length of the key → indication of the strength of the cryptosystem.

    -   Longer the key → harder to guess.

➢ Authentication Protocols →

-   **PAP** (*password authentication protocol*): using PPP to validate
    > users. Less secure than CHAP, and old.

-   **CHAP** (*Challenge handshake authentication protocol*): Also uses
    > PPP. More secure than PAP. 3-way handshake (*requires both the
    > server & client to run the password through a hash function along
    > with an OTP sent from the server*).

-   **EAP** (*Extensible Authentication Protocol*): Also uses PPP. Newer
    > and more advanced (*than PAP, CHAP*). Uses auth methods (*ex.
    > EAP-TLS, PEAP, LEAP, EAP-Fast, etc.*).

## 2b. Attacks / Threats

➢ Attacks/Threats →

-   **Ciphertext-only attack**: attacker has access to ONLY the
    > ciphertext(s).

-   **Known Plaintext attack**: attacker is assumed to have access to
    > sets of corresponding plaintext AND ciphertext.

-   **Statistical attack**: attacker uses identified statistical
    > patterns.

-   **Algebraic attack**: exploits vulnerabilities w/in the intrinsic
    > algebraic structure of mathematical functions.

-   **Birthday attack**: depends on duplicate values occurring.

-   **Frequency analysis attack**:

# \[3\] Number Theory

➢ **Binary Math**: Basic premise is knowing what combination of binary
digits will produce a binary "1".

-   AND → requires two 1's to output a 1. (**1 & 1 = 1**)

-   OR → requires at least one 1 to output a 1. (**1 OR \_ = 1**)

-   XOR → there must be a mismatch (i.e., one 1 and one 0) to output
    > a 1. (**1 XOR 0 = 1**)

➢ **Set Theory**:

+-----------------------+--------------+-------------------------------+
| SYMBOL NAME           | SYMBOL       | DESCRIPTION                   |
+=======================+==============+===============================+
| Intersection \[AND\]  | A ∩ B        | \- The objects in the final   |
|                       |              | set are from A & B            |
|                       |              |                               |
|                       |              | \- Ex. union of {1, 2, 3} &   |
|                       |              | {2, 3, 4} → {2, 3}.           |
+-----------------------+--------------+-------------------------------+
| Union \[OR\]          | A ∪ B        | \- The objects in the final   |
|                       |              | set are from A or B           |
|                       |              |                               |
|                       |              | \- Ex. union of {1, 2, 3} +   |
|                       |              | {2, 3, 4} → {1, 2, 3, 4}.     |
+-----------------------+--------------+-------------------------------+
| Subset \[subset of\]  | A ⊆ B        | \- Ex. A ⊆ B expresses that A |
|                       |              | is a subset of B,             |
|                       |              |                               |
|                       |              | i.e., [every]{.underline}     |
|                       |              | member of A is a member of B  |
|                       |              |                               |
|                       |              | \- subset has fewer elements  |
|                       |              | or equal to the set           |
+-----------------------+--------------+-------------------------------+
| Belongs to            | ∈            | \- relation symbol ∈ for      |
|                       |              | membership.                   |
| \[member of a set\]   |              |                               |
|                       |              | \- A∈B → A is a member of the |
|                       |              | set B                         |
+-----------------------+--------------+-------------------------------+
| Does not belong to    | \[∈ with     | \- when an object is NOT in a |
|                       | diagonal     | set                           |
| \[member not part     | slash\]      |                               |
| of\]                  |              |                               |
+-----------------------+--------------+-------------------------------+
| Such that             | \|           | "So that"                     |
+-----------------------+--------------+-------------------------------+

➢ **Modulus Operator Math** →

-   Returns the remainder → after X is divided into by Y.

    -   X mod Y = \[remainder of X / Y\]\
        > 20 mod 6 = \[remainder of 20 / 6\] = 3 with **remainder of 2**

    -   

-   Ex. 7 mod 4

    -   7 / 4 = 1 \[**with remainder of 3**\]

    -   Therefore, 7 % 4 = **[3]{.underline}**.

-   Ex. 25 mod 7

    -   25 / 7 = 3. \[**with remainder of 4**\]

    -   Thus 25 % 7 = **[4]{.underline}**.

➢ **Combination vs Permutation** →

-   combinations = not concerned with the order

-   permutations = all options considered including sequence.

➢ In **probability theory** →

-   we determine the likelihood of an event happening, typically by
    > understanding the chances of how each of the elements involved in
    > an event interact, and the likelihood of them happening. \>\>

    -   Dependent, Independent, and mutually exclusive.

➢ **Prime number** → is a value which only has factors of 1 and itself
(*ex. 7, 13, 23, etc*.)

-   and used in areas such as [key exchange]{.underline} and in [public
    > key encryption]{.underline}.

-   Factorizing the result of the multiplication of 2 large prime
    > numbers → takes huge amounts of computational power & time.

# \[4\] Symmetric Cryptography

## 4a. Recap

➢ **Symmetric Cryptography (***aka Secret Key encryption***)**

-   makes use of a [single secret key]{.underline} for both encryption
    > and decryption.

-   Since the same key is used for both encryption and decryption, a
    > challenge that exists is

    -   finding a secure way to share or transport the key between the
        > sender & receiver (*decrypter*).

-   Ex. AES is a secure symmetric algorithm.

+-----------------------------------+-----------------------------------+
| Advantages                        | Disadvantages                     |
+===================================+===================================+
| \- FASTER                         | \- Key management / Key           |
|                                   | distribution                      |
| -   Allows us to quickly encrypt  |                                   |
|     > bulk messages.              | \- Scalability issue. For each    |
|                                   | pair of people that need to talk  |
| \- Algorithms freely available.   | → they need another key. If you   |
| Many strong versions.             | have 10 people that need to       |
|                                   | communicate → you'll need 45      |
| -   AES isn't able to be          | different keys. Formula →         |
|     > brute-forced easily.        | N(N-1)/2 = 10 x ((10-1)/2) = 45   |
|                                   |                                   |
| \- Excellent confidentiality      | \- Even with 1000 users, you'd    |
|                                   | need around 1,000,000 keys...This |
| -   But, limited integrity.       | isn't feasible in a large user    |
|                                   | population.                       |
|     -   Can be used w/ hash       |                                   |
|         > values, or CBC MAC → to | \- What if distributing keys out  |
|         > ensure the integrity    | of band? → need to transmit in a  |
|                                   | different channel (*than the one  |
| -   The weakness usually comes    | to transmit the actual message*)  |
|     > from the                    |                                   |
|     > implementation/tool of the  | \- Doesn't provide much beyond    |
|     > algorithm.                  | confidentiality & some integrity. |
|                                   | Will need to be addressed w/ more |
|                                   | modern implementations.           |
|                                   | Advantages → \[1\] Fast (ideal    |
|                                   | for bulk encryption; good for     |
|                                   | streaming media, ex. VoIP, video  |
|                                   | feeds), \[2\] Confidentiality     |
|                                   | (BUT, \[*problem*\] the           |
|                                   | crypto-variable must be           |
|                                   | distributed through some sort of  |
|                                   | secure means → meaning            |
|                                   | distributing it out-of-band).     |
+-----------------------------------+-----------------------------------+

➢ **Symmetric Key Exchange - recap**:

-   **Major problem** of secret-key encryption → how to pass the key
    > between the entity encrypting and the entity decrypting.

-   **TWO main methods for key exchange** in symmetric cryptography
    > → (1) Use a key exchange algorithm (such as Diffie-Hellman).
    > Encrypt the key with the recipient's public key; (2) Pass it to
    > the other side and then allow the recipient to use their private
    > key to decrypt it (i.e., via public key encryption).

-   **Forward secrecy** →

    -   Important key exchange concept -- usage of forward secrecy.

    -   Means that a compromise of the long-term keys will NOT
        > compromise any previous session keys.

    -   Q: Which encryption component ensures the compromise of
        > long-term key prevents the compromise of any previous session
        > keys? → Forward Secrecy

-   **Ephemeral key** →

    -   Temporary, per session.

    -   Aka cryptographic key. It's generated for each
        > execution/connection.

    -   The leakage of any long-term key would not cause all the
        > associated session keys to be breached.

➢ **Diffie-Hellman** → (*an asymmetric cipher, used for key exchange of
secret key in symmetric cryptography*)

-   DH methods have been used extensively to create a shared secret key,
    > but suffers from MitM attacks. An improved method is to use public
    > key encryption.

    -   Weakness: it's fairly easy to precompute on values for two
        > popular Diffie-Hellman parameters (*and which use the
        > DHE_EXPORT cipher set*).

-   The DHE_EXPORT Downgrade attack →

    -   Involves forcing the key negotiation process to default to
        > 512-bit prime numbers. For this the client only offers
        > DHE_EXPORT for the key negotiation, and the server, if it is
        > set up for this, will accept it. The precomputation of 512-bit
        > keys with g values of 2 and 5 (*which are common*) are within
        > a reasonable time limit.

    -   [Methods to combat DHE_EXPORT Downgrade attacks]{.underline}:\
        > (1) Disabling → Export Cipher Suites,\
        > (2) Use ECDHE -- Elliptic-Curve DH \[Ephemeral\].\
        > (3) Use a strong group.

```{=html}
<!-- -->
```
-   DH has three groups (bases): Group 1, 3 or 5, which vary in the size
    > of the prime number used.

    -   Ex. when using IPSec, you often use DH groups (*to calculate
        > what the symmetric crypto-variable will be*).

    -   The strength of the DH relates to the [size of the prime number
        > bases]{.underline} which are used in the key exchange.

➢ Two types of symmetric encryption (*Stream & Block*):

1.  **[Stream]{.underline} encryption** →

-   involves [encrypting one bit at a time]{.underline}, i.e., a
    > synchronous stream.

```{=html}
<!-- -->
```
-   Symmetric stream encryption is often much faster than block and can
    > typically be applied in real-time applications.

    -   Best for hardware (0s & 1s).

-   \[4\] RC4, ChaCha, FISH, PIKE

2.  **[Block]{.underline} encryption** →

-   Involves grouping data into blocks, and [encrypting the individual
    > blocks]{.underline}.

    -   Ex. AES

    -   Best for software level.

```{=html}
<!-- -->
```
-   Padding is used to fill blocks to operating size when the data does
    > not fit perfectly.

-   Manage how blocks of data are processed through block cipher mode
    > implementations.

    -   For instance, one may choose to use the DES block cipher
        > configured with ECB as the mode of operation.

-   Common block cipher modes → ECB, CBC, **CFB**, **OFB**, **CTR**, &
    > PCBC

    -   CFB, OFB, and CTR → allow the block cipher to operate like a
        > stream cipher.

-   With block ciphers, the plaintext & ciphertext are always the same.

➢ **S-boxes** (*substitution boxes*) →

-   Secret key ciphers make use of substitution boxes (S-boxes) to
    > perform substitution as part of the encryption process.

-   S-boxes take a given input and leverage look-up tables to produce a
    > given output.

➢ **Work factor** →

-   The work needed to be able to break the cipher code

-   As processing power magnifies, security of current ciphers decreases
    > (*work factor decreases*)

➢ **Salting** →

-   Process of adding an IV to the ciphering process to change its
    > operation

-   Ensures that the ciphertext does not give the original plaintext
    > when played back

## 4b. Stream Ciphers

+----+----------------+----------------------+------------------------+
| \# | Stream         | Key Size             | Block Size             |
|    |                |                      |                        |
|    |                | (bits)               |                        |
+====+================+======================+========================+
| 1  | RC4            | 40 -- 2048           | N/A                    |
|    |                |                      |                        |
|    |                | (WEP→ 40 bit key)    |                        |
+----+----------------+----------------------+------------------------+
| 2  | ChaCha         | 256                  |                        |
+----+----------------+----------------------+------------------------+
|    |                |                      |                        |
+----+----------------+----------------------+------------------------+
| 3  | FISH           | ----                 | N/A                    |
+----+----------------+----------------------+------------------------+

## 4c. Block Ciphers

➢ **Block Ciphers - recap**:

-   Used when total plaintext is available BEFORE we do the encryption.
    > (*Emails, Word docs, Spreadsheets*)

    -   Block-mode cipher provides a great level of confidentiality, and
        > some integrity.

-   Symmetric block encryption → involves first grouping data to be
    > encrypted (*typically your plaintext*)n into blocks of a specific
    > size and then encrypting those blocks.

-   Block cipher modes merely outline [how the blocks will be
    > handled]{.underline} depending on the implementation selected
    > (*i.e., which mode is used*). Implementation selection can be
    > based on anything just as type of cipher can.

    -   Factors can include security needs or not, processing capacity,
        > organization preference, etc.

-   At minimum, each block of data will be encrypted using the
    > encryption key of the block cipher being used as you will see with
    > ECB. Other variations are configured to incorporate additional
    > components to meet desired security and/or performance.

-   Most modern block ciphers have a 128-bit block size

+-----------+-----------+-----------+-----------+-----------+-----------+
| \#        |           | Key Size  | Block     | Rounds    | NOTE:     |
|           |           |           | Size      |           |           |
|           |           | (bits)    |           |           |           |
|           |           |           | (bits)    |           |           |
+===========+===========+===========+===========+===========+===========+
| 1         | DES       | 56        | 64        | 16x       |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 2         | 3DES      | 112       | 64        | 48x       |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 3         | AES       | 128, 192, | 128       | 10x, 12x, |           |
|           |           | 256       |           | 14x       |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 4         | Blowfish  | 32 → 448  | 64        | 16x       | \-        |
|           |           |           |           |           | Feistel   |
|           |           |           |           |           | cipher.   |
|           |           |           |           |           | By Bruce  |
|           |           |           |           |           | Schneier. |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 5         | Twofish   | (up to)   | 128       | 16x       | \-        |
|           |           | 256       |           |           | Feistel   |
|           |           |           |           |           | cipher.   |
|           |           |           |           |           | By Bruce  |
|           |           |           |           |           | Schneier+ |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 6         | Skipjack  | 80        | 64        | 32x       | \- Dev.   |
|           |           |           |           |           | by NSA    |
|           |           |           |           |           | for use   |
|           |           |           |           |           | in        |
|           |           |           |           |           | clipper   |
|           |           |           |           |           | chip      |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 7         | IDEA      | 128       | 64        | \>17x     | \- 1991.  |
|           |           |           |           |           | 8         |
|           |           |           |           |           | identical |
|           |           |           |           |           | transf    |
|           |           |           |           |           | ormations |
|           |           |           |           |           | per       |
|           |           |           |           |           | round.    |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 8         | TEA       | 128       | 64        | (s        | \- 1994.  |
|           |           |           |           | uggested) | Wheeler & |
|           |           |           |           | 64x       | Needman.  |
|           |           |           |           |           | Feistel.  |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 9         | CAST      | 40 → 128  | 64        | 12x, 16x, |           |
|           |           |           |           | (*\>80*)  |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 10        | SHARK     | 128       | 64        | 6x        | \-        |
|           |           |           |           |           | Rijmen,   |
|           |           |           |           |           | Daemen,   |
|           |           |           |           |           | Preneel,  |
|           |           |           |           |           | Bosselaer |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 11        | Serpent   | 128, 192, | 128       | 32x       |           |
|           |           | 256       |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+
| 12        | RC5       | 1 → 2048  | 32, 64,   | (up to)   |           |
|           |           |           | 128       | 255x      |           |
|           | RC6       |           |           |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+

+---+---------------+---------------------------------------------------+
| \ | Block Cipher  | Description                                       |
| # |               |                                                   |
|   | MODES         |                                                   |
+===+===============+===================================================+
| 1 | ECB:          | \- Simplest mode of encryption. Each plaintext    |
|   | Electronic    | block/group is encrypted separately w/ same key   |
|   | Codebook      | (*then decrypted separately*).                    |
|   |               |                                                   |
|   |               | \- [Always]{.underline} produces the same result  |
|   |               | for the same plaintext                            |
|   |               |                                                   |
|   |               | \- DON'T USE. It has serious weaknesses.          |
+---+---------------+---------------------------------------------------+
| 2 | CBC:          | \- 1st plaintext block → IV to encrypt. Last      |
|   | Cipher-Block  | ciphertext → XOR's w/ next plaintext → THEN its   |
|   | Chaining      | encryption occurs                                 |
|   |               |                                                   |
|   |               | \- Uses an IV to encrypt [ONLY]{.underline} the   |
|   |               | first block, then uses the result of that         |
|   |               | encryption to encrypt the next blocks.            |
|   |               |                                                   |
|   |               | \- Plaintext is XOR'd -- using previous           |
|   |               | ciphertext → [BEFORE]{.underline} being encrypted |
|   |               |                                                   |
|   |               | \- As a result, every subsequent ciphertext block |
|   |               | depends on the previous one. Chaining occurs,     |
|   |               | using IV. Most commonly used mode.                |
+---+---------------+---------------------------------------------------+
| 3 | CFB:\         | \- 1st plaintext block → IV to encrypt. Last      |
|   | Cipher        | ciphertext→ becomes import for encryption         |
|   | Feedback      | algorithm → encrypted output is XOR'd w/          |
|   |               | plaintext. Loops back on itself.                  |
|   |               |                                                   |
|   |               | \- The preceding ciphertext becomes the import    |
|   |               | for the encryption algorithm.                     |
|   |               |                                                   |
|   |               | \- [After]{.underline} the encrypted pseudorandom |
|   |               | output, it's then XOR'd with the next plaintext.  |
|   |               |                                                   |
|   |               | \- Like CBC mode, but this is a stream (not a     |
|   |               | block). The block is turned into a keystream      |
|   |               | generator. Encrypted bit by bit, by bit.          |
|   |               |                                                   |
|   |               | \- Ciphertext from the previous round is          |
|   |               | encrypted each round and then added to the        |
|   |               | plaintext bits.                                   |
+---+---------------+---------------------------------------------------+
| 4 | OFB:          | \- 1st plaintext block → IV to encrypt. Last      |
|   |               | encryption algorithm → becomes import for         |
|   | Output        | encryption algorithm → encrypted output is XOR'd  |
|   | Feedback      | w/ plaintext. Loops back on itself.               |
|   |               |                                                   |
|   |               | \- Same as cipher feedback. Except that the       |
|   |               | encryption algorithm input is the output from the |
|   |               | preceding block. (*CFB uses the previous          |
|   |               | ciphertext as encryption algorithm input, but OFB |
|   |               | uses previous algorithm*)                         |
|   |               |                                                   |
|   |               | \- Can function on streams and create keystreams. |
|   |               |                                                   |
|   |               | \- Turning a block cipher into a stream cipher    |
|   |               | (*by generating a keystream block*), which are    |
|   |               | then XOR'd w/ the plaintext blocks to get the     |
|   |               | ciphertext. .                                     |
|   |               |                                                   |
|   |               | \- Drawback → the repetition of encrypting the IV |
|   |               | may produce the same state that has occurred      |
|   |               | before.                                           |
|   |               |                                                   |
|   |               | \- OFB Loop → a mechanism which mitigates a       |
|   |               | copy-&-paste attack, when using AES.              |
+---+---------------+---------------------------------------------------+
| 5 | CTR:          | \- Counter has a different way of approach. -     |
|   |               | Each plaintext block is XOR'd with an encrypted   |
|   | Counter       | counter (and uses a nonce). The counter is then   |
|   |               | incremented for each subsequent block.            |
|   |               |                                                   |
|   |               | \- Also can turn block cipher into stream cipher  |
|   |               | (*generating a keystream block*),                 |
|   |               |                                                   |
|   |               | \- No error propagation, because the IV comes     |
|   |               | BEFORE the ciphertext. The XOR/IV process is      |
|   |               | applied BEFORE it encrypts the next block of      |
|   |               | data.                                             |
|   |               |                                                   |
|   |               | \- Can function on streams and create keystreams. |
|   |               |                                                   |
|   |               | \- Streams are created regardless of content      |
|   |               | encrypting data.                                  |
|   |               |                                                   |
|   |               | \- Subsequent values of an increasing counter are |
|   |               | added to a [nonce]{.underline} value and the      |
|   |               | results are encrypted as usual.                   |
|   |               |                                                   |
|   |               | \- The nonce plays the same role as IVs in        |
|   |               | previous modes.                                   |
|   |               |                                                   |
|   |               | \- One bit of plaintext or ciphertext is damaged  |
|   |               | → only one corresponding output bit is damaged as |
|   |               | well. Thus, it is possible to use various         |
|   |               | correction algorithms to restore the previous     |
|   |               | value of damaged parts of received messages.      |
+---+---------------+---------------------------------------------------+
| 6 | P-CBC:        | \- Like CBC mode.                                 |
|   | Propagating   |                                                   |
|   | CBC           | \- Mixes bits from previous ciphertext AND        |
|   |               | plaintext blocks [before]{.underline} encrypting  |
|   |               | them.                                             |
|   |               |                                                   |
|   |               | \- If one ciphertext bit is damaged, the next     |
|   |               | plaintext block and all subsequent blocks will be |
|   |               | damaged and unable to decrypt.                    |
+---+---------------+---------------------------------------------------+

# \[5\] Asymmetric Cryptography

➢ **Symmetric Key Exchange**: Using a public and private key.

+---+---------+--------------------------------------------------------+
| \ |         | Summary                                                |
| # |         |                                                        |
+===+=========+========================================================+
| 1 | R S A   | \- Leverages prime number characteristics,             |
|   |         |                                                        |
|   |         | \- Key size: 1024 → 4096 bits                          |
|   |         |                                                        |
|   |         | \- Rounds: 1x                                          |
|   |         |                                                        |
|   |         | \- Authors: Rivest, Shamir, Alderman                   |
+---+---------+--------------------------------------------------------+
| 2 | ECC     | \- used with key exchange methods\                     |
|   |         | (*as with DSA, in creating digital signatures*)        |
|   |         |                                                        |
|   |         | \- Improved solution over RSA                          |
+---+---------+--------------------------------------------------------+
| 3 | D S A   | \- Digital Signature Algorithm                         |
|   |         |                                                        |
|   |         | \- used w/ key exchange methods (*as w/ ECC*)          |
+---+---------+--------------------------------------------------------+
| 4 | El      | \- Used in recent versions of PGP                      |
|   |         |                                                        |
|   | Gamal   | \- Extension of DH, usually the slowest                |
+---+---------+--------------------------------------------------------+
| 5 | DH      | \- ​​No authentication and vulnerable to MITM attacks    |
|   |         |                                                        |
|   | Diffie- |                                                        |
|   |         |                                                        |
|   | Hellman |                                                        |
+---+---------+--------------------------------------------------------+

# \[6\] Hash Functions

+---+----------+------------------+------------------------------------+
| \ |          | [H               | DESCRIPTION                        |
| # |          | ash]{.underline} |                                    |
|   |          | Value (bits)     |                                    |
+===+==========+==================+====================================+
| 1 | MD5      | 128              | \- RFC 1321                        |
|   |          |                  |                                    |
|   | MD6      | 1 → 512          | \- The algorithm operates on a     |
|   |          |                  | 128bit state (divided into 4 32bit |
|   |          |                  | words)                             |
|   |          |                  |                                    |
|   |          |                  | \- Submitted to the NIST SHA-3     |
|   |          |                  | Competition                        |
+---+----------+------------------+------------------------------------+
|   |          |                  |                                    |
+---+----------+------------------+------------------------------------+
| 2 | SHA -1   | \[-1\] 160       |                                    |
|   |          |                  |                                    |
|   | SHA -2   | \[-2\] 256, 384, |                                    |
|   |          | or 512           |                                    |
|   | SHA -3   |                  |                                    |
|   |          | \[-3\] variable  |                                    |
+---+----------+------------------+------------------------------------+
| 3 | RI       | 160              | \- Other versions exist: *-128,    |
|   | PEMD-160 |                  | -256, -320*                        |
|   |          |                  |                                    |
|   |          |                  | \- Original RIPEMD had collision   |
|   |          |                  | issues.                            |
+---+----------+------------------+------------------------------------+
| 4 | FORK-256 | 256              | \- Uses 512-bit blocks             |
+---+----------+------------------+------------------------------------+
| 5 | GOST     |                  | \- Defined by Russian National     |
|   |          |                  | Standard                           |
|   |          |                  |                                    |
|   |          |                  | \- 256-bit output                  |
+---+----------+------------------+------------------------------------+
| 6 | TIGER    | 192              | \- Designed by Ross Anderson & Eli |
|   |          |                  | Biham ('95)                        |
+---+----------+------------------+------------------------------------+
| 7 | MAC /    |                  | \- A MAC uses a block cipher in    |
|   | HMAC     |                  | CBC mode to improve integrity.     |
|   |          |                  | Symmetric key value. Data origin   |
|   |          |                  | authentication                     |
|   |          |                  |                                    |
|   |          |                  | \- An HMAC adds a key to a kash to |
|   |          |                  | improve integrity.                 |
+---+----------+------------------+------------------------------------+

➢ [Note]{.underline}:

-   A message is input into a **hash** function \> then hash value is
    > **encrypted** using the sender's [private key]{.underline}

    -   The result → **[Digital Signature]{.underline}**

-   One character is changed → ENTIRE hash is changed.

-   Windows stores passwords as a hash in a file called a SAM file.

-   Rainbow tables → store common hashes to be used for attacks.

# \[7\] Bitcoin

➢ [Questions]{.underline}:

-   Q: How is information about Bitcoin transitions stored? →

    -   **Distributed peer-to-peer network**

-   Q: What is one of the [primary characteristics of a
    > blockchain]{.underline} in the context of Bitcoin? →

    -   **Adding blocks to a blockchain is computationally expensive**

-   Q: In the context of Bitcoin, what is the length (*in bits*) of the
    > [private key used to sign transactions]{.underline} (*and
    > associated with an individual wallet*)? →

    -   **256 bits**

# \[8\] WiFI Encryptions

+----+-------------+---------------------------------------------------+
| \# | NAME        | DESCRIPTION                                       |
+====+=============+===================================================+
| 1  | WEP         | \- IV size → 24 bits (small)                      |
|    |             |                                                   |
|    |             | \- Key size → 40 bits (RC4) \[*increased to 128   |
|    |             | bits (WPA/TKIP)*\]                                |
+----+-------------+---------------------------------------------------+
| 2  | WPA         | \- IV size → 48 bits (TKIP) \[*increased from 24  |
|    |             | bits (WEP)*\]                                     |
|    |             |                                                   |
|    |             | \- WPA uses 128 bit RC4 stream cipher             |
+----+-------------+---------------------------------------------------+
| 3  | WPA2        | \- WPA-2 advanced the WPA standard, by keeping    |
|    |             | compatibility with WPA, but adding AES-CCMP       |
|    |             | (*AES- Counter-mode CBCMAC Protocol*), which is a |
|    |             | block encryption method.                          |
|    |             |                                                   |
|    |             | \- Again, it supported two modes: Personal (PSK)  |
|    |             | and Enterprise.                                   |
+----+-------------+---------------------------------------------------+

➢ Encryption schemes commonly used with Wi-Fi include:

-   40-bit (RC4 → WEP)

-   128-bit (RC4 → WPA -- Wi-Fi Protected Access)

-   128 / 256-bit (AES → WPA-2)

➢ [Questions]{.underline}:

-   Q: Which mechanism mitigates a copy-and-paste attack when using AES?
    > → **Output Feedback (OFB) loop**

-   Q: What is the max length of encryption keys used by WEP? → **40
    > bits (RCA)**

-   Q: What's a difference between WPA-Enterprise & WPA-Personal? →
    > **Support for an authentication server (enterprise)**

-   Q: Cipher used w/ WEP → **RC4**

-   Q: How does TKIP improve WPA over WEP? → **Hashes the IV and secret
    > key**

# \[9\] Tunneling

➢ [Questions]{.underline}:

-   Q: VPN connection is configured, and is utilizing IPSec tunnel mode
    > (w/ ESP) b/w corporate and remote offices. Where can the packets
    > be inspected by IDSs and virus scanners? → **At headquarters AND
    > offsite office**

-   Q: Which default port must be open for the IPsec key exchange to be
    > successful? → **UDP 500**

-   Q: Which protocol indicates the VPN is using Authentication Header
    > (AH)? → **51**

# \[10\] Key Exchanges

  -----------------------------------------------------------------------
  \#   NAME                     DESCRIPTION
  ---- ------------------------ -----------------------------------------
  1    DH (Diffie-Hellman)      \- Provides a method for key exchange
                                using a one-way function.

  2    MQV                      \- Authentication key agreement (very
       (Menezes-Qu-Vanstone)    similar to DH)

  3    ECDH (Elliptic Curve     \- Ensures PFS during key exchange
       Diffie-Hellman)          

  4    KEA (Key Exchange        
       Algorithm)               
  -----------------------------------------------------------------------

➢ [Questions]{.underline}:

-   Q: Which mechanism can be used to ensure perfect forward secrecy
    > (*PFS*) during key exchange when using Symmetric Encryption? →
    > **ECDH** (*Elliptic Curve DH*)

# \[11\] Secure Channel

+---+---------------------+--------------------------------------------+
| \ | NAME                | DESCRIPTION                                |
| # |                     |                                            |
+===+=====================+============================================+
| 1 | OCB                 | Fast, but patent issues.                   |
|   |                     |                                            |
|   | (Offset Codebook    |                                            |
|   | Mode)               |                                            |
+---+---------------------+--------------------------------------------+
| 2 | CCM                 | Slower than OCB but no known patent        |
|   |                     | issues.                                    |
|   | (Counter with       |                                            |
|   | CBC-MAC Mode)       |                                            |
+---+---------------------+--------------------------------------------+
| 3 | CWC                 | Speed improvement on CCM. No known patent  |
|   |                     | issues.                                    |
|   | (Carter-Wegman CTR  |                                            |
|   | Mode)               |                                            |
+---+---------------------+--------------------------------------------+
| 4 | GCM                 | NIST standard block cipher mode.           |
|   |                     | Improvement on CWC. No known patent        |
|   | (Galois Counter     | issues.                                    |
|   | Mode)               |                                            |
+---+---------------------+--------------------------------------------+

# \[12\] Random Number Generators

➢ **Random Number Generators**:

-   Table Lookup Generators

-   Hardware Generators

-   Algorithmic (Software) Generators

➢ **Algorithmic Pseudo-Random Number Generators**:

1.  [Linear Congruential Generators]{.underline} → The algorithm is:
    > Xn+1=(aXn+c) Mod m where n\>0

2.  [Lagged Fibonacci Generator]{.underline} (LFG) → formula: y=
    > Xk+Xj+1. can be Additive LFG, Multiplicative LFG or Two-tap LFG.

3.  [Blum Blum Shub]{.underline} → The algorithm is: Xn+1=Xn2 Mod m

4.  [Yarrow]{.underline} → By Bruce Schneider, john Kesley & Niels
    > Ferguson, supplanted by Fortuna

5.  [Fortuna]{.underline} → Group of PRNGs. 3 main components:
    > generator, entropy accumulator and seed file.

# \[13\] Formulas

+---+-------------------+----------------------------------------------+
| \ | NAME              | DESCRIPTION                                  |
| # |                   |                                              |
+===+===================+==============================================+
| 1 | RSA               | \- Relationship w/ prime numbers; Security   |
|   |                   | derives from large prime numbers.            |
|   |                   |                                              |
|   |                   | encryption: C = Me(%n)                       |
|   |                   |                                              |
|   |                   | decryption: P = Cd(%n)                       |
+---+-------------------+----------------------------------------------+
| 2 | Symmetric         | encryption: C = E(k,p) \[Ciphertext =        |
|   | Encryption        | EncryptionFunction (key, plaintext)          |
|   |                   |                                              |
|   |                   | decryption: P = E(k,c) \[Plaintext =         |
|   |                   | EncryptionFunction (key, ciphertext)         |
+---+-------------------+----------------------------------------------+
| 3 | EC (Elliptic      | y2 = (x3 + Ax + B)                           |
|   | Curve)            |                                              |
+---+-------------------+----------------------------------------------+
