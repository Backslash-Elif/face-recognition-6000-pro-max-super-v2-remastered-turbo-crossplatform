# Projektdokumentation

Diese Dokumentation beschreibt Planung, Aufbau, Umsetzung, Tests und Reflexion des Projekts.  
Sie ist so strukturiert, dass eine aussenstehende Fachperson den Ablauf vollständig nachvollziehen kann.

---

# 1. Einleitung

Dieses Projekt wurde im Rahmen des Moduls 346 umgesetzt und behandelt die Entwicklung eines einfachen FaceRecognition-Services in der AWS-Cloud. Dabei wird ein Bild in einen S3-Bucket hochgeladen, automatisch durch eine Lambda-Funktion verarbeitet und mit Amazon Rekognition analysiert. Das Ergebnis – die erkannten Personen und deren Wahrscheinlichkeit – wird als JSON-Datei in einem zweiten Bucket gespeichert.

Ziel war es, eine funktionierende technische Lösung zu erstellen, die den gesamten Cloud-Ablauf demonstriert und gleichzeitig die Kriterien des Moduls erfüllt: eine klare Architektur, eine automatisierte Bereitstellung mittels Init-Script, eine korrekte Implementierung der Lambda-Funktion sowie aussagekräftige Tests mit Dokumentation.

---

# 2. Architektur und Konzept

In diesem Kapitel wird das technische Konzept erläutert.  
Die eingesetzten Komponenten werden erklärt und unser Zusammenspiel dargestellt.

## 2.1 Systemübersicht

flowchart LR
    A[Input S3 Bucket<br>Upload eines Bildes] --> B[AWS Lambda<br>Event Trigger]
    B --> C[Amazon Rekognition<br>RecognizeCelebrities]
    C --> D[Output S3 Bucket<br>JSON Ergebnis]

## 2.2 Komponentenbeschreibung

|Komponente	| Beschreibung |	Zweck |
|-----------|--------------|--------|
|Input S3 Bucket | Speichert hochgeladene Bilder |	Startet die Lambda-Funktion beim Upload|
|AWS Lambda Funktion |	Arbeitet das Bild auf, ruft Rekognition auf |Automatische Verarbeitung ohne Server |
|Amazon Rekognition |	Analyse des Bildes, erkennt bekannte Personen	|Liefert Namen + Confidence-Werte|
Output S3 Bucket |	Speichert das Ergebnis als JSON	| Dient als Output-Speicher für die Analyse|

---

# 3. Umsetzung
# 3. Umsetzung

Dieses Kapitel beschreibt die technische Umsetzung des Projekts. Dazu gehören der Aufbau der Cloud-Ressourcen, die Erstellung der Lambda-Funktion, die Automatisierung mittels Skripten sowie die getestete Funktionsweise.

## 3.1 Aufbau der Cloud-Ressourcen
Hier wird erklärt, welche AWS-Ressourcen erstellt wurden und wie sie miteinander verbunden sind.
- Erstellung der S3 Buckets (Input / Output)
- Erstellen der IAM-Rolle für Lambda
- Definition der Berechtigungen
- Konfiguration des S3-Event-Triggers

## 3.2 Lambda-Funktion
Beschreibung der Funktionalität der Lambda-Funktion.
- Trigger durch S3-Upload
- Laden des Bildes
- Aufruf von Amazon Rekognition (RecognizeCelebrities)
- Verarbeitung des Resultats
- Schreiben der JSON-Ausgabe in den Output-Bucket

## 3.3 Init-Script (Automatische Erstellung)
Dokumentation des Scripts, das alle Ressourcen automatisch anlegt.
- Zweck des Scripts
- Ablauf und Logik
- Vorteile der Automatisierung

## 3.4 Test-Script (Automatisierte Prüfung)
Beschreibung des Scripts, das Bilder hochlädt und Ergebnisse abruft.
- Upload des Testbildes
- Polling/Wait-Mechanismus bis zur Auswertung
- Download der JSON-Ausgabe
- Ausgabe der erkannten Personen

## 3.5 Wichtige technische Entscheidungen
- Entscheidung 1 – warum diese Architektur gewählt wurde
- Entscheidung 2 – warum Rekognition RecognizeCelebrities
- Entscheidung 3 – warum Automation via CLI/Shell statt manuell im Console-UI

## 3.6 Codebeispiele
Hier kannst du später Ausschnitte einfügen, z. B. die Lambda-Funktion oder relevante Befehle.

## 3.7 Herausforderungen während der Umsetzung
- Beispiel: IAM-Berechtigungen funktionierten anfangs nicht korrekt
- Beispiel: Lambda-Timeout / zu grosse Bilder
- Beispiel: JSON-Struktur testen

---

# 4. Installation und Verwendung

Hier wird beschrieben, wie die Lösung installiert, gestartet und ausgeführt wird.

## 4.1 Voraussetzungen

- benötigte Software  
- Systemumgebung  
- weitere Abhängigkeiten  

## 4.2 Installation

```bash
git clone <repo-url>
cd projekt
./install.sh
```

## 4.3 Starten der Anwendung

```bash
./start.sh
```

---

# 5. Tests und Ergebnisse

Alle Testfälle wurden durchgeführt und protokolliert.

## 5.1 Testübersicht

| Testfall | Beschreibung | Erwartet | Ergebnis | Screenshot |
|----------|--------------|----------|----------|-------------|
| Test 1 | Erklärung | Erwartung | erfolgreich | test1.png |
| Test 2 | Erklärung | Erwartung | erfolgreich | test2.png |
| Test 3 | Erklärung | Erwartung | erfolgreich | test3.png |

## 5.2 Beispielauswertung

```json
{
  "status": "ok",
  "details": "Beispielresultat"
}
```

## 5.3 Fazit

- Test 1: erfolgreich  
- Test 2: erfolgreich  
- Test 3: erfolgreich  

---

# 6. Aufgabenverteilung

| Teammitglied | Aufgabe | Anteil |
|--------------|---------|--------|
| Person A | Implementierung | 40% |
| Person B | Dokumentation & Tests | 35% |
| Person C | Konzept & Architektur | 25% |

---

# 7. Reflexion

## 7.1 Persönliche Reflexionen

### Person A
- positive Punkte  
- Herausforderungen  
- Verbesserungspotential  

### Person B
- positive Punkte  
- Herausforderungen  
- Verbesserungspotential  

### Person C
- positive Punkte  
- Herausforderungen  
- Verbesserungspotential  

## 7.2 Gesamtreflexion

- Was gut funktionierte  
- Was verbessert werden könnte  
- Erkenntnisse für zukünftige Projekte  

---

# 8. Quellen und Anhänge

## 8.1 Quellen

- Dokumentationen  
- Onlineresearch  
- weitere Ressourcen  

## 8.2 Anhänge

- zusätzliche Diagramme  
- Screenshots  
- ergänzende Dateien  
