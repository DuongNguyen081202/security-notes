Es gibt 3 Ziele der Kryptographie:
1. Vertraulichkeit: Angerifer kann Inhalt der Nachrichten nicht lernen
2. Integrität: Angreifer kann Nachricht nicht ändern, ohne die Änderung bekannt wird
3. Authentizität: Angreifer kann nicht bahaupten, dass eine Nachricht von jemand kam, die diese nicht gesendet hat

Es gibt 2 Arten von Kryptographie: Symmetrie (gleicher Schlüssel zum Ver- und Entschlüsseln) und Asymmetrie (2 Schlüssel zum Ver- und Entschlüsseln).

**Kerckhoffs´Prinzip**: ein Kryptosystem muss selbst dann sicher sein, wenn alles daran öffentlich bekannt ist -außer dem Schlüssel.

Es gibt auch 2 Arten von Schiffren: **klassische** Chiffren (bsp. Shift-Chiffre: Caesars Chiffre, Substitutionschiffre) und **moderne** Chiffren. Moderne Chiffre enthält 3 zu merkende Dinge: Formale Definitionen, systematisches Design, und sehr sichere kryptographische Konstruktionen mit Sicherheitsbeweisen (beim Sicherheitsbeweis gibt ansonsten kryptographische Annahme: wäre Annahme falsch, wäre Verfahren nicht mehr sicher).

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
- Algorithmen: (Gen, Enc, Dec)

<img width="586" height="109" alt="Bildschirmfoto 2025-10-07 um 14 17 00" src="https://github.com/user-attachments/assets/18b9a3d1-06f9-422a-8850-2fb72e37cf7d" />

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
- Enc(.) hier spielt die Rolle als PRP, so wir schätzen eine Blockschiffre stark oder nicht dadurch ein, ob Schlüsselraum groß genug oder nicht ist. Dies vorstellt uns auch die Sicherheit von Blockschiffre (Angreifer kann nicht zwischen Enc(.) und P(.) unterscheiden).

<img width="648" height="156" alt="Bildschirmfoto 2025-10-07 um 14 15 11" src="https://github.com/user-attachments/assets/f40499c1-899e-4104-9f1f-b229eb8fc96e" />

**Data Encryption Standard (DES)** 
- Blocklänge n= 64 Bits
- Schlüssellänge k= 56 Bits

**Triple DES**
- Schlüssellänge: 3*56= 168 Bits

<img width="610" height="70" alt="Bildschirmfoto 2025-10-07 um 14 15 38" src="https://github.com/user-attachments/assets/c481110b-55c0-44cc-945a-62e95857bc89" />

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

- CBC ist IND-CPA sicher, aber es gibt Probleme mit Padding sind häufig in der Praxis. So was ist **Padding Angriffe** auf CBC? Annahme: Angreifer hat Chiffretext und Zugriff auf Padding Orakel, hat aber keine Ahnungüber Klartext und Schlüssel. Schritte von Angreifer: Angreifer ändert Chiffretext Block 1 so lange, bis gültiges Padding entsteht, weiter mit andere Blocks wird Angreifer ursprünglichen Klartext rekonstruieren können.

**Counter Modus (CTR)** 

<img width="541" height="257" alt="Bildschirmfoto 2025-10-07 um 10 53 53" src="https://github.com/user-attachments/assets/ef318ba2-ac8b-4ea3-bd4a-108dff4852ab" />

<img width="539" height="247" alt="Bildschirmfoto 2025-10-07 um 10 55 29" src="https://github.com/user-attachments/assets/ff798999-8976-4fa0-8841-f81628158493" />

---

**Kryptographische Hashfunktionen** $H: \ {0,1\}^\* \to \{0,1\}^n$
- Eingabe: Nachricht beliebiger Länge
- Ausgabe: fixe Länge
- 3 Sicherheitsdefinitionen:
  + Preimage resistance: gegeben h ist es schwer m zu finden, so dass H(m) = h
  + Second Preimage resistance: gegeben m ist es schwer m´ ≠ m zu finden, so dass h := H(m) = H(m´)
  + Collision resistance: es ist schwer, m und m´ zu finden, so dass h := H(m) = H(m´)
 
### Message Authentication Codes (MACs)
- Für Erhaltung Integrität und Vertraulichkeit der Nachricht
- Algorithmen: (Gen, Mac, Vrfy)

   <img width="480" height="85" alt="Bildschirmfoto 2025-10-07 um 14 44 57" src="https://github.com/user-attachments/assets/3368d58e-15f5-4168-8562-8bcd25d2c91e" />

**CBC-MAC**

<img width="386" height="169" alt="Bildschirmfoto 2025-10-07 um 14 46 42" src="https://github.com/user-attachments/assets/5a14d656-cc3a-4ea1-ad13-36b37bd92b93" />

und mit Nachricht unterschiedlicher Länge, aber es ist nicht sicher, da der Tag für die modifizierte Nachricht berechnet werden kann:

<img width="548" height="173" alt="Bildschirmfoto 2025-10-07 um 14 48 11" src="https://github.com/user-attachments/assets/d0133b39-9acc-439b-9cd9-122da1ca955c" />

Wir anwenden stattdessen **HMAC** für die Nachrichten beliebiger Länge. die Schritte sind: 1. Berechne y = H(m) der langen Nachricht m mit Hilfe von hashfunktion; 2. Berechne MAC

**Authentifizierte Verschlüsselung** kombinieren Verschlüsselung und Integritätsschutz, um Ziele: Vertraulichkeit, Integrität, und Authentizität der Nachricht zu gewährleisten.
1. Encrypt-then-MAC
   1. Verschlüsseln: c= $\mathrm{Enc}_{k_E}(\text{nonce}, m)$ (nonce hier kann auch IV sein)
   2. Authentisieren: t= $\mathrm{MAC}_{k_M}(\text{AAD} || c)$
   - Sende: (nonce, c, t)
   - Empfang: Tag prüfen, und entschlüsseln nur bei Erfolg
   - Probleme: anfällig für Padding/Timing- Orakel in bestimmten Modi (TLS-CBC: Lucky-13, Padding-Orakel); IND-CCA sicher durch Authentifizierung
2. Mac-then-Encrypt:
   1. Authentisieren: t= $\mathrm{MAC}_{k_M}(\text{m})$
   2. Verschlüsseln: c= $\mathrm{Enc}_{k_E}(\text{nonce}, m||t)$
   - Sende: (nonce, c)
   - Empfang: Erst entschlüsseln, dann Tag prüfen

**Asysmmetrische Kryptographie**
- Es gibt stattdessen ein Schlüsselpaar (pk, sk), dies macht es möglich, dass kein Schlüsselaustausch notwendig ist, dies folgt auch, dass nur n Schlüsselpaare gebraucht sind, statt <sup>n(n-1)</sup>/<sub>2</sub>
- Algorithmen: (Gen, Enc, Dec)

<img width="585" height="127" alt="Bildschirmfoto 2025-10-12 um 02 37 43" src="https://github.com/user-attachments/assets/5065defd-1f10-4c18-9206-f1dff4a986e1" />

**RSA Verschlüsselung**
1. RSA Schlüsselerzeugung: GenRSA(n) mit Sicherheitsparameter n
   - Wähle 2 n-bit *Primzahlen* p, q mit p ≠ q
   - Berechne N= p*q
   - Wähle e> 1, sodass ggT(e, 𝝋(N)) = 1
   - Berechne d = $\{e\}^\{-1\}$ mod𝝋(N); 𝝋(N) =(p-1)(q-1)
   - Ausgabe: (N,e,d) = GenRSA(n)
     
   <img width="273" height="180" alt="Bildschirmfoto 2025-10-12 um 02 50 24" src="https://github.com/user-attachments/assets/9b6389df-14b0-45fe-ae6b-3c6e622eec64" />

2. RSA Annahmen:
   1. d ist benögtigt, um die Invertierung der RSA Funktion zu berechnen
   2. y ist zufällig in $\{Z\}^\{+\}_\{N\}$
   3. Gegebn (N, e, y) ist es schwierig x zu berechnen, so dass z ≡ $\{x\}^\{e\}$ mod N
- **Homomorphe Verschlüsselung**: Verschlüsselungsverfahren heißt (multiplikativ) homomorph, wenn $\mathrm{Enc}(\mathsf{pk}, m_0)\cdot \mathrm{Enc}(\mathsf{pk}, m_1)
= \mathrm{Enc}(\mathsf{pk}, m_0\cdot m_1).$
  - Textbuch RSA ist homomorph, da $(m_0^{\,e} \bmod N)\cdot (m_1^{\,e} \bmod N)
\equiv (m_0\cdot m_1)^{e} \pmod N.$
- Diese Verschlüsselung ist deterministisch, so damit Textbuch RSA nicht mehr deterministisch wird, tragen wir Zufälligkeit in Encoding-Schritt ein, und Format wird geprüft in Decoding-Schritt. Dies nennen wir **RSA OAEP**:

  <img width="552" height="275" alt="Bildschirmfoto 2025-10-12 um 19 44 58" src="https://github.com/user-attachments/assets/a9a4a87a-a586-4854-a2d5-26a00fbe5b0f" />

Denn Textbuch RSA ist fast immer unsicher in der Praxis, brauchen wir eine alternative Verschlüsselungsverfahren. Nächste betrachten wir das **Elgamal Verfahren**
- Diskrete Logarithmus Annahme:
  + Setup: zyklische Gruppe G der Ordnung q mit Generator g und q prim
  + Gegeben: *zufälliges* h ∈ G
  + Suche: x, sodass $\{g\}^\{x\}$ = h
  + Annahme: diskreten Logarithmus zu finden ist schwer für geeignete Gruppe G
  + Andere Varianten: **CDH- und DDH-Annahme**:
    1. CDH-Annahme: es ist schwer, $\{g\}^\{xy\}$ zu berechnen
    2. DDH-Annahme: es ist schwer, zu entscheiden, ob ein T aus $\{g\}^\{xy\}$ kommt oder zufällig ist
**Schlüsselaustausch**
1. Diffie-Hellman Schlüsselaustausch:
   <img width="651" height="272" alt="Bildschirmfoto 2025-10-15 um 10 07 24" src="https://github.com/user-attachments/assets/dc4b403c-4399-4ff3-b572-f05cff91ded7" />
   Zur Verbesserung der Praxistauglichkeit wird **hybride Verschlüsselung** eingesetzt: Sie kombiniert einen asymmetrischen Schlüsselaustausch (KEM) mit der effizienten symmetrischen Verschlüsselung der Daten (DEM).
   - Verschlüsselung: <img width="717" height="287" alt="Bildschirmfoto 2025-10-15 um 17 28 09" src="https://github.com/user-attachments/assets/2cec1d23-6f5a-4d2b-b299-59e5a8c7a796" />
  - Entschlüsselung: <img width="713" height="288" alt="Bildschirmfoto 2025-10-15 um 17 29 21" src="https://github.com/user-attachments/assets/9304def3-ccf6-48af-895b-1cda90e6dbc6" />

**Signaturen**
*Digitale Signaturen*
```mermaid
flowchart LR
    A[Geheimer Schlüssel sk] --> B[Sig]
    B --> C[Signatur]
    C --> D[Ver]
    E[Öffentlicher Schlüssel] --> D
    D --> F[1 = `akzeptieren` oder 0 = `verwerfen`]
```
- Der Paar (pk, sk) ermöglicht auch **Mehrfachauthentifizierung**: Empfänger bekommt einmal öffentlichen Schlüssel pk von Sender über einen authentifizierte Kanal, dann der Empfänger kann jedes Mal eine neue Signatur aus dem Sender mithilfe von demselben pk prüfen.
  + Algorithmen: (Gen, Sig, Ver)
    <img width="595" height="182" alt="Bildschirmfoto 2025-10-15 um 21 42 56" src="https://github.com/user-attachments/assets/f16ca8eb-2528-48a7-a0eb-d36b373673da" />
  + Sig(sk,m) hängt stark von Nachricht ab, so Angreifer kann keine Signeturen auf neue Nachricht fälschen.
 
Um die Authentizität und Integrität der Nachricht zu prüfen (Angreifer kann keine Signatur auf neue Nachricht fälschen), wenden **UEF-CMA** Sicherheitsspiel an
