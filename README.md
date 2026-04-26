
Individuelle Learning Phase – GitHub Actions (Workflows, Variablen und Secrets)
Ziel der Übung
In dieser Übung habe ich gelernt, einen einfachen GitHub-Actions-Workflow zu erstellen und schrittweise zu erweitern. Der Workflow automatisiert Systemprüfungen, nutzt Variablen, verarbeitet Secrets, erstellt Reports und trennt zwischen Entwicklungs- und Produktionsumgebungen.

Aufgabe 1: Einfachen Workflow erstellen
Ich habe einen Workflow in .github/workflows/sysadmin-basics.yml erstellt.
Der Workflow:
    • startet bei push und workflow_dispatch
    • läuft auf ubuntu-latest
    • nutzt actions/checkout@v4
    • führt einfache Shell-Befehle aus (Datum, Systeminfos, Verzeichnisinhalt)
    • erstellt eine Datei reports/system-report.txt mit Systeminformationen

Aufgabe 2: Umgebungsvariablen verwenden
Ich habe folgende Variablen definiert:
    • APP_NAME
    • TARGET_ENV
    • REGION
Dabei habe ich Variablen auf Workflow- und Step-Ebene verwendet.
Die Werte wurden in einer Datei reports/runtime-info.txt gespeichert und zusätzlich im Log ausgegeben, um die aktuelle Umgebung nachvollziehbar zu machen.

Aufgabe 3: Marketplace Action (Artifacts)
Ich habe die Action actions/upload-artifact verwendet, um die erzeugten Report-Dateien hochzuladen.
Folgende Dateien wurden als Artifact gespeichert:
    • reports/system-report.txt
    • reports/runtime-info.txt
Das Artifact ist nach dem Workflow-Lauf im GitHub Actions Tab herunterladbar.

Aufgabe 4: Secrets sicher verwenden
Ich habe zwei Secrets im Repository angelegt:
    • CLOUD_API_TOKEN
    • SSH_TARGET
Im Workflow wurden diese Secrets sicher eingebunden:
    • als Umgebungsvariablen verwendet
    • nicht im Log ausgegeben
    • nur geprüft, ob sie vorhanden sind
Wenn ein Secret fehlt, erscheint eine klare Meldung im Log.

Aufgabe 5: Umgebungsspezifische Konfiguration
Ich habe zwei Konfigurationsdateien erstellt:
    • config/dev.env
    • config/prod.env
Der Workflow entscheidet abhängig vom Branch:
    • main → Produktion (prod)
    • andere Branches → Entwicklung (dev)
Es wird protokolliert:
    • welche Umgebung aktiv ist
    • welche Konfigurationsdatei verwendet wird
    • welche Werte geladen wurden

Aufgabe 6: Test und Dokumentation
Ich habe den Workflow mehrfach getestet:
    • erfolgreicher Lauf
    • fehlerhafter Lauf (zur Fehleranalyse)
    • erneuter erfolgreicher Lauf nach Korrektur
Die Ergebnisse wurden in der README.md dokumentiert, inklusive:
    • Workflow-Name
    • Trigger
    • verwendete Variablen
    • verwendete Secrets
    • erzeugte Artefakte
    • Regel für dev/prod

Fazit
Durch diese Übung habe ich gelernt:
    • wie GitHub Actions Workflows aufgebaut sind
    • wie man Variablen und Secrets sicher nutzt
    • wie man Artefakte erstellt und herunterlädt
    • wie man verschiedene Umgebungen (dev/prod) trennt
    • wie man CI/CD-Prozesse praktisch umsetzt




# GitHub Actions – Workflows, Variablen und Secrets

## 📌 Projektübersicht

Dieses Projekt zeigt die praktische Umsetzung eines CI/CD-Workflows mit GitHub Actions.  
Es beinhaltet Automatisierung von Systemprüfungen, Nutzung von Variablen, sicheren Umgang mit Secrets sowie eine einfache Trennung zwischen Entwicklungs- und Produktionsumgebung.

---

## 🎯 Lernziele

- Erstellung eines GitHub Actions Workflows
- Nutzung von Umgebungsvariablen
- Sicherer Umgang mit Secrets
- Erstellung und Upload von Artifacts
- Einführung einer einfachen dev/prod Umgebung
- Praktische Umsetzung von CI/CD Grundlagen

---

## ⚙️ Workflow Struktur

Der Workflow befindet sich unter:


---

.github/workflows/sysadmin-basics.yml

---


Er wird ausgelöst durch:

- `push`
- `workflow_dispatch` (manuell)

---

## 🧪 Aufgabe 1 – Basis Workflow

Der Workflow:

- läuft auf `ubuntu-latest`
- verwendet `actions/checkout@v4`
- führt Systembefehle aus:
  - Datum anzeigen
  - Systeminformationen abrufen
  - aktuelles Verzeichnis anzeigen
  - Dateien auflisten
- erstellt eine Report-Datei:

```

reports/system-report.txt


----


🔧 Aufgabe 2 – Umgebungsvariablen
Verwendete Variablen:
    • APP_NAME 
    • TARGET_ENV 
    • REGION 
Einsatz:
    • Workflow-Level Variable 
    • Step-Level Variable 
    • Ausgabe in Log und Datei 
Ergebnisdatei:
---
reports/runtime-info.txt

----



📦 Aufgabe 3 – Artifacts
Verwendete Marketplace Action:

---
actions/upload-artifact

----
Hochgeladene Dateien:
    • reports/system-report.txt 
    • reports/runtime-info.txt 
➡️ Die Dateien sind nach dem Workflow-Lauf im GitHub Actions Bereich als Download verfügbar.







🔐 Aufgabe 4 – Secrets
Im Repository wurden folgende Secrets angelegt:
    • CLOUD_API_TOKEN 
    • SSH_TARGET 
Verwendung:
    • Übergabe als Umgebungsvariablen 
    • keine Ausgabe im Log 
    • nur Prüfung, ob vorhanden oder nicht 
✔ Secrets werden nicht im Klartext angezeigt




🌍 Aufgabe 5 – Umgebungen (dev / prod)
Es existieren zwei Konfigurationsdateien:

---

config/dev.env
config/prod.env

---

Logik:
    • Branch main → prod 
    • andere Branches → dev 
Inhalte:
    • BASE_URL 
    • LOG_LEVEL 
    • MAINTENANCE_MODE 
Der Workflow protokolliert:
    • aktive Umgebung 
    • verwendete Konfigurationsdatei 
    • geladene Werte 

📊 Ergebnis / Tests
Der Workflow wurde erfolgreich getestet:
    • ✔ erfolgreicher Run 
    • ❌ simulierter Fehlerfall 
    • ✔ erneuter erfolgreicher Run nach Fix 

🧠 Fazit
Dieses Projekt zeigt die Grundlagen von CI/CD mit GitHub Actions:
    • Automatisierte Workflows 
    • Wiederverwendbare Variablen 
    • Sichere Nutzung von Secrets 
    • Strukturierte Umgebungen (dev/prod) 
    • Erstellung von Reports und Artifacts 

🚀 Erweiterungsmöglichkeiten
    • manueller Input für Environment 
    • GitHub Environments (dev/prod mit Schutzregeln) 
    • erweitertes Error Handling 
    • Docker Deployment Pipeline
