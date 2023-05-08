---
marp: true
theme: default #uncover #gaia #default
paginate: true
headingDivider: true
footer: "HdM Stuttgart - Rechnernetze - Tutorium"
---

# Rechnernetze - Tutorium

# zu Kapitel 3

Link zu den Folien :arrow_down:
[GitHub Pages](https://uggah.github.io/Rechnernetze-Tutorium/)

---

<!--footer: "" -->

0. Ein kleines Quiz vorab
1. Was ist CSMA/CD und ist es fair?
2. Beschreibe, wie sich bei CSMA/CD-Ethernet Distanz, Paketlänge und Bitrate
   gegenseitig beeinflussen.
3. Wie wird die **_Taktsynchronisation_** zwischen zwei Stationen bei Ethernet gelöst?
4. Warum werden die Signale im Ethernet **_codiert_** übertragen?
5. An welchem Grundproblem leidet Gigabit-Ethernet und wie wird dieses Problem gelöst? Beschreibe die Folgen. Was versteht man unter **_Skew Delay_**?

---

6. Erläuter die Begriffe **_Flow Control_** und **_Link Aggregation_**.
7. Ethernet Frames (10 MBit/s Ethernet) sollen mit Hilfe eines Protokoll Sniffers (z.B. dem in der Vorlesung eingesetzten Kabelhai) _eingefangen_ und ausgewertet werden. Wie viele Rahmen pro Sekunde sind maximal zu erwarten? Berechne die Rahmenrate einer Station in Abhängigkeit von der Größe der Payload (kleinster und größter Wert der Payload-Länge). Berechne auch den eigentlichen Datendurchsatz (ab Layer 3).

---

# 0. Ein kleines Quiz vorab
## Für was stehen und für was sind die Abkürzungen zuständig?:

- ITU
- IEEE
- IETF
- RFC

---

- ITU: International Telecommunications Union
  - Standards für den Telekommunikationsbereich
- IEEE: Institute of Electrical and Elektronics Engineers
  - Normierungen und Standardisierungen für Übertragungstechniken und Protokolle
- IETF: Internet Engineering Task Force
  - eine Art Forum, Erstellung von Vorschlägen für Standardisierung
- RFC: Request for comment
  - Anfrage bei der IETF

---

# 1. Was ist CSMA/CD und ist es fair?

## Für was steht CSMA/CD?
## Wie funktioniert CSMA/CD?
## Ist CSMA/CD fair?
---

# Für was steht CSMA/CD?

---

## CS - Carrier Sense (Träger Zustandserkennung)

Jede Station prüft, ob das Medium frei ist

## MA - Multiple Access (Mehrfachzugriff)

Mehrere Stationen teilen sich das Medium

## CD - Collision Detection (Kollisionserkennung)

Wenn mehrere Stationen gleichzeitig senden, erkennen sie die Kollision

---

# Wie funktioniert CSMA/CD?

---

![bg 80% right](https://github.com/Uggah/Rechnernetze-Tutorium/blob/master/marp/images/03_csmacd.png?raw=true)

- Alle Komunikationspartner hören die Leitung ab
- Ist die Leitung frei kann gesendet werden
- Unterscheidet sich das Abgehörte Signal vom Gesendeten, gab es eine Kollision
- Alle Komunikationspartner warten eine zufällige Zeit und es geht von vorne los

---
# Ist CSMA/CD fair?
---

# Ja.

## Da niemand beim Senden bevorzugt wird.

---

## 2. Beschreibe, wie sich bei CSMA/CD-Ethernet Distanz, Paketlänge und Bitrate gegenseitig beeinflussen.

![bg 80% right](https://github.com/Uggah/Rechnernetze-Tutorium/blob/master/marp/images/03_csmacd.png?raw=true)

![80% left](https://github.com/Uggah/Rechnernetze-Tutorium/blob/master/marp/images/03_csmacd2.png?raw=true)

---

# 3. Wie wird die **_Taktsynchronisation_** zwischen zwei Stationen bei Ethernet gelöst?

---

# Präambel

- 7 Bytes
- dient der **_Takt Synchronisation_**
- alternierende Bitfolge _101010...1010_

# SFD (Start Frame Delimiter)

- 1 Byte
- auf diese folgt der Start Frame Delimiter (SFD) mit der Bitfolge _10101011_

Dann beginnt die MAC Adresse und somit der eigentliche Inhalt ...

---

# 4. Warum werden die Signale im Ethernet **_codiert_** übertragen?

---

# Codierte Übertragung

- Taktsynchronisation
- Vermeidung von großen Gleichstromanteil

![bg right:50% 90%](https://upload.wikimedia.org/wikipedia/commons/thumb/9/90/Manchester_encoding_both_conventions.svg/1024px-Manchester_encoding_both_conventions.svg.png)

Von Stefan Schmidt - Enhancement of Manchester Encoding, Gemeinfrei, https://commons.wikimedia.org/w/index.php?curid=1219799

---

# 5. An welchem Grundproblem leidet Gigabit-Ethernet und wie wird dieses Problem gelöst? Beschreibe die Folgen.

---

# Problem

- es lässt Half-Duplex Verbindungen zu, daher wird
- CSMA/CD benötigt und es ist eine
- sehr geringe Längenausdehnung möglich
  - Zeit verkürzt sich, in der man Kollisionen erkennen kann

---

# Lösung

- Carrier-Extension
- Frame Bursting
- 4 Aderpaare Vollduplex
- Signalcodierung (PAM-5)

---

## Carrier Extension zusammen mit ...

Frames die 64 Bytes (minimale Länge) lang sind, werden auf 512 Bytes erweitert. Bei 64 Bytes ist das Paket schon auf dem Medium und es kann keine Kollision mehr erkannt werden. Durch die Erweiterung sind Kollisionsdomänen Ausdehnungen auf 200 Meter möglich.

---

## ... Frame Bursting

Die Performance bei kleineren Datenpaketen wird durch die Carrier Extension verschlechtert. Um das zu kompensieren, können Server, Switches und andere Ethernet Segmente mehrere solcher kleiner Datenpakete schicken, damit die Bandbreite besser ausgenutzt wird.

---

## Adernpaare

2 adrig

> Coaxkabel Halbduplex Geschwindigkeit bis 10 Mbit/s
> Definierte Pausen bei CSMA/CD, jeder bekommt Zeit zum quatschen

4 adrig

> TP-Kabel Halb- / Vollduplex Geschwindigkeit bis 2x 100 Mbit/s
> Auf 4 Adern kann man getrennt in beide Richtungen alles abwickeln

8 adrig

> TP-Kabel Vollduplex Geschwindigkeit bis 2x 1000 Mbit/s und 2x 10.000 Mbit/s

Link zum nachlesen: http://www.elektronik-kompendium.de/sites/kom/0301281.htm

---

## PAM5 Signalcodierung

| Kombination | V / Doppelader |
| ----------- | -------------: |
| 000         |            0 V |
| 001         |          0,5 V |
| 010         |            1 V |
| 011         |         -0,5 V |
| 100         |            0 V |
| 101         |          0,5 V |
| 110         |           -1 V |
| 111         |        - 0,5 V |

![bg right:50% 90%](https://www.itwissen.info/lex-images/pam5-codierung-mit-vier-bitkombinationen.png)

---

# Was versteht man unter **_Skew Delay_**?

---

# Skew Delay

- geringer Längenunterschied der Adernpaare im Twisted Pair Kabel
- gute Kabel haben eine kleine Skew Delay
- erfordert sorgfältiges _crimpen_
- hohe Qualitätsanforderungen an den Hersteller

---

# 6. Erläuter die Begriffe **_Flow Control_** und **_Link Aggregation_**.

---

# Flow Control (Flusssteuerung)

---

# Flow Control (Flusssteuerung)

- Empfänger kann ein Pause Signal senden
  - falls der Sender zu viele Daten sendet
  - um einen Pufferüberlauf mit Datenverlust zu verhindern
- Verhinderung von Paketverlust
- Verhinderung von zu hoher Latenz

---

# Link Aggregation

---

# Link Aggregation

- fast mehrere parallele Verbindungen zu einer logischen Verbindung zusammen
- einfaches Mittel um die Bandbreite und somit Datenrate zu vervielfachen

## Vorteile

- Ausfallsicherheit
- Lastverteilung
- Geringerer Konfigurationsaufwand (zum Beispiel nur eine IP-Adresse)

---

# 7. Ethernet Frames (10 MBit/s Ethernet) sollen mit Hilfe eines Protokoll Sniffers (z.B. dem in der Vorlesung eingesetzten Kabelhai) _eingefangen_ und ausgewertet werden. Wie viele Rahmen pro Sekunde sind maximal zu erwarten? Berechne die Rahmenrate einer Station in Abhängigkeit von der Größe der Payload (kleinster und größter Wert der Payload-Länge). Berechne auch den eigentlichen Datendurchsatz (ab Layer 3).

---

# Paketlänge

## ${Umwandlung\:in\:Bit}$ = $\frac{10\:Mbit}{Sekunde}$ = $\frac{10.000.000\:Bit}{Sekunde}$

---

# Paketlänge (mit Präambel und Interframe Gap)

## ${Kleinster\: Payload}$ = $8 + 14 + 46 + 4 + 12$ = $84 \: byte$

## ${Größter\: Payload}$ = $8 + 14 + 1500 + 4 + 12$ = $1538 \: byte$

---

# Umwandlung der Paketlänge in Bit

## $84 \: byte * 8 = 672 \: bit$

## $1538 \: byte * 8 = 12304 \: bit$

---

# Rahmen pro Sekunde und Datendurchsatz bei 10 Mbit / Sekunde

## ${Kleinster\:Payload}$ = $\frac{10.000.000\:bit}{672\:bit}$ = $\frac{14.881\:Rahmen}{Sekunde}$

## ${Größter\:Payload}$ = $\frac{10.000.000\:bit}{12.304\:bit}$ = $\frac{813\:Rahmen}{Sekunde}$

---

# Datendurchsatz

## ${Kleinster\:Payload}$ = ${14.881 * 46\:byte}$ = $\frac{684.625\:byte}{Sekunde}$

## ${Größter\:Payload}$ = ${813 * 1500\:byte}$ = $\frac{1.219.500\:byte}{Sekunde}$

---

# Weitere Fragen?

Bitte per E-Mail an [kk172@hdm-stuttgart.de](mailto:kk172@hdm-stuttgart.de), [lg088@hdm-stuttgart.de](mailto:lg088@hdm-stuttgart.de). Wir beantworten die dann im kommenden Meeting ausführlich.

# Bis nächste Woche :smile:

> `git pull` nicht vergessen
