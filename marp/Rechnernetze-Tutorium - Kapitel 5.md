---
marp: true
theme: default #uncover #gaia #default
paginate: true
headingDivider: true
footer: "HdM Stuttgart - Rechnernetze - Tutorium | Copyright © Michael Vanhee"
auto-scaling: true
inlineSVG: true
---

# Rechnernetze - Tutorium

# zu Kapitel 5

Link zu den Folien :arrow_down:
[GitHub Pages](https://uggah.github.io/Rechnernetze-Tutorium/)

---

<!--footer: "" -->

1. Erläutere die Aufgaben und die Funktionsweise von ARP.
2. Wie wird in einem Netz mit Hilfe von ARP verhindert, dass versehentlich eine IP doppelt vergeben wird?
3. Beschreibe die VLAN-Idee. Welche Vor- und Nachteile siehst du bei den Einsatzmöglichkeiten? Was versteht man unter VLAN Tagging (802.1q)?
4. Wie bestimmt man die Broadcast Adresse eines IP Gerätes? Warum muss die Subnetz Maske im Internet nicht mit übertragen werden?
5. Erläutere NAT, PAT, Full Cone, Restricted Cone, Port Restricted Cone.

---

6. In welchen Fällen bereitet der Einsatz von NAT Probleme?
7. Berechne den brachliegenden Adressumfang der Class E. Warum werden Class E Adressen angesichts des massiven Adressmangels nicht als normale Adressen verwendet?
8. Wozu wurde CIDR und VLSM eingeführt und wie funktionieren beide Ansätze?
9. Was versteht man unter longest match routing?
10. Ein Unternehmen verfügt über die IP-Adresse 147.11.0.0/25. Folgende Subnetze werden benötigt: Ein Netz für 59 Rechner und zwei Netze mit je zwei verfügbaren IP Adressen für Punkt zu Punkt Verbindungen. Führe die Subnetzbildung so durch, dass die einzelnen Subnetze möglichst klein sind.

---

11. Ein Kunde eines ISP erhält 55 zusammenhängende Class C Adressen. Eine dieser Class C Adressen lautet 200.72.71.0.
    1. Wie lautet im optimalen Fall die CIDR Routing Anweisung im Router des ISP?
    2. Ein anderer Kunde des ISP soll aus diesem Bereich seine Wunschnetz IP 200.72.100.0 erhalten. Wie lautet die Routing Tabelle in diesem Fall?

---

12. Fasse die Routing Einträge für die nachfolgenden vier IP Adressen jeweils soweit wie möglich zusammen:

    1. 220.56.132/24
       220.56.133/24
       220.56.134/24
       220.56.135/24
    2. 220.56.146.0/24
       220.56.147.0/24
       220.56.148.0/24
       220.56.149.0/24

---

# IP Adressierung

- für die Kommunikation im Internet ist die MAC Adresse unverzichtbar
- in die Routingtabelle steht jedoch nur die IP Adresse
- IPs sind nicht Ortsgebunden, logische Abstraktion
  > UPDATE :exclamation:
  > natürlich sind offizielle IP Adressen von Unternehmen schon ortsansässig

## Wie erkundet dann ein IP Gerät die MAC Adresse des Empfängers?

- Statisch (dazu werden IP Adressen einer bestimmten MAC Adresse zugeordnet)
- Dynamisch (mit ARP)

---

# 1. Erläutere die Aufgaben und Funktionsweise von ARP.
## 1.1 Für Was steht ARP?
## 1.2 Wo kommt ARP zum Einsatz?
## 1.3 Wie funktioniert ARP?

---

# ARP - Address Resolution Protocol

- ermittelt anhand einer IP Adresse die dazugehörige MAC Adresse
- falls kein Eintrag in der ARP Tabelle vorhanden ist
  - wird ein Broadcast (FF-FF-FF-FF-FF-FF) an alle Teilnehmer gesendet
  - **ARP Request** mit MAC Adresse und IP Adresse des Hosts
  - bei übereinstimmender Adresse kommt ein **ARP Reply**

---

![bg fit](https://github.com/Uggah/Rechnernetze-Tutorium/blob/master/marp/images/05_kabelhai.png?raw=true)

---

# 2. Wie wird in einem Netz mit Hilfe von ARP verhindert, dass versehentlich eine IP doppelt vergeben wird?

---

# Gratuitous (unaufgefordertes) ARP

- Host sendet ARP Request an den Broadcast
  - bei dem er seine eigene IP als Quelle und Ziel einträgt
    :arrow_right: :exclamation: Es darf keine Antwort kommen:exclamation: - das passiert bsp. bei jedem Systemstart vom Betriebssystem

Bekommt der Host ein ARP Reply, ist die Adresse bereits vergeben. Bekommt er kein ARP Reply, war die Vergabe der IP Adresse erfolgreich.

---

# 3.

# Beschreibe die VLAN Idee.

# Welche Vor- und Nachteile siehst du bei den Einsatzmöglichkeiten?

# Was versteht man unter VLAN Tagging (802.1q)?

---

# VLAN Idee

- Organisationsstruktur kann abgebildet werden
  - Einkauf, Verkauf, Fertigung, Personal, Gäste, ..
- VLANs benötigen einen Router um Daten austauschen zu können
- somit können logische Gruppen innerhalb eines physikalischen Netzes voneinander getrennt werden

---

# Vorteile

- Performance
  - Priorisierung von bestimmten Diensten wie VoIP
- Sicherheit
  - das Teilnetz der Ideenfabrik kann vom öffentlichen Gäste Netz getrennt werden
- Netzmanagement Upgrade
  - logische Gruppen lassen sich flexibler verändern
- Orts- und Raumunabhängig
  - ein großes Entwicklerstudio in Montreal und Paris ist im VLAN XYZ und kann so leichter Daten austauschen
- Dienste
  - VoIP, Webserver, Games, ..

---

# Nachteile

- VLAN Switch ist teurer
- Ausfallsicherheit bei der Netzausdehnung eines VLANs über mehrere Switch
- zusätzliche Sicherheitsmaßnahmen notwendig
- größere VLANs erfordern kompetente Mitarbeiter, da sie unübersichtlich und schwer zu warten werden, wenn die dezentral organisiert sind

---

# VLAN kann auf verschiedene Arten zugewiesen werden

- Port
- MAC
- IP
- Policy

---

# VLAN Tagging (IEEE 802.1Q)

Dabei wird in den 4 Byte des Ethernet Frames die Information abgespeichert.

- ermöglicht das mehrere VLANs über einen Switch Port genutzt werden können
- zeigen die Zugehörigkeit des VLANs

---

# 4.

# Wie bestimmt man die Broadcast Adresse eines IP Gerätes?

# Warum muss die Subnetz Maske im Internet nicht mit übertragen werden?

---

# Broadcast Adresse bestimmen

- IP 192.168.5.232
- Netzmaske 255.255.255.248 (/29)

Die Broadcast Adresse bekommt man durch die `ODER (OR)` Verknüpfung von IP Adresse und invertierter Netzmaske.

---

|                                | erste 24 Bit | letzte 8 Bit |
| ------------------------------ | -----------: | -----------: |
| IP Adresse                     |   192.168.5. |     11101000 |
| :exclamation: + OR Verknüpfung |              |              |
| negierte Netzmaske             |       0.0.0. |     00000111 |
| =                              |   192.168.5. |     11101111 |
| Broadcast Adresse              |   192.168.5. |          239 |

## Broadcast Adresse <=> letzte Subnetzadresse
---

# Warum muss die Subnetz Maske im Internet nicht mit übertragen werden?

Die SN Maske des Ziels spielt schlicht und einfach keine Rolle für die Funktionsweise von IP

---

# 5. Erläutere

- NAT
- PAT
- Full Cone
- Restricted Cone
- Port Restricted Cone

---

# NAT - Network Address Translation

> UPDATE :exclamation:
>
> - Empfängeradresse ~~Absenderadresse~~ durch eine andere ersetzen
> - Änderungen im IP Header, dadurch ändert sich die Frame Check Sequence (FCS) auf Layer 2 .. eine Fehlerkorrektur auf, typisch mit Cyclic Redundancy Check (CRC 32 Bit)

- Nutzung privater Adresseräume (bsp. 192.168.0.0/16)
- Warum?
  - Sicherheit durch verstecken des internen Netz
  - mehrere Hosts können gleichzeitig eine Internetverbindung nutzen

---

# PAT - Port Adress Translation

Ähnlich wie bei NAT werden auch hier die privaten IP Adressen eines internen Netzwerks mithilfe von Port Nummern in die öffentliche IP Adresse ersetzt.

---

# Full Cone

- interne Adressen werden in externe Adressen und Ports übersetzt
- externe Clients können ohne Einschränkungen Verbindungen zu internen Clients aufbauen

---

# Restricted Cone

- interner Client muss mit dem externen Client eine Verbindung aufbauen, bevor der externe senden kann

---

# Port Restricted Cone

- zusätzlich zu Restricted Cone muss der externe Client auf dem gleichen Port senden, auf dem der Verbindungsaufbau statt gefunden hat.

---

# 6. In welchen Fällen bereitet der Einsatz von NAT Probleme?

---

# Probleme von NAT

> UPDATE :exclamation:

- manche Protokolle übertragen die IP Adresse im Payload
  - bsp. SIP und SDP
  - beide sind VoIP Protokolle

Du musst dir das so vorstellen. Das Telefon kennt zwar dir öffentliche IP Adresse vom VoIP Server, der Server kennt aber deine nicht. Denn im Payload steht bsp. 192.168.1.2 und die private IP Adresse ist von außen nicht erreichbar.

![bg right:33% fit](https://github.com/Uggah/Rechnernetze-Tutorium/blob/master/marp/images/05_sip.png?raw=true)

---

# 7.

# Berechne den brachliegenden Adressumfang der Class E.

# Warum werden Class E Adressen angesichts des massiven Adressmangels nicht als normale Adressen verwendet?

---

# Class E - Zusammenfassung und Berechnung

Start Adresse ist 240.0.0.0 (führende Bits 1111) und die letzte Adresse ist 255.255.255.255. Es gibt keine Subnetz Maske, es gibt keine CIDR Notation, usw.

- Brachliegende Adressen
  - $Class-E$ = $2^{28}$ = 268.435.456
  - $16 * 256 * 256 * 256$

---

# Warum werden Class E Adressen angesichts des massiven Adressmangels nicht als normale Adressen verwendet?

TCP/IP Stacks im Betriebssystem wurden von Anfang an so konfiguriert, dass sie den Adressraum nicht akzeptieren.

IPv6 wurde entwickelt und löst IPv4 ab. Das ändern des IPv4 TCP/IP Stacks wird nicht passieren, da alle IP Geräte neu konfiguriert werden müssten.

---

# 8. Wozu wurde CIDR und VLSM eingeführt und wie funktionieren beide Ansätze?

---

# CIDR - Classless Interdomain Routing / Supernetting

- :exclamation: Gegenteil von Subnetting
- mehrere Netze mit gleichem IP Adressenanteil werden zu einer Route zusammengefasst

## Vorteile

- Routing Tabellen werden reduziert
- Adressbereiche werden besser ausgenutzt

---

# eine Beispiel Notation hast du oben schon gesehen

- IP 192.168.5.232
- Netzmaske 255.255.255.248 (/29)

## entspricht **192.168.5.232 /29**

---

## Zu 10.10.1.32/27

### gehört 10.10.1.44

### aber nicht 10.10.1.90

Von IP_Address_Match.png: Baccala@freesoft.orgderivative work: Zapyon (talk) - IP_Address_Match.png, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=12768693

![bg right:60% fit](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/IP_Address_Match.svg/1920px-IP_Address_Match.svg.png)

---

# VLSM - Variable Length Subnet Masks

- ermöglicht maßgeschneiderte Subnetz Masken
- mehrere Subnetz Masken können dadurch ermöglicht werden
  :arrow_right: Verschachtelung von Adressblöcken

# Vorteile

- Routen im LAN werden zusammengefasst
- Routing Tabelle wird reduziert
- mehrere Teilnetze werden mit einem Eintrag zusammengefasst
  :arrow_right: Routen Aggregation

---

# VLSM Beispiel

> Aus dem Adressblock 10.1.0.0/16 wird für die Adressierung von Punkt-zu-Punkt-Netzen ein Subnetz 10.1.1.0/24 reserviert. Aus diesem wird dann für das erste Punkt-zu-Punkt-Netz das Subnetz 10.1.1.0/30, das zweite 10.1.1.4/30 etc. entnommen.

---

# Tipp zum üben:

Zum Beispiel hier: https://www.ww-a.de/eex-online/informatik.php bei Netzwerke auf CIDR und VLSM klicken. Es generiert dir Aufgaben, zeigt dir den Lösungsweg und die Lösung auf.

---

# VLSM Tabelle

| IPs Anzahl | 2^  | Subnetz Anzahl |     Subnetz     | Subnetz in Binär |  /  |
| :--------: | :-: | :------------: | :-------------: | :--------------: | :-: |
|    254     | 2^0 |       1        |  255.255.255.0  |  11.. 0000 0000  | /24 |
|    126     | 2^1 |       2        | 255.255.255.128 |  11.. 1000 0000  | /25 |
|     62     | 2^2 |       4        | 255.255.255.192 |  11.. 1100 0000  | /26 |
|     30     | 2^3 |       8        | 255.255.255.224 |  11.. 1110 0000  | /27 |
|     14     | 2^4 |       16       | 255.255.255.240 |  11.. 1111 0000  | /28 |
|     6      | 2^5 |       32       | 255.255.255.248 |  11.. 1111 1000  | /29 |
|     2      | 2^6 |       64       | 255.255.255.252 |  11.. 1111 1100  | /30 |

---

# 9. Was versteht man unter longest match routing?

---

# Longest Match Routing / Longest Prefix Match

Was muss man tun?

1. IP Adresse und Routing Einträge binär schreiben
2. IP Adresse mit dem Routing Eintrag vergleichen
   - :exclamation: Longest Prefix Match macht es klar, man sucht nach dem längsten übereinstimmenden Präfix
3. Ein Paket wird dann über diese Route weiter geleitet.

---

# Beispiel

> Woher kommt eigentlich das Wort?

---

# Die Routing Tabelle eines ISP umfasst unter anderem nachfolgende Einträge:

|   Route |              IP | 1. Byte | 2. Byte Binär | 3. Byte  | 4. Byte  |
| ------: | --------------: | ------: | :-----------: | :------: | :------: |
| Route 1 | 174.16.0.0 / 12 |     174 |   00010000    | 00000000 | 00000000 |
| Route 2 | 174.16.0.0 / 18 |     174 |   00010000    | 00000000 | 00000000 |
| Route 3 | 174.16.0.0 / 26 |     174 |   00010000    | 00000000 | 00000000 |
| Route 4 |     0.0.0.0 / 0 |       0 |   00000000    | 00000000 | 00000000 |

---

# An welches der vier Ziele wird ein Paket mit nachfolgender IP Adresse weiter geleitet?

|           IP | 1. Byte |  2. Byte |  3. Byte |  4. Byte |   / | Route |
| -----------: | ------: | -------: | -------: | -------: | --: | ----: |
|  174.16.0.10 |     174 | 00010000 | 00000000 | 00001010 | /28 |     ? |
| 174.18.54.89 |     174 | 00010010 | 00110110 | 01011001 | /14 |     ? |
| 174.16.35.27 |     174 | 00010000 | 00100011 | 00011011 | /18 |     ? |
| 174.34.56.63 |     174 | 00100010 | 00111000 | 00111111 | /10 |     ? |

---

# Lösung

| IP           | Route   |
| ------------ | ------- |
| 174.16.0.10  | Route 3 |
| 174.18.54.89 | Route 1 |
| 174.16.35.27 | Route 2 |
| 174.34.56.63 | Route 4 |

---

# 10. Ein Unternehmen verfügt über die IP-Adresse 147.11.0.0/25. Folgende Subnetze werden benötigt: Ein Netz für 59 Rechner und zwei Netze mit je zwei verfügbaren IP Adressen für Punkt zu Punkt Verbindungen. Führe die Subnetzbildung so durch, dass die einzelnen Subnetze möglichst klein sind.

---

# Subnetz Bildung

## IP 147.11.0.0 / 25

## Netzmaske 255.255.255.128 (/25)

| Netz | Anzahl IPs (+2) | 2^  | Anzahl Adressen |        Adress Raum        |  /  |
| :--: | :-------------: | :-: | :-------------: | :-----------------------: | :-: |
|  A   |     59 + 2      | 2^6 |       64        | 147.11.0.0 - 147.11.0.63  | /26 |
|  B   |      2 + 2      | 2^2 |        4        | 147.11.0.64 - 147.11.0.67 | /30 |
|  C   |      2 + 2      | 2^2 |        4        | 147.11.0.68 - 147.11.0.71 | /30 |

---

> Prüfungstipp, mach dir eine Tabelle.
> Kleine Auswahl an Links mit verschiedenen Tabellen:

- https://www.elektronik-kompendium.de/sites/net/0907201.htm
- https://www.tecchannel.de/a/grundlagen-zu-routing-und-subnetzbildung-teil-3,434977,6
- http://mywiki.ergun.de/index.php?title=IP-Adressen_Berechung_und_Subnetting

---

# 11. Ein Kunde eines ISP erhält 55 zusammenhängende Class C Adressen. Eine dieser Class C Adressen lautet 200.72.71.0.

# i. Wie lautet im optimalen Fall die CIDR Routing Anweisung im Router des ISP?

# ii. Ein anderer Kunde des ISP soll aus diesem Bereich seine Wunschnetz IP 200.72.100.0 erhalten. Wie lautet die Routing Tabelle in diesem Fall?

---

# i.

# Anleitung

---

1. 55 Adressen :arrow_right: 6 Bit (vom 3. Byte) :arrow_right: /18
2. gegebene Adresse 200.72.71.0 binär schreiben :arrow_right: "200.72.`01000111`.0"
3. Netz ID berechnen

|                                 | IP Byte 1,2 | IP Byte 3 binär | IP Byte 4 |
| ------------------------------- | ----------- | --------------- | --------- |
| IP Adresse                      | 200.72.     | 01000111        | .0        |
| :exclamation: + AND Verknüpfung |             |                 |           |
| /18                             | 255.255.    | 11000000        | .0        |
| Netz ID                         | 200.72.     | 01000000        | .0        |

4. Adressraum geht von 200.72.64.0 bis 200.72.127.0
5. Einsatz von Longest Match Routing

---

# ii.

# 200.72.100.0 /24

---

# 12. Fasse die Routing Einträge für die nachfolgenden vier IP Adressen jeweils soweit wie möglich zusammen:

i.
220.56.132/24, 220.56.133/24, 220.56.134/24, 220.56.135/24

ii.
220.56.146.0/24, 220.56.147.0/24, 220.56.148.0/24, 220.56.149.0/24

---

# Anleitung

1. Du schreibst die IP binär hin und schaust wie weit beide übereinstimmen.
   > Mach es dir einfach und lass den uninteressanten Teil weg.
2. Fasse die IPs zusammen
3. Den übereinstimmen Teil als neue IP notieren
4. Schrägstrichschreibweise anpassen

---

# i.

| IP            |           | 3. Byte  | Routing                      |
| ------------- | --------- | -------- | ---------------------------- |
| 220.56.132/24 | "220.56." | 10000100 |                              |
| 220.56.133/24 | "220.56." | 10000101 |                              |
| 220.56.134/24 | "220.56." | 10000110 |                              |
| 220.56.135/24 | "220.56." | 10000111 | :arrow_right: 220.56.132 /22 |

---

# ii.

| IP              |           | 3. Byte  | Routing                        |
| --------------- | --------- | -------- | ------------------------------ |
| 220.56.146.0/24 | "220.56." | 10010010 |                                |
| 220.56.147.0/24 | "220.56." | 10010011 |                                |
| 220.56.148.0/24 | "220.56." | 10010100 |                                |
| 220.56.149.0/24 | "220.56." | 10010101 | :arrow_right: 220.56.144.0 /21 |

---

# Weitere Fragen?

Bitte per E-Mail an [kk172@hdm-stuttgart.de](mailto:kk172@hdm-stuttgart.de), [lg088@hdm-stuttgart.de](mailto:lg088@hdm-stuttgart.de). Wir beantworten die dann im kommenden Meeting ausführlich.

# Bis nächste Woche :smile:

> `git pull` nicht vergessen
