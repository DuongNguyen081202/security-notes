Es gibt 3 Ziele der Kryptographie:
1. Vertraulichkeit: Angerifer kann Inhalt der Nachrichten nicht lernen
2. Integrität: Angreifer kann Nachricht nicht ändern, ohne die Änderung bekannt wird
3. Authentizität: Angreifer kann nicht bahaupten, dass eine Nachricht von jemand kam, die diese nicht gesendet hat

Es gibt 2 Arten von Kryptographie: Symmetrie (gleicher Schlüssel zum Ver- und Entschlüsseln) und Asymmetrie (2 Schlüssel zum Ver- und Entschlüsseln).

**Kerckhoffs´Prinzip**: ein Kryptosystem muss selbst dann sicher sein, wenn alles daran öffentlich bekannt ist -außer dem Schlüssel.

Es gibt auch 2 Arten von Schiffren: **klassische** Chiffren (bsp. Shift-Chiffre, Substitutionschiffre) und **moderne** Chiffren. Moderne Chiffre enthält 3 zu merkende Dinge: Formale Definitionen, systematisches Design, und sehr sichere kryptographische Konstruktionen mit Sicherheitsbeweisen (beim Sicherheitsbeweis gibt ansonsten kryptographische Annahme: wäre Annahme falsch, wäre Verfahren nicht mehr sicher).

### Kryptographische primitive

|                     | **Symmetrische Kryptoprimitive**                                   | **Asymmetrische Kryptoprimitive**               |
|---------------------|---------------------------------------------------------------------|--------------------------------------------------|
| **Vertraulichkeit** | <ul><li>Symmetrische Chiffren</li><li>Blockchiffren</li></ul>      | <ul><li>Public Key Encryption (PKE)</li></ul>   |
| **Integrität & Authentizität** | <ul><li>Message Authentication Codes (MAC)</li></ul>   | <ul><li>Digitale Signaturen</li></ul>           |

### Kryptographische Konstruktionen (Beispiele)

|                     | **Symmetrische Konstruktionen**                                   | **Asymmetrische Konstruktionen**                         |
|---------------------|-------------------------------------------------------------------|----------------------------------------------------------|
| **Vertraulichkeit** | <ul><li>One-Time Pad</li><li>DES (3DES), AES</li></ul>            | <ul><li>RSA Verschlüsselung</li><li>ElGamal Verschlüsselung</li></ul> |
| **Integrität & Authentizität** | <ul><li>CBC-MAC</li><li>HMAC</li></ul>                 | <ul><li>RSA Signaturen</li><li>Schnorr Signaturen</li></ul>          |

**Symmetrische Kryptographie**
```mermaid
%%{init: {"securityLevel":"loose","flowchart":{"htmlLabels":true}} }%%
flowchart LR
    A["Klartext <i style='color:#c00'>m</i>"] --> ENC["Verschlüsselung"]
    ENC --> Ctxt["Chiffretext <i style='color:#c00'>c</i>"]
    Ctxt --> DEC["Entschlüsselung"]
    DEC --> Mout["<i style='color:#c00'>m</i>"]

    Key[Gen] -->|"Geheimer Schlüssel <i style='color:#c00'>k</i>"| ENC
    Key -->|"Geheimer Schlüssel <i style='color:#c00'>k</i>"| DEC

    classDef box fill:#ffffff,stroke:#000,rx:6,ry:6,color:#111;
    class A,ENC,Ctxt,DEC,Mout,Key box;
    linkStyle default interpolate basis
```

**Sicherheitsspiel**
1. IND-CPA: Angreifer darf so viele Nachrichten verschlüsseln lassen, wie es will. Aber die Gewinnwahrscheinlichkeot des Angreifers liegt immer bei gegen <sup>1</sup>/<sub>2</sub>
- Gefahr: Chosen Ciphertext Angriff, bsp. Padding Orakel Angriff
2. IND-CCA: Angreifer bekommt Zugang zu Orakel, das ausgewählte Chiffretexte entschlüsseln kann. Aber die Gewinnwahrscheinlichkeot des Angreifers liegt immer bei gegen <sup>1</sup>/<sub>2</sub>

**One-Time-Pad (OTP)** kann auch Vernam Chiffre genannt werden
- OTP zur Verschlüsselung von Bitstrings der Länge n
- Formal definition:
  + Gen: Ausgabe zufälliger Schlüssel $k \overset{\mathrm{R}}{\gets} \{0,1\}^n$.
  + Enc: für m ∈ M: Ausgabe Enc(k, m) = k ⊕ m.
  + Dec: für c ∈ C: Ausgabe Dec(k, c) = k ⊕ c.
- Sicherheit: mit dem Annahme: Schlüssel darf nur einmal verwendet werden

### Blockschiffre
- Ver- und Entschlüsselung von Nachrichten/Chiffretextblöcken mit fixer Länge
- Blocklänge n =|m|=|c|: häufig 64-128 Bits
- Schlüssellänge k: häufig 128-256 Bits
```mermaid
flowchart LR

  %% --- Verschlüsselung ---
    M1["Nachricht M (n bits)"] --> E["Enc"]
    E --> C1["Chiffretext C (n bits)"]
    K1["Schlüssel K (k bits)"] --> E

  %% --- Entschlüsselung ---
    C2["Chiffretext C (n bits)"] --> D["Dec"]
    D --> M2["Nachricht M (n bits)"]
    K2["Schlüssel K (k bits)"] --> D
```

**Data Encryption Standard (DES)** 
- Blocklänge n= 64 Bits
- Schlüssellänge k= 56 Bits

**Triple DES**
- Schlüssellänge: 3*56= 168 Bits
```mermaid
flowchart LR
    direction TB
    D1[DES]
    K0[K0] --> D1

    direction TB
    D2[DES⁻¹]
    K1[K1] --> D2

    direction TB
    D3[DES]
    K2[K2] --> D3

  M["M ∈ {0,1}^64"] --> D1 --> D2 --> D3 --> C["C ∈ {0,1}^64"]
```
- This Modell kann mit MitM Angriff attackiert werden, oder mit Seite-Kanal-Angriffe und Fehlerangriffe.
- Probleme:
  + Nicht IND-CPA sicher
  + Nicht möglich Nachrichten beliebiger Länge zu verschlüsseln
 
### Modes of Operation
**Electronic Code Book (ECB) Modus**

<img width="370" height="273" alt="Bildschirmfoto 2025-10-06 um 21 33 11" src="https://github.com/user-attachments/assets/19370868-6fb7-4a9b-be48-7d88b2212405" />

- Der Klartext muss um ein Padding eingefügt werden, wenn |m| kein Vielfaches der Blocklänge ist
- Dieses Modus ist deterministisch


**Cipher Block Chaining (CBC) Modus**

<img width="545" height="252" alt="Bildschirmfoto 2025-10-06 um 21 41 01" src="https://github.com/user-attachments/assets/1a67ac63-42f3-4923-b7fd-f71abdd309e6" />
<img width="545" height="253" alt="Bildschirmfoto 2025-10-06 um 21 40 06" src="https://github.com/user-attachments/assets/3b4bfe0b-3291-47b5-b880-587670711b3b" />

- CBC ist IND-CPA sicher, aber es gibt Probleme mit Padding sind häufig in der Praxis. So was ist Padding Angriffe auf CBC? Annahme: Angreifer hat Chiffretext und Zugriff auf Padding Orakel, hat aber keine Ahnungüber Klartext und Schlüssel. Schritte von Angreifer: Angreifer ändert Chiffretext Block 1 so lange, bis gültiges Padding entsteht, weiter mit andere Blocks wird Angreifer ursprünglichen Klartext rekonstruieren können.

**Counter Modus (CTR)** 

<img width="541" height="257" alt="Bildschirmfoto 2025-10-07 um 10 53 53" src="https://github.com/user-attachments/assets/ef318ba2-ac8b-4ea3-bd4a-108dff4852ab" />

<img width="539" height="247" alt="Bildschirmfoto 2025-10-07 um 10 55 29" src="https://github.com/user-attachments/assets/ff798999-8976-4fa0-8841-f81628158493" />
