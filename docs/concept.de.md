---
title: asymtrack — Konzept v0.1
author: Egon Leitner
type: wissen
keywords: [asymtrack, Symptomtagebuch, ePRO, MDR, DiGA, Konzept]
status: entwurf
created: 2026-09-02
modified: 2026-09-02
frontmatter_version: 5
description: Deutsche Fassung der ersten Konzeptfassung für asymtrack, inklusive regulatorischer Abgrenzung, Evidenzlage und offener Entscheidungen.
---

# asymtrack — Konzept (v0.1)

> **Status:** erster Entwurf, 2026-09-02. Nichts davon ist entschieden. Der Technologie-Stack
> bleibt bewusst offen. Abschnitte mit *UNGEPRUEFT* enthalten Fremdzulieferung, die nicht
> gegen Primärquellen abgeglichen wurde.
> **Sprachfassungen:** Leitfassung ist [concept.md](concept.md) (englisch, gemäß
> Container-Regeln §4). Dieses Dokument ist die deutsche Übersetzung und wird mitgeführt.

## 1. Die Idee in einem Absatz

Ein Patient, oder ein noch nicht Patient, erfasst Symptome, Messwerte und das allgemeine
Befinden auf dem eigenen Handy oder Tablet. Die Aufzeichnung ist so strukturiert, dass sie
einem Arzt nützt. In einer späteren Stufe kann der Arzt dem Patienten ein Fragenset
mitgeben, das aus einer Diagnose oder einer Verdachtsdiagnose abgeleitet ist. Der Name ist
eine Zusammenziehung: **A**nother **Sym**ptom **Track**er.

## 2. Warum sich das lohnen könnte

- Symptomtagebücher sind in deutschen Leitlinien verankert. Der Kopfschmerzkalender steht in
  AWMF 030/057 und in der zugehörigen Patientenleitlinie, die Blutdruckselbstmessung ist in
  der NVL Hypertonie und in den ESC-Leitlinien etabliert.
- Die bestehenden Apps schneiden schlecht ab. Stiftung Warentest bewertete keine
  Kopfschmerz-App besser als „befriedigend" (bestes Ergebnis: 2,6 für M-sense und
  Kopfschmerzwissen). Hauptkritik waren die mangelnde Erhebung der Krankengeschichte und
  fehlende wissenschaftliche Nutzenbelege.
- Strukturierte Selbstdokumentation wirkt messbar auf den Versorgungsverlauf, auch dort, wo
  sie nicht auf die Sterblichkeit wirkt (siehe Abschnitt 3).

## 3. Evidenzlage, ehrlich benannt

| Behauptung | Sicherheit | Quelle |
|---|---|---|
| ePRO-Monitoring verbessert Symptomkontrolle und Lebensqualität und senkt Notaufnahmebesuche | hoch | PRO-TECT, sekundäre Endpunkte, HR 0,84 für die Zeit bis zum ersten Notaufnahmebesuch |
| ePRO-Monitoring verlängert das Überleben | **nicht belegt** | Basch et al. JAMA 2017 (monozentrisch, n=766) war positiv; PRO-TECT (52 Praxen, n=1191), auf Gesamtüberleben gepowert, war null: HR 0,99, 95% KI 0,83 bis 1,17, p=0,86 |
| Patientenschulung zur Selbstmessung verbessert Adhärenz und Blutdruckkontrolle | sehr geringe Aussagesicherheit | NVL Hypertonie: Evidenz mit unklarem oder hohem Verzerrungsrisiko |

**Folge für die Positionierung:** kein Überlebens- oder Outcome-Versprechen bewerben.
Beworben wird, was belegbar ist: bessere Dokumentation, bessere Gespräche, frühere Erkennung
von Medikamentenübergebrauch.

## 4. Die regulatorische Grenze, die entscheidende Leitplanke

Nach MDCG 2019-11 (Revision 1, Juni 2025) ist Software, die Informationen nur aufzeichnet,
speichert und anzeigt, in der Regel **kein** Medizinprodukt. Der Leitfaden nennt Tagebücher
zur Aufzeichnung von Insulindosen ausdrücklich als Beispiel. Ein medizinischer Zweck
entsteht, sobald die Software aus den Daten eine Bewertung ableitet. Die Klassifizierung
folgt dann Anhang VIII, Regel 11 MDR.

MDCG erlaubt ausdrücklich einen **modularen Ansatz**: Ein Produkt darf aus Medizinprodukt-
und Nicht-Medizinprodukt-Modulen bestehen.

Daraus ergibt sich eine klare Linie für das Projekt:

| Bleibt außerhalb der MDR | Kippt in die MDR |
|---|---|
| Patient erfasst frei gewählte Einträge | App leitet Risiko, Score oder Empfehlung ab |
| App zeigt und exportiert das Erfasste | App triagiert, alarmiert oder interpretiert |
| Arzt stellt ein Fragenset als freies Formular zusammen | Fragenset ist an eine Diagnose gebunden und das Ergebnis fließt in eine klinische Entscheidung |

Regime, die unabhängig vom MDR-Status gelten:

- **Art. 9 DSGVO** — Gesundheitsdaten, besondere Kategorie. Das risikoreichste Gut im Projekt.
- **EU AI Act** — nur relevant, wenn ein Modell an einer Bewertung mitwirkt. Wissensbasis
  liegt unter `50.20.40.EU-AI-Act`.
- **DiGA-Weg (§ 33a, § 139e SGB V)** — Erstattungspfad über den BfArM-Fast-Track, drei Monate
  nach vollständiger Einreichung, Risikoklassen I, IIa, IIb. Verlangt den Nachweis positiver
  Versorgungseffekte, die BSI-Zertifizierung nach TR-03161 ist seit 01.01.2025 verpflichtend.
  Ab 01.01.2026 sind mindestens 20 Prozent des dauerhaften Vergütungsbetrags
  erfolgsabhängig, die anwendungsbegleitende Erfolgsmessung (AbEM) startete am selben Datum.
  **Für jede frühe Version außerhalb des Scope.**

## 5. Interoperabilität: „dem Arzt dienlich" ist ein Integrationsproblem

Ärzte lesen keine Apps. Sie lesen ihr Primärsystem. Der Weg dorthin führt in Deutschland über
die ePA mit MIOs auf FHIR-Basis, seit ePA 3.0 gibt es neben dem dokumentenbasierten auch
einen datenbasierten Teil. Das erste MIO, der elektronische Medikationsplan, soll ab 2026
nutzbar sein. **Ein MIO für Symptomtagebücher existiert nicht.**

Praktische Folge: Eine v1 kann nicht integrieren. Der billigste ehrliche Kanal ist ein
Export, den der Patient zum Termin mitbringt, als PDF oder Ausdruck.

## 6. Offene Entscheidungen

1. **Produkt oder Fingerübung?** Ob damit eine Erlösabsicht verfolgt wird, ändert die Antwort
   auf fast alles Weitere.
2. **Eine Indikation oder indikationsoffen?** Indikationsoffen vervielfacht validierte
   Fragebogensätze, Fachgesellschaften und Wettbewerber. Empfehlung aus dem kritischen
   Durchgang: mit genau einer starten.
3. **Technologie-Stack.** Bewusst offen. Erwogene Optionen: PHP/SQLite-PWA nach dem
   bestehenden MioDato-Muster, lokal-first-PWA mit IndexedDB, native App.
4. **Bekommt der Arzt in v1 ein Konto?** Der kritische Durchgang sagt nein: Der Arzt ist nicht
   der Nutzer, sondern das Nadelöhr. Es gibt keine EBM-Ziffer dafür, ein Fragenset in einer
   App zuzuweisen.

## 7. Empfohlener Zuschnitt einer ersten Version

Abgeleitet aus Abschnitt 4 und 6, so gewählt, dass sie nachweisbar außerhalb der MDR bleibt:

- Eine Indikation.
- Nur patientenseitige Erfassung, kein Arzt-Konto.
- Kein Scoring, keine Interpretation, keine Empfehlung.
- Ausgabe ist ein Export, den der Patient zum Termin mitbringt.
- Die Daten bleiben auf dem Gerät, bis der Patient sie selbst exportiert.

## 8. Kandidaten-Indikationen, UNGEPRUEFT

Die folgende Liste stammt von einer anderen KI und ist als Roh-Input festgehalten. Sie wurde
nicht gegen Leitlinien, Marktdichte oder Datenkomplexität geprüft und ist **keine**
Priorisierung.

**Herz-Kreislauf und Stoffwechsel:** Diabetes mellitus (Typ 1 und 2), arterielle Hypertonie,
Herzinsuffizienz.

**Neurologie und Psychiatrie:** Migräne und chronischer Kopfschmerz, Epilepsie, Depression
und bipolare Störung.

**Atemwege:** Asthma bronchiale, COPD.

**Gastroenterologie und Allergologie:** Reizdarmsyndrom, chronisch-entzündliche
Darmerkrankungen (Morbus Crohn, Colitis ulcerosa), Lebensmittelallergien und
-unverträglichkeiten.

**Rheumatologie und chronische Schmerzen:** rheumatoide Arthritis, Fibromyalgie.

Bei der Recherche teilweise bestätigt: der Kopfschmerzkalender (AWMF 030/057, MOH-Leitlinie
DGN 2022, gültig bis 30.11.2026) und die Blutdruckselbstmessung (NVL Hypertonie, ESC). Alles
Übrige in dieser Liste bleibt ungeprüft.

## 9. Bekannte Wettbewerber

| Produkt | Indikation | Anmerkung |
|---|---|---|
| M-sense (Newsenselab, Berlin) | Migräne | Warentest 2,6, Testsieger; kostenlose Basis-Stufe, kostenpflichtige Therapiebegleitung |
| Migräne App (Schmerzklinik Kiel) | Migräne | mit der Schmerzklinik Kiel und der TK entwickelt, kostenlos |
| DMKG-App | Kopfschmerz | kostenlos, werbefrei, von der Fachgesellschaft selbst |
| Kopfschmerzwissen | Kopfschmerz | Warentest 2,6 |

Nicht recherchiert: Cara Care (Reizdarm) und Kalmeda (Tinnitus), beide DiGA.

## 10. Quellen

- MDCG 2019-11 Rev. 1, Qualifizierung und Klassifizierung von Software unter MDR und IVDR
- MDR Anhang VIII, Regel 11
- BfArM DiGA-Leitfaden v3.5, § 33a und § 139e SGB V, DiGAV
- Basch et al., JAMA 2017;318(2):197-198
- PRO-TECT, clusterrandomisierte Studie, Nature Medicine 2025
- Stiftung Warentest, Kopfschmerz- und Migräne-Apps
- AWMF 030/057 (Migräne), MOH-Leitlinie DGN 2022, NVL Hypertonie (AWMF nvl-009)
- KBV MIO und gematik INA, ePA 3.0 FHIR

## 11. Grenzen der Recherche

Cara Care und Kalmeda wurden nicht recherchiert. Die G-BA-DMP-Anforderungen zur Peak-Flow-
und Blutzucker-Selbstdokumentation wurden nicht gegen Primärquellen geprüft. TR-03161 und
die DiGAV-Details stützen sich ausschließlich auf Sekundärquellen.
