**Sicherheit** heißt beide Safety und Security auf Englisch:
- Safety: gegenüber Fehlern
- Security: gegenüber böswilligen Handlungen

Es gibt 5 **Sicherheiteigenschaften** (erweitert):
1. Vertrauenlichkeit von Daten/Nachrichten
2. Integrität von Daten/Berechnungen
3. Verfügbarkeit von Dienst
   (CIA-Triade)
5. Authentizität von Dateien
6. Anonymität von Benutzern
   
Kryptographie liefert 3 **Ziele**:
1. Vertraulichkeit: Angerifer kann Inhalt der Nachrichten nicht lernen
2. Integrität: Angreifer kann Nachricht nicht ändern, ohne die Änderung bekannt wird
3. Authentizität: Angreifer kann nicht bahaupten, dass eine Nachricht von jemand kam, die diese nicht gesendet hat

Es gibt 2 Arten von Kryptographie: Symmetrie (gleicher Schlüssel zum Ver- und Entschlüsseln) und Asymmetrie (2 Schlüssel zum Ver- und Entschlüsseln).

**Kerckhoffs´Prinzip**: ein Kryptosystem muss selbst dann sicher sein, wenn alles daran öffentlich bekannt ist -außer dem Schlüssel.

Es gibt auch 2 Arten von Schiffren: **klassische** Chiffren (bsp. Shift-Chiffre: Caesars Chiffre, Substitutionschiffre, Vigenere-chiffre, OTP) und **moderne** Chiffren. Moderne Chiffre enthält 3 zu merkende Dinge: Formale Definitionen, systematisches Design, und sehr sichere kryptographische Konstruktionen mit Sicherheitsbeweisen (beim Sicherheitsbeweis gibt ansonsten kryptographische Annahme: wäre Annahme falsch, wäre Verfahren nicht mehr sicher).

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
- Ciphertextslänge c= 64 Bits
- Hauptschwachpunkt: kurzer Schlüsssel

**Triple DES**
- Schlüssellänge: 3*56= 168 Bits

<img width="610" height="70" alt="Bildschirmfoto 2025-10-07 um 14 15 38" src="https://github.com/user-attachments/assets/c481110b-55c0-44cc-945a-62e95857bc89" />
- angreifbar mit MitM Angriff.

**Advanced Encryption Standard (AES)**
 - Schlüssellänge: 128, 192 oder 256 Bits
 - Block-Größe: 128 Bits
 - ist mit Seiten-Kanal-Angriffe oder Fehleerangriffe angreifbar.
  
- Probleme von Blockschiffren:
  + Nicht IND-CPA sicher, weil es deterministisch ist
  + Nicht möglich Nachrichten beliebiger Länge zu verschlüsseln

  
### Modes of Operation
**Electronic Code Book (ECB) Modus**

<img width="370" height="273" alt="Bildschirmfoto 2025-10-06 um 21 33 11" src="https://github.com/user-attachments/assets/19370868-6fb7-4a9b-be48-7d88b2212405" />

- Der Klartext muss um ein Padding eingefügt werden, wenn |m| kein Vielfaches der Blocklänge ist
- Dieses Modus ist deterministisch

**Cipher Block Chaining (CBC) Modus**

<img width="545" height="252" alt="Bildschirmfoto 2025-10-06 um 21 41 01" src="https://github.com/user-attachments/assets/1a67ac63-42f3-4923-b7fd-f71abdd309e6" />
<img width="545" height="253" alt="Bildschirmfoto 2025-10-06 um 21 40 06" src="https://github.com/user-attachments/assets/3b4bfe0b-3291-47b5-b880-587670711b3b" />

- CBC ist IND-CPA sicher, aber es gibt Probleme mit Padding sind häufig in der Praxis. So was ist **Padding Angriffe** auf CBC? Annahme: Angreifer hat Chiffretext und Zugriff auf Padding Orakel, hat aber keine Ahnung über Klartext und Schlüssel; ansonsten muss der Webserver ein überprüfbares Padding Schema (PKSC#7) verwenden. Schritte von Angreifer: Angreifer ändert Chiffretext Block 1 so lange, bis gültiges Padding entsteht mithilfe von Fehlermeldungen oder side-channel Messungen, weiter mit andere Blocks wird Angreifer ursprünglichen Klartext rekonstruieren können.

**Counter Modus (CTR)** 

<img width="541" height="257" alt="Bildschirmfoto 2025-10-07 um 10 53 53" src="https://github.com/user-attachments/assets/ef318ba2-ac8b-4ea3-bd4a-108dff4852ab" />

<img width="539" height="247" alt="Bildschirmfoto 2025-10-07 um 10 55 29" src="https://github.com/user-attachments/assets/ff798999-8976-4fa0-8841-f81628158493" />

- Nonce kommt aus einer randomisierte Zählfunktion, was einen Zufallswert (Nonce) und eine natürliche Zahl (Counter) auf eine Bitkette fester Länge an. Eine einfache Implementierung benutzt die Binärdarstellung der natürlich Zahl mit 0-Padding (LSB- oder MSB-Kodierung). **Problem** ist, dass ein randomisierter Zähler kann nie injektiv sein, so soll man die Periode so lang wie möglich wählen.
  
- Die Länge von der Kombination von Nonce und Counter hängt von der Größe des Blocks. diese Länge definiert den maximale Werte von Nonce und Counter.
  
- **Nonce vs. IV**: Nonce wird benutzt, da CTR nur Einzigartigkeit benögtigt, Nonce kann auch deterministisch sein (-> uniqueness matters), aber IV betonnt auch die Unvorhersagbarkeit (-> unpredicablity matters). So Nonce verhindert die Wiederverwendung von Schlüsselströmen, während IV das Durchsickern von Informationen aus gewähltern Klartext verhindert.
  
---

**Kryptographische Hashfunktionen** $H: \ {0,1\}^\* \to \{0,1\}^n$
- Eingabe: Nachricht beliebiger Länge
- Ausgabe: fixe Länge
- 3 Sicherheitsdefinitionen:
  + Preimage resistance: gegeben h ist es schwer m zu finden, so dass H(m) = h
  + Second Preimage resistance: gegeben m ist es schwer m´ ≠ m zu finden, so dass h := H(m) = H(m´)
  + Collision resistance: es ist schwer, m und m´ zu finden, so dass h := H(m) = H(m´)
 
### Message Authentication Codes (MACs)
- Für Erhaltung Integrität und Authentifizität der Nachricht
- Algorithmen: (Gen, Mac, Vrfy)

   <img width="480" height="85" alt="Bildschirmfoto 2025-10-07 um 14 44 57" src="https://github.com/user-attachments/assets/3368d58e-15f5-4168-8562-8bcd25d2c91e" />

**CBC-MAC**

<img width="386" height="169" alt="Bildschirmfoto 2025-10-07 um 14 46 42" src="https://github.com/user-attachments/assets/5a14d656-cc3a-4ea1-ad13-36b37bd92b93" />

und mit Nachricht unterschiedlicher Länge, aber es ist nicht sicher, beispielweise sei MAC(M) = t und MAC(B) = s, so die neue Nachricht M´ = M || (t ⊕ B) hat den gültigen Tag s.

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
- Der Paar (pk, sk) ermöglicht auch **Mehrfachauthentifizierung**: einmalig Schlüssel authentisieren => anschließend beliebig viele Nachrichten signiert prüfen.
  + Algorithmen: (Gen, Sig, Ver)
    <img width="595" height="182" alt="Bildschirmfoto 2025-10-15 um 21 42 56" src="https://github.com/user-attachments/assets/f16ca8eb-2528-48a7-a0eb-d36b373673da" />
  + Sig(sk,m) hängt stark von Nachricht ab, so Angreifer kann keine Signeturen auf neue Nachricht fälschen.
 
Um die Authentizität und Integrität der Nachricht zu prüfen (Angreifer kann keine Signatur auf neue Nachricht fälschen), wenden **EUF-CMA** Sicherheitsspiel an

Bis jetzt kennen wir 3 Arten für Datenintegrität: Koolisions-resistente Hashfunktion, digitale Signaturen, MACs. Weiter werden wir uns mit **Signaturverfahren** beschäftigen. Es gibt 2 Arten von Signaturverfahren: **RSA-basierte Signaturen**, und **Diskreter-Logarithmus-basiert**; beide Verfahren folgen dem sogenannten *"Hash-and-Sign"-Prinzip*
- Hash-and-Sign-Prinzip ermöglicht das Signieren von beliebig langen Nachrichten, und Hashfunktion trägt zut Sicherheit des Verfahren bei.
  <img width="1322" height="474" alt="image" src="https://github.com/user-attachments/assets/b6e6eb51-cf32-4487-807c-f9ce0b63c565" />
1. RSA-basiert Signaturen:
   - RSA Signieren: hier wird sk = (N,d) verwendet
     1. Hashe Nachricht m auf H(m)
     2. Kodiere "kurzen" Hashwert auf RSA-Länge
     3. "Kern"-Signaturverfahren: wende RSA-Schlüssel $\{(·)\}^\{d\} mod N$ an
   - RSA Verifizieren: hier wird pk = (N,e) verwendet
     1. Hashe Nachricht m auf H(m)
     2. Kodiere "kurzen" Hashwert auf RSA-Länge
     3. Vergleiche Signatur $\{s\}^\{e\} mod N$ mit Encode(H(m))
<img width="433" height="210" alt="Bildschirmfoto 2025-10-17 um 02 43 05" src="https://github.com/user-attachments/assets/c72e5563-d6c0-43c0-a935-ec3344a8fbdf" />

2. Diskrete-Logarithmus-basiert Signaturen: hier betrachten wir **Schnorr-Signaturen**:
   - Setup:
     + Gruppe G zyklisch, Primordnung q, Generator g
     + Schlüssel: privat $\{x\} \in {1,...,q-1}$, öffentlich $\{y\} = \{g\}^\{x\}$
   - Signieren:
     1. Wähle *zufällige Nonce k* $\in {1,...,q-1}$
     2. $\{R\} = \{g\}^\{k\}$, Challenge r = H(R||m)
     3. s = k + r*x*(mod q)
     4. Signatur: (r,s)
   - Verifikation
     1. $\{R'\} = \{g\}^\{s\}*\{y\}^\{-r\}$
     2. v = H(R'||m)
     3. Ausgabe 1 iff v = r, sonst Ausgabe 0
    
**Zertifikate**
1. Zertifizierungshierarchie:
```mermaid
   flowchart TB
    root[Root-CA]
    inter[übergeordnete CA]
    ca[CA]
    holder[Schlüsselinhaber]

    root -->|Zertifiziert mittels Signatur| inter
    inter -->|Zertifiziert mittels Signatur| ca
    ca -->|Zertifiziert mittels Signatur| holder
```

2. Zertifikate revozieren
   1. Variante 1: Certificate Revocation Lists (CRLs)
      - Veröffentlicht unterschriebene Liste aller gesperrter Zertifikate
   2. Online Certificate Status Protocol (OCSP)
      - Benutzer fragt Gültigkeit eines bestimmten Zertifikats ab
      - Es gibt viele Vorteile:
        + Echtzeitabfrage
        + Kürzer & effizienter

Jetzt unterscheiden wir uns die folgenden Begriffe:
1. Identifizierung: Identität feststellen
2. Authentisierung: Identität bestätigen
3. Autorisierung: bestimmen, was gegenüber machen darf nach bestandener Kontrolle

## Authentisierung
### 3 Faktoren zur Authentisierung – Übersicht

| Faktor (Auth) | Beispiele | Vorteile | Nachteile |
|---|---|---|---|
| **Wissen - Was man weiß** | Passwort, PIN | einfach zu ändern; einfach mitnehmbar | kann vergessen werden; leicht zu duplizieren/phishen |
| **Besitz - Was man hat** | Chipkarte, Hardware-Token| einfach mitnehmbar; nicht leicht zu duplizieren | übertragbar/teilbar; leicht zu stehlen/verlieren |
| **biometrische Authentisierung - Was man ist** | Biometrie: Fingerabdruck, Gesicht| nicht übertragbar; individuell | oft (relativ) fälschbar; unveränderbar bei Leak; Datenschutz/Privacy-Probleme |

**Passwortspeicherung**
1. Naive: einfacher Abgleich mit im Klartext gespeicherten Passwörtern
2. Verschlüsselung: Speichere Passwärter verschlüsselt, Sever hat zusätzlich Schlüsselpaar (sk, pk). Hier sind die Einwegfunktionen benötigt.
3. Hashen: Speichere Passwörter als Hash
4. Rainbow Table: benutzen Hashfunktion H: Passwort -> Hash und Reduktionsfunktion R: Hash -> Passwort, um eine Kette für jede Passwörtern zu erstellen. Aber es Time-Memorz Tradeoff gibt: je länger die Ketten, desto weniger Speicherbedarf, aber desto mehr Zeitaufwand
5. Salted Hashing: wähle zufälligen Salt S, mit mindestens 64 Bits, speiche H(S||pwd) in Passwort.
6. Peppering: verhält wie Salted Hashing, aber Salt(s) geheim halten

**Tokens**
Es existiert 2 **Arten von Token**: *Software*- (bsp. Web-Cookies) und *Hardware*-Token (bsp. Autoschlüssel), ansonsten betrachten wir auch 2 **Eigenschaften von Token**: *statisch* (bsp. einfache Überstragung des Geheimnisses) und *dynamisch* (Berechnung mit Geheimnis zur Authentisierung). Mithilfe von dynamisches Token können wir **Replay-Angriffe** vorbeugen.

**Biometrische Authentisierung**
- Fehler:
  + Falsch positiv
  + Falsch negativ
- Probleme:
  + nicht widerrufbar
  + benötigt vertrauenswürdige Geräte vor Ort
  + oft leicht zu fälschen

**Single-Sign-On (SSO)**
- Vorteile:
  + Nur ein Passwort notwendig
  + Phishing-Attacken schwerer, da einzelne Login-Stelle leichter auf Korrektheit überprüft werden kann
  + IT-Sicherheitmaßnahmen fokussieren sich auf zentrale Stelle
 - Nachteil: Verfügbarkeit von Dienst hängt von Verfügbarkeit des SSO ab
 - Für Authentisierung des SSOs, wenden wir Kerberos Protokoll an.
   <img width="695" height="144" alt="Bildschirmfoto 2025-10-17 um 12 34 28" src="https://github.com/user-attachments/assets/0f4b5f7b-bd8b-4385-89a5-569348e38e78" />

## Autorisierung
- Autorisierung heißt, dass wir die Rechten für jemand auf jede Datei zuweisen werden (Zugriffkontrolle)
- Schutzziel: Integrität und Vertraulichkeit
- Es gibt 2 Arten der Autorisierung:
  1. Rechtfestsetzung:
     1. Discretionary Access Control (DAC): Eigentümer des Objekts legt Zugriffsrechte für Subjekte fest
     2. Mandatory Access Control (MAC): Autorität setzt Zugriffsrechte fest
  2. Granularität der Zuweisung:
     1. Role-based Acess Control (RBAC): Zugriffsrecht durch Rolle festgelegt 
     2. Attribute-based Access Control (ABAC): feinere Zugriffsrecht gemäß logischer Formel

Beisiele für **DAC**: 
1. Acces Matrix Model
<img width="714" height="159" alt="Bildschirmfoto 2025-10-17 um 12 42 03" src="https://github.com/user-attachments/assets/5b9a8df0-cdd6-48e7-a0a7-b8b0ae06a674" />
2. Acces Control List
   <img width="590" height="151" alt="Bildschirmfoto 2025-10-17 um 12 44 43" src="https://github.com/user-attachments/assets/ad05fa86-c941-4696-a1a2-2d60810f360d" />

Für **MAC** ist **Bell-LaPadula Modell** das klassische Modell mit Fokus auf Vertraulichkeit in Multi-Level Security. Dieses Model regelt die Informationsflüsse in eine Hierarchie: 
- No-Read-Up Regel: Lesezugriff (*read*) nur erlaubt wenn Hierarchie Subjekt ≥ Hierarchie Objekt
- No-Write-Down Regel: Erzeugung von Objekten (*append*) nur für Hierarchie ≥ Hierarchie des Subjekts
So muss jedem Subjekt eine Sicherheitsklasse $\{SC(s)\} \in \{SC\}$ zugewiesen (*Clearance*), und jedem Objekt wird eine Sicherheitsklasse $\{SC(o)\} \in \{SC\}$ zugewiesen (*Classification*)

### Netzwerksicherheit
**WLAN vs. WAN**
- Local Area Netzwerk (LAN): Menge an verknüpften lokalen Geräten, die miteinander kommunizieren können
- Wide Area Netz (WAN): Verbinden mehrer LAN mit Routern
  <img width="798" height="260" alt="Bildschirmfoto 2025-10-18 um 22 00 43" src="https://github.com/user-attachments/assets/bb4a12aa-5756-43bd-80d4-e40e33d1c7db" />

**Protokoll**: Vereinbarung wie einzelne Knoten im Netzwerk miteinander kommunizieren:
- Syntax: Wie ist die Kommunikation strukturiert und spezifiert
- Semantik: Bedeutung der Kommunikation

**Netwerk-schichtenmodelle**
1. OSI Modell: Kommunikation zwischen 2 OSI Modell:
<img width="687" height="323" alt="Bildschirmfoto 2025-10-19 um 13 14 54" src="https://github.com/user-attachments/assets/1cda487c-3b02-4908-9b8c-dac333ebb55e" />
2. TCP/IP Modell: Kommunikation zwischen 2 TCP/IP Modell:
   <img width="652" height="324" alt="Bildschirmfoto 2025-10-19 um 13 17 58" src="https://github.com/user-attachments/assets/4c7ada62-c844-4bb0-9c65-635ad4d493c5" />

### Protokolle auf jedem Layer
<img width="878" height="318" alt="Bildschirmfoto 2025-10-19 um 13 20 45" src="https://github.com/user-attachments/assets/84f61329-8c11-4d26-9ed3-d855abcec57c" />

1. Link Layer:
   - Bietet an: Übertragung zwischen 2 Punkten inklusive Konvertierung in physikalische Signale
   - Beispiele: Ethernet, WiFi, Address Resolution protocol (ARP)
   - Die kommunikation muss beinhalten: Senderadresse, Zieladresse, und Daten
   - Identifikation: mit **MAC Adressen**:
     + 6 Byte Adresse, die jedes netzwerkfähige Gerät im Internat besitzt
     + Weltweit eindeutige Adresse der Hardware (eindeutig pro Netwerkschnittstelle)
     + steht aus: OUI (erste 3 Bytes = Hersteller) + gerätespezifischer Teil (letzte 3 Bytes)
     + Beispiel: 13:37:ca:fe:f0:0d
   - Angriffe auf Link Layer:
     Nutzt die Wahrheit, dass manchen LANs Broadcast Kommunikation nutzen, der Angreifer kann zuhören mithilfe von Netzwerkkarte in ''promiscuous mode'', oder Analyse mit ''Paket Sniffer''. Ansonsten benutzt Link Layer MAC Adresse für Identifikation, führt dies zu einige Angriffstechniken:
     
     1. MACs als Zugrifftechniken: is kein Angriff, aber ein Schwach von Link Layer, weil MAC Adresse leicht spoofbar ist, ansonsten MAC Adrressen sind auch leicht per Software zu ändern
        
     2. MAC Flooding: is ein Angriff, bei dem der Angreifer den MAC-
Adressspeicher eines Switches mit vielen gefälschten Einträgen füllt. Ist die Tabelle überlaufen, kennt der Switch die echten Zuordnungen nicht mehr und floodet Frames an alle Ports - er verhält sich faktisch wie ein Hub

     3. ARP Spoofing /ARP Poisoning:
        - is nur möglich, wenn A ermittelt in *IPv4* zu einer bekannten IP-Adresse per ARP, da ARP keine Authentisierung besitzt, so A akzeptiert auch unangeforderte Antworten unf überschreiben ihre ARP-Cache
        - Nutzt die Wahrheit, dass wenn A eine Nachricht an B über LAN schicken möchte und nur B's IP Adresse kannt, dann A muss B's MAC Adresse lernen, um Link Layer Protokoll zu nutzen, das Protokoll werde beispielweise so aussieht:<img width="612" height="247" alt="Bildschirmfoto 2025-10-20 um 10 08 50" src="https://github.com/user-attachments/assets/d32800ce-f54a-4e47-9201-e1e65c9dc84b" />
        - Hier ist ein Angrifftechnik, dass der Angreifer die Identität einer anderen Partei vortäuscht, also um Datenverkehr anderer Nutzer über den eigenen Rechner zu leiten. Die Folgen von diesem sind, MitM und DoS Angriffe überführen zu lassen
        - Protokoll: A stellt die Anfrage via Broadcast, so Angreifer sendet daher gefälschte ARP-Replies, damit A die MAC Adresse von Angreifer in Cache speichern.
        - Gegenmaßnahmen:
          + durch Monitoring erkennen
          + Verschlüsselung des Datenverkehrs aufhöheren Schichten (IPSec, TLS) gegen MitM-Angriff
          + Nutzt stattdessen IPv6 für Neighbor Discovery Protocol (NDP)
    
      4. DHCP Spoofing (Dynamic Host Configuration Protocol Spoofing):
         - Obwohl DHCP das Protokoll von Applikation Layer: es nutzt UDP (Transport Layer) und initiale Broadcoasts laufen (Link Layer), aber dieser Angriff nutzt die Schwachstelle auf Link Layer ausnutzen: der Client muss zuerst via Broadcast Anfrage nach Konfiguration schicken, DHCP-Server kann Client ein Angebot für Konfiguration machen (bsw., IP-Adresse, Gateway, usw.) - hier kann auch Angreifer eigenes Angebot schicken, weiterhin wählt Client Angebot des Angreifers, denn er kann unehrliche/ehrliche Angebote nicht unterscheiden. Am Ende ausgewählter Server bestätigt Konfiguration.
         - Zusammenfassung: DHCP Spoofing ist der **Angriff auf Link Layer, der Auswirkungen auf den Internet Layer** hat: Der Angreifer gibt sich im Link Layer als DHCP-Server aus, wodurch Clients falsche IP-, Gateway- und DNS-Einstellungen (Internet Layer) erhalten.
         - Gegenmaßnahmen:
           + Monitoring, IDS
           + DHCP Snooping
           + Verwendung von Schutzmechanism aus höheren Ebenen

 2. Internet Layer:
    - Bietet an: Sendung von Paketen von jedem Quellgerät zu jedm Zielgerät
    - erlaubt die Kommunikation über verschiedene LANs hinweg mittels globaler Adressierung
    - Pakete beinhalten: Sender-, Zieladdresse, Daten; Pakete mitgleicher Sender-, Zieladdresse können unterschiedliche Routen nehmen
      **Internet Protocol (IP)**:
      - is die Protokoll zur Kommunikatio zwischen Geräten im Internet, hat eindeutige Identifikation von Geräten im Internet mittels **IP Adresse**
      1. IPv4: 32 Bit Adresse der Form: 120.19.22.00
      2. IPv6: 128 Bit Adresse der Form: 2607:f140:8801::1:23
      - Probleme von IP: is **unzuverlässig**:
        + Pakete können verloren gehen
        + Pakete können Fehler aufweisen
        + Pakete können in falscher Ordnung beim Empfänger eintreffen
    - **Internet Control Message Protocol** (ICMP): wird von Routern und Hosts verwendet, um Fehler- und Steuerungsnachrichten über den IP-Verkehr auszutauschen; er wird direkt über IP übertragen
      + **Ping of Death** bezeichnet ein absichtlich übergroßes (durch Fragmentierung) ICMP-Echo-Paket, das beim Reassemblieren das IP-Limit überschreitet und so Systeme zum Absturz bringen kann – es handelt sich nicht um normale Pings.
    
3. Transport Layer:
   - Bietet an: Ende-zu-Ende Kommunikation im Internet für verschiedene Dienste, ermöglicht unterschiedliche Anwendung auf einem Host durch **Ports** (120.19.22.00 **:443**)
   - Protokolle: TCP, UDP, und QUIC
     # TCP vs. UDP – Übersicht

| Protokoll | Verbindung | Zuverlässigkeit | Reihenfolge | Übertragung/Overhead | Kurzbeschreibung |
|---|---|---|---|---|---|
| **TCP** | Verbindungsorientiert (stellt Verbindung zwischen Endpunkten her) | **Zuverlässig** (korrekte Pakete werden bestätigt/neu gesendet) | **Geordnet** (Pakete kommen in korrekter Reihenfolge an) | **Langsamer** (mehr Kontrollmechanismen bsp. Handshake) | Für zuverlässige, geordnete Datenströme. |
| **UDP** | Verbindungslos | **Unzuverlässig** (keine Garantie für Zustellung) | **Ungeordnet** (keine Reihenfolge-Garantie) | **Schneller** (weniger Overhead) | Für einfache, latenzkritische Übertragungen. |
   - Eigenschaften von TCP:
     + TCP teilt beim Sender die Nachricht in kleinere Pakete auf und setzt diese beim Empfönger wieder zusammen
     + Verwendung von **Sequenznummern**, um Ordnung beim Empfänger wieder herzustellen; jeder TCP-Verbindung erfordert 2 Arten von Sequenznummnern: isn für Nachrichten vom Client an den Server (client_isn) und isn für Nachrichten vom Server an den Client (server_isn) und ISNs ist zufällig für jede neue Verbindung für Verhinderung von TCP hijacking)
     + Empfänger antwortet mit Empfangsbestätigung **ACK**. Wenn ACK nicht beim Sender eintrifft, sender das Paket erneut
     + Weiterhin gibt es ein kryptografisches Protokoll oberhalb von TCP: TLS (Transport Layer Security), das per Handshake Sitzungsschlüssel aushandelt und danach Anwendungsadten vertraulich und integritätgeschützt überträgt
     Datenübertragung mit TCP:
       <img width="636" height="292" alt="Bildschirmfoto 2025-10-25 um 22 28 52" src="https://github.com/user-attachments/assets/270876a6-a61b-4df9-8a26-c151faa7f07e" />
   - TCP Flags:
     1. ACK:
        + Indikator dafür, dass der Benutzer den Empfang von etwas bestätigt
     2. SYN:
        + Indikator für den Beginn der Verbindung
     3. FIN:
        + ist eine Möglichkeit, die Verbindung zu beenden
        + erfordert eine Bestätigung (ACK)
        + es werden keine Pakete mehr gesendet, aber weiterhin empfangen
     4. RST
        + ist eine öglichkeit, eine Verbindung zu beenden
        + erfordert keine Bestätigung (ACK)
        + es werden keine Pakete mehr gesendet und empfangen
   - Angriffe:
      1. TCP Hijacking: ist ein Angriff, darin Angreifer eine bestehende TCP Besitzung manipuliert (Daten ändern oder einschleusen); es geben 2 Arten:
         1. Dateninjektion: Spoofing von Datenpaketen, um schädliche Daten in eine Verbindung einzuschleusen. Für Spoofing muss Angreifer INS des Absender kennen. Normalerweise geben es 2 Arten von Angreifer:
            1. On-path-Angreifer: Verhältnismäßig einfach (Race-Condition)
            2. Off-Path-Angreifer: 32-Bit-ISN erraten
            - Gegenmaßnahmen:
              + Nutze Protokolle in höherer Schicht, um Angriffe zu verhindern
              + Zufällige Wahl der ISN schützt vor Off-Path Angreifer
         2. RST-Injektion: Spoofing eines RST-Pakets, um eine Verbindung zwangsweise zu beenden. Es wird manchmal von Zensur- oder Filter-Systeme benutzt; ein Dritter fälscht ein TCP-Segment mit RST-Flag, so beide Enpunkte glauben, der Peer habe die Verbindung zurückgestzt, führt dazu, dass Verbindung abbricht (DoS-Angriff)
       2. TCP Flooding: nutzt die Wahrheit aus, dass SYN Speicher nur beschränkte Anzahl an 'nicht abgeschlossenen' TCP Verbindung speichert; Angreifer sende viele SYN-Anfragen, ohne SYN-ACK mit ACK zu beantworten (DoS Angriff)
          - Gegenmaßnahme: SYN Cookies: Da man alle Werte aus später ampfangenen Werten extrahieren kann, bis auf SeqNr_S. so wir können TCP-Buffer erst an bei abgeschlossenem Handshake legen, dies macht den Angriff teuer; es gibt aber Problem, weil SeqNr_S nicht vorhersagbar sein darf. Aber wir können Speicher mit SYN-Cookie reservieren: $\mathrm{SeqNr\_S} := H(k_s,\ \mathrm{SeqNr\_C},\ \mathrm{IP\_C},\ \mathrm{Port\_C})$. So, nur wenn $\mathrm{SeqNr\_S} + 1 = H(k_s,\ \mathrm{SeqNr\_C},\ \mathrm{IP\_C},\\mathrm{Port\_C}) + 1,$ dann wird Speicher reserviert.

4.  Application Layer:
   - Bietet an: Funktion für netzbasierte Software; bsp. HTTP/HTTPS für Webseite, FTP für Filesharing, usw.
   - Adressierung der Anwendung mittels Ports
   - Protokolle:
     1. HTTP/HTTPS: Transport von Web-Inhalten
        + HTTP: über TCP 80, zustandlos
        + HTTPS: HTTP über TLS, meist TCP 443
     2. DNS/DNSSEC: Namensauflösung
        + DNS (Domain Name System): über UDP 53 für kleine Antworten, und über TCP 53 für großen Antworten
        + DNSSEC: Signiert DNS-Records für Integrität und Authentizität
     3. SMTP: E-Mail-Übertragung: über Ports 25 (Server nach Server), 587 (Submission mit STATTLS), und 465 (SMTPS/ TLS-wrapped)
   - Protokoll für Routing: Border Gateway Protokoll (BGP)
     + Jedes AS teilt seine aktuellen Routen mit seinen Nachbarn
     + Metrik für Paket Routing:
       1. Länge des Präfix
       2. Bei mehreren Routen zum selben Ziel wird die kürzeste Route gewählt
     + BGP Hijacking: Angreifer erstellt korrumpiertes AS, was macht falsche Angaben zur Erreichbarkeit von Netzen
        * Gegenmaßnahmen:
         1. Überwachung des Internetverkehrs
         2. RIR speichern wem welche Präfixe gehören
         3. Nutzen Resource Public Key Infrastructure (RPKI): Kryptographische Absicherung von BGP Bekanntmachungen
   - Hier werden wir genauer betrachten, was **TLS** ist:
     + TLS ist ein Sicherheitsprotokoll, das oberhalb von TCP arbeitet und oft als Teil der Anwendungsshicht betrachtet wird
     + Dies ermöglicht sichere Kommunikationskanäle für das Internet:
       * Vertraulichkeit: Angreifer kann Kommunikation nicht mitlesen
       * Integrität: Verhindert Abänderung der Kommunikation
       * Authentizität: Client komuniziert mit dem legitimen Server
     + Der Aufbau von TLS:
       * Handshake:
         + ist Aushandlung kryptographischer Verfahren/Parameter
         + Authentikation Etabilierung eines Sitzungsschlüssels k
         + geben es 3 Handshake-Familien:
           1. Ephemeral Diffie-Hellman (TLS-DHE)
           2. Static Diffie-Hellman (TLS-DH)
           3. RSA Verschlüsselung (TLS-RSA)
         + Beispiel für TLS-DHE Handshake (vereinfacht):
           <img width="738" height="317" alt="Bildschirmfoto 2025-10-27 um 15 15 26" src="https://github.com/user-attachments/assets/56aa6f8f-df38-493b-a425-2925d3ae726a" />
$\mathrm{fin}_C$ und $\mathrm{fin}_S$ wirken als Message Authentication Code (MAC), der die Integrität von übertragenen Daten schützt
       * Record Layer: Dateverschlüsselung und Authentifizierung mit Schlüssel k
         <img width="471" height="112" alt="Bildschirmfoto 2025-10-27 um 10 40 34" src="https://github.com/user-attachments/assets/fa06e7cb-0f3a-43e1-87ba-b3535a9c7131" />
      + Cipher Suites: gehören zu TLS, legen fest, mit welchen Algorihmen eine TLS-Verbindung arbeitet. Es gibt Unterschied unter die Versions von TLS,a aber allgemein bestimmt eine Cipher Suite: Schlüsselaustausch, Authentisierung/Signaturverfahren, Verschlüsselung, Integrität, Hashfunktion
   - DNS:
     + Schritte:
       - Rechner muss IP von Webseite suchen
       - DNS Server kennt entweder IP-Adresse oder fragt Root-Server zu zuständigem Name-Server
       - DNS Server antwortet den Rechner die IP-Adresse der Webseite
       - Rechner speichert IP-Adresse lokal
      + DNS Adress Records:
     
| Name | Type | Class | TTL | RDLength | RData |
|------|------|--------|-----|-----------|-------|
| Fully Qualified Domain Name | Datentypbezeichner | Klassenbezeichner | Time to Live – Verfallsdatum | Länge des Data-Felds in Bytes | Der im Record abgelegte Wert zum Schlüssel |<img width="786" height="263" alt="Bildschirmfoto 2025-11-10 um 23 09 45" src="https://github.com/user-attachments/assets/b848f5ca-e648-45ab-8ff5-92d821a0ebb7" />

   - DNSSEC:
     + bietet noch Integrität bei der Antwort an, damit Cache-Poisoning-Angriffe verhindert wird.
     + DNS über TLS? kann auch eine Möglichkeit sein, aber wir möchte DNS schnell und leicht, während TLS langsam ist, ansonsten hilft TLS nicht beim Caching (aber DNS-Rekord muss zwischengespeichert werden), und auch nicht gegen bösartifen Nameservern. So sichert TLS den Kommunikationskanal, aber ermöglicht nicht Vertrauenswürdigkeit der Daten zu prüfen.
     + DNS nutzt stattdessen
       1. Kryptographie um zu beweisen, dass zurückgegebenen Antworten korrekt sind (mit digitale Signaturen von Nameservern), und
       2. hierarchisches, verteiles Vertrauenssytem (bsp. Root-Nameserver) zur Identifikation, um vor bösartigem Nameserver zu schützen
   - TOR - The Onion Router:
     + ist ein Overlay/Anonymisierungsnetwerk auf Applikation Layer, das IP-Verbindung anonymisiert, indem der Client sein Traffic (IP-Pakete) durch mehrere Replay-Knoten (Entry - Middle - Exit) leitet
   - Angriffe: (1-5 sind auf TLS)
     1. Cipher Suite Rollback Angriff:
        + ein MiTM-Angreifer ändert die Liste der Cipher Suites in der ClientHello Nachricht
        + er löscht alle starken Cipher Suites, so muss der Server eine schwache Cipher Suite wählen
     2. ChangeCipherSpec Message Drop Angriff: grifft auf SSL 2.0 oder vorige Versionen an:
        + der MiTM-Angreifer fängt die ChangCipherSpec Nachrichten ab und verwirft sie, dann werden sie niemals auf verschlüsselte Übertragung umgeschltet, alle Daten werden dann im Klartext übertragen
     3. Version Rollback Angriff:
        + MiTM-Angreifer modifiziert die SSL 3.0 ClientHello Nachricht, sodass sie wie ein SSL 2.0 ClientHello aussieht. Dies zwingt den Server angreifbares SSL 2.0 zu benutzen
        + Gegenmaßnahmen: Im Padding bei RSA-Ciphersuites integriert der Client eine SSL-Versionsnummer, der Server wird dann prüfen, ob die Versionsnummer korrekt ist
     4. Bleichenbachers Angriff auf TLS-RSA
        - Ausnutzen die Fakt, dass TLS-RSA RSA-PKCS#1 v1.5 Encryption anwendet (vor TLS 1.3)
        - RSA-PKCS#1 v1.5 Encryption:
          1. Sei pre_master_secret (pms) ein Bit String (46 zufällige Bytes + 2 Buyte Versionsnr.
          2. m := pad(pms) := 0x00 || 0x02 || random || 0x00 || pms
          3. $c_{\text{PKCS}} \;=\; \text{Enc}_{\text{RSA}}(e,m) \;:=\; m^{e} \bmod n$
         <img width="604" height="295" alt="Bildschirmfoto 2025-10-27 um 16 17 36" src="https://github.com/user-attachments/assets/2584e764-7264-4258-ada6-757868052a1d" />
         Genauer: <img width="473" height="183" alt="Bildschirmfoto 2025-10-27 um 16 17 55" src="https://github.com/user-attachments/assets/9f8aa0eb-2ac7-4cd7-8574-9f0945b4405a" />
         
        - Gegenmaßnahmen: aber kann nicht ganz gegen anderen Angriffen
          + Wählen neues Premaster-Secret, wenn Padding von pms nicht korrekt
          + ein wenig mehr Zeit für Extra-Schritt (Constannt-Time Implementation)
      5. Der Crime Angriff: *C*ompression *R*atio *I*nfo-leak *M*ade *E*asy Angriff; ist der Angriff auf Verschlüsselung + Kompression, um HTTP Cookies aus dem Browser wobei Cookies für Webseiten dienne zu klauen. Genauer gesagt, CRIME ist ein seiteneffekt-/Compression-Oracle-Angriff auf Verbindungen, bei denen Daten vor der Verschlüsselung komprimiert werden; durch Beobachtung der verschlüsselten Payload-Länge kann ein Angreifer geheime Werte/Cookie rekonstruieren.
         - Voraussetzungen:
           1. Client greift auf unsichere Verbindung zu und macht Anfrage auf korrekter Webseiten
           2. Angreifer kann verschlüsselte Kommunikation abhören
           3. Compression vor Verschlüsselung ist aktiviert
         - Schritte:
           + Bösartiges Javascript zwingt das Opfer, zahlweiche Anfragen zu senden
           + Angreifer kontrolliert Teile der Anfragedaten
           + Angreifer beobachtet die Größe der komprimierten Anfragen, während der Veränderung des schickenden Text bis das verrateten Text zu Geheimnis passt (komprimierte Text wird kürzer)
           + Durch systematische Änderungen der gesendeten Daten und Beobachtung der Größe der komprimierten Anfrage kann der Angreifer auf den Wert des Cookies schließen
         - Gegenmaßnahme: TLS 1.3 oder höher (kein Kompression mehr)
      6. DNS Cache Poisoning & Spoofing:
         1. Cache Poisoning Angriff: Angerifer speichert bösartige DNS Records bei einem DNS Server
            - Cache des DNS Servers wird dann vergiftet durch
            - DNS nutzt UDO und keine Verifikation der Authentizität
          2. Cache Spoofing Angriff: ermöglicht durch Cache Poisoning Angriff: Anfragen an eine Domäne werden an die IP-Adresse des Angreifers weitergeleitet (da DNS Server falsche Daten speichert)
           - Gegenmaßnahmen:
             + Bailiwick-Überprüfung: der Resolver akzeptiert nur Records von Nameservern, die für angefragte Zone verantwortlich sind
             + DNSSEC
       7. DNS Reflection Angriff: ein Art von DDoS Angriff, macht Endsystem/Zwischensystemen überlastet
          - Funktionsweise:
            + Reflection: Angreifersysteme senden mit gespoofter Opfer-IP-Addresse DNS-Anfragen an Server
            + Amplification: Anworten von Server an Opfer sind deutlich größer als Anfragen
          - Gegenmaßnahmen:
            1. Opfer-seitig:
               - Kapazitätsreserven an Netz und Systemen bereitstellen
               - Filterung von gespooften IP-Paketen (aufwändig)
            2. Gegen Missbrauchter DNS-Dienst:
               - Minimierung der Antwortgröße, um Amplification-Fakto
               - Filterung von gespooften IP-Paketen
            3. Gegen den Angreifer:
               - Eliminierung von Paketen mit gespoofter IP-Adresse im Ursprungsnetzwerke
               - Stilllegung von Botnetzen
       9. DNS Tunneling:
          - verdecktes Übertragen von beliebigen Daten über DNS-Anfragen, damit die folgenden möglich werden:
            + Extraktion von ausspionierten Informationen aus einem kompromitierten Netzwerk
            + Umgehung von Netzsperren und Firewalls
            + Verdeckte Kommunikation von Bots mit ihrem Master
          - Funktionsweise:
            + Angreifer setzt autoritativen Server und Domain als Endpunkt auf
            + Client codiert Daten in angefragten Namen
            + Resolver leiten Daten an autoritaativen Server weiter
          - Gegenmaßnahme: Filtern durch Firewall mit statischer Anomaliedetektion oft möglich
         
### WLAN Sicherheit
- Typische Komponenten eines WLAN Netwerkes:
  + Access point: ein Gerät, das die Verbindung zum Netwerk ermöglicht
  + SSID - service set identifier: Name des WLAN Netwerkes
  + Password (optional): um Kommunikation abzusichern
- WLAN Verschlüsselung:
  1. Ziele:
     - Jeder mmit dem WLAN-Passwort kann dem Netzwerk beitreten
     - Ohne Kenntnis des Passworts können Nachrichten nicht mitgelesen werden
   2. Versionen von WLAN Verschlüsselung:
      1. WPA2:
         - verwendet AES
         - Angriffe:
           + Wörterbuchattacke
           + Rogue Access Point: Angreier kann sich selbst als Access Point ausgeben
           + KRACKATTACK: Fehler im Standard führt zum Resseten von kryptographischen Variablen bei Replay von Nachrichten
         - nutzt Handshake: damit Client und Access Point gemeinsame Schlüssel zum Schutz der Kommunikation anleitet
           
           <img width="277" height="427" alt="Bildschirmfoto 2025-11-12 um 04 42 04" src="https://github.com/user-attachments/assets/ad7ed1ff-2eb8-49cb-8c54-34f14023262a" />

           optimiert: WPA2 4-way Handshake:

           <img width="275" height="424" alt="Bildschirmfoto 2025-11-12 um 05 08 52" src="https://github.com/user-attachments/assets/b9c81d86-2c32-4df7-86ea-a1a61073a661" />
           
         - Angriffe auf Handshake:
           + Offline brute-force attack: nutzt einmaligen Mitschnitt von Kommunikation, um Sicherheit offline zu brechen (sichtbare Nonce mithören)
           + Rogue Access Point: Aangreifer gibt sich als Access Point aus, und führt das Handshake mit eigener Nonce durch: MitM-Angriff. Aber Angreifer braucht Kenntnis des Passworts.
      2. WPA3:
         - SEA (Simultaneous Authentication of Equals/Dragonfly) Schlüsselaustausch: ist DH-Schlüsselaustausch + Ableitung des Generators von Passwort. Es verhindert Offline Dictionary Attacks, und bietet Forward Secrecy, aber anfällig für ARP oder DHCP Spoofing
         -  Sicherheitsratschläge sind mit Vorsicht zu genießen:
           + Veränderung der IP-Adresse des Routers
           + Filterung von MAC-Adressen
           + Unterdrückung von SSID-Beacons
           + Einschränkung der Reichweite des WLANs
         - WPA3 Enterprise Version:
           + Client baut über Access Point Verbindung zu Authentifizierungsservice auf
           + Service authentifiziert sich über digitales Zertifikat
           + Client authentifiziert sich mit eigenem Username und Passwort
           + Service verteilt frischen one-time key
             
- Wardriving: ist das GPS-gestützte Aufspüren und Kartieren von WLANs durch passives/halb-aktives Scannen, ist primär zur Bestandsaufnahme, kann aber auch zur Angriffsvorbereitung missbraucht werden.

### Websicherheit
**Web**
- ist World Wide Web (WWW): eine Anwendung im Internet; eine Sammlung von Webservern, und daruaf zugegriffen mit Webbrowsern
- Bausteine des Webs:
  1. eindeutige Identifizierung von Daten und Dienste mit *Uniform Resource Locator (URL)*
  2. Kommunikation zwischen Browser und Server, um Daten auszutauschen: *Hypertext Transfer Protocol (HTTP)*
  3. Bestandteilen, daraus eine Webseite besteht:
     1. Hypertext Markup Language (HTML): ist Auszeichnungssprache, um statische Webseiten zu erstellen
     2. Cascading Style Sheets (CSS): Stylesheet-Sprache, um Aussehen einer Webseite zu definieren
     3. JavaScript (JS): Skriptsprache, die vom Browser ausgeführt wird und somit dynamische Webseite ermöglicht

**Bausteine des Webs**
1. URL
   - Grundlegender Aufbau: schema ":" schema-specifischer Teil
     + Beispiele für Schema: http(s), ftp, ssh, usw.: hilft uns dabei, mit welchem benutzten Protokoll im Internet für Kommunikation zu definieren
     + schema-spezifischer Teil: `//{<user>:<password>@}<host>{:<port>}{/<path>}{?<query>}{#<fragment>}:`:
       1. Beutzername und Passwort: für Basic Authetifizierung
       2. Domain: definiert welcher Webserver kontaktiert werden soll
       3. Port: Specifizierung einer Anwendung auf dem Webserver (bsp. 8080 für HTTP, 443 für HTTPS, 21 für FTP)
       4. Pfad: definiert welche Datei vom Webserver geladen werden soll
       5. Abfrage: zusätzliche Informationen an den Server, dir dort versrbeitet werden können
       6. Fragment: wird von Browser verwendet, um an Stelle auf Seite zu scrollen
   
   - URL-Encoding: ist eine Transport-Kodierung, keine Sicherheitsmaßnahme, damit es sichergestellt wird, dass URLs technisch korrekt, eindeutig und kompatibel bleiben

2. HTTP
   - ist ein Protokoll, um Daten an Server zu schicken und von Server zu Empfangen
   - baut auf Anfrage-Antwort Prinzip auf
   - Fortschritt: HTTPS: ist sichere Variante von HTTP, nutzt Verschlüsselung der Daten mittels TLS
   
   Beispiel für HTTP Anfrage und HTTP Antwort:
   
   Anfrage: 
   <img width="400" height="250" alt="Bildschirmfoto 2025-11-16 um 00 59 34" src="https://github.com/user-attachments/assets/d8471bfc-4324-4f9a-b2e8-03f6e6b2e945" />
   
   Antwort: 
   <img width="370" height="220" alt="Bildschirmfoto 2025-11-16 um 01 28 00" src="https://github.com/user-attachments/assets/e451bc1a-f365-4f1a-939b-1bd31fcda123" />

**Bausteine einer Webseite** (HTML, CSS, JS)
1. HTML: ist eine Auszeichnungssprache, um strukturierte Dokumente zu erstellen
2. CSS : ist eine Style-sheet-Sprache, um das Aussehen/Design einer Webseite festzulegen
3. JS: ist Skriptsprache, die für dynamische Webseiten entwickelt wurde
   - Eingebettet in HTML-Seiten
   - Kann den Inhalt der Seiten verändern, neue Inhalte laden
   - wird im Browser des Clients ausgeführt

Jetzt wissen wir, wie der Browser JS ausführt, JS bringt auch einige Sicherheitsrisiken im Web mit:
1. Angriffe auf den Webserver
2. Böse Webseite darf deinen PC nicht kaputt machen
3. Böse Webseite darf nicht mit anderen Webseiten interagieren

Für Risiko 3 braucht der Browser eine Regel: "JS von einer Seite darf nicht einfach Daten von andren Seiten lesen", was auch "Same-Origin Policy" gennannt wird. Als Folgende lernen wir kennen, was Same-Origin Policy ist.

**Same-Origin Policy**
- Origin setzt sich zusammen aus: Protokoll, Domain, und Port (aus URL)
- 2 Webseiten haben die gleiche Origin, falls alle 3 Elemente übereinstimmen.
- Regel: JS auf eine Webseite darf nicht Dokumente mit andere Origin zugreifen

Wie wir wissen, dass HTTP zustandlos ist (es ist nur ein Anfrage-Antwort Protokoll, und Server behandelt jede Anfrage unabhängig), aber Webseiten brauchen Zustand (bsp. **Session-Token** für Login, Warenkorb, Sprache, usw.). Aus diesem Grund brauchen wir Cookies

**Cookies**
- enthält Daten, um Zustand über mehrere Anfragen zu erhalten, zum Beispiel:
  + Daten werden als Name-Wert-Paar gespeichert
  + Cookie nur über HTTPS schicken, oder auch HTTP möglich
  + wann Cookie zu Anfrage hinzugefügt wird
  + Ob JS verbieten auf den Cookie zuzugreifen
  + Ab wann ist der Cookie nicht mehr gültig
Beispiel:
<img width="252" height="191" alt="Bildschirmfoto 2025-11-16 um 15 42 44" src="https://github.com/user-attachments/assets/77d944bf-c9c7-454b-b24b-6259502eacf8" />

- Erstellung eines Cookies:
  + Server kann in HTTP Response den Header "set-cookie" setzen
  + JS kann Cookie erzeugen
  + Manuelle Erzeugung im Browser ist möglich
- Speicherung eines Cookies: Browser speichert die Cookies
- Senden eines Cookies:
  + Browser fügt Cookies automatisch zu jeder Anfrage an die entsprechende Domain hinzu
  + Server kann gesendete Informationen dann verarbeiten und nutzen
 
Ablauf der Sendung eines Cookies:
<img width="575" height="258" alt="Bildschirmfoto 2025-11-16 um 15 18 29" src="https://github.com/user-attachments/assets/4c6ea5a7-91eb-4f00-b2e8-98d79a7bcb72" />
- Sicherheitsrisiken:
  + Webserver darf nicht Cookies für andere Webser setzen
  + Cookies dürfen nicht an falsche Adressarten gesendet werden
- Cookie Policy: ist eine Menge an Regeln, die beanwortet:
  + Wenn Browser ein Cookie von Webserver empfängt, soll er es akzeptieren?
  + Wenn Browser eine Anfrage an Webseite stellt, soll er das Cookie mitsenden
Mit Cookie Policy and Same-Origin Policy bestimmen wir: wer Cookies setzen darf, wohin sie gesendet werden, und wer sie lesen darf

**Session Authentifizierung**
- Session Token:
  + wird von Server erstellt, wenn wir uns erstmal in einer Webseite einloggen
  + Websserver sendet Session Token, das in Cookie abgelegt wird
  + Bei jeder neuen Anfrage wird der Session Token mitgesendet
  + Nach log-out löschen Webserver und Client-Browser das Session Token
 
Um Sicherheit des Session Token zu gewahrleisten, muss Server Session Token zufällig wählen und sicher auf Server ablegen; ansonten muss Browser sicherstellen, das bösartige Webseite Session Token nicht lernen kann (beispieleweise Maßnahmen: durch Cookie Policy, Same-Origin Policy, oder Setzen des HttpOnly-Felds)

So zum Schluss wissen wir, dass ohne Cookies gibt es keine bequeme Sessions/Logins, und ohne Same-Origin & Cookie Policy könnte andere Seiten unsere Session klauen

Jetzt lernen wir kennen, wie Angreifer die Bausteine von dem Web und der Webseiten missbrauchen kann. Wir gewöhnen uns an *Cross-Site Request Forgery (CSRF)*, *Cross-Site Scripting (XSS)*, und *SQL Injection* an:

**CSRF**
- nutzt aus, dass Browser Cookies automatisch mitsendet
- Idee: Angreifer bringt ein eingeloggtes Opfer dazu, ungewollte Requests an eine Seite zu schicken. Browser hängt automatisch Cookies an, so wirkt es wie legitime Anfrage vom Opfer
- Typischer Ablauf: 
