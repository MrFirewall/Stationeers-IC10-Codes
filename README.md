# 🚀 Stationeers IC10 Scripts Sammlung

![Game](https://img.shields.io/badge/Game-Stationeers-blue)
![Language](https://img.shields.io/badge/Language-IC10-orange)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## 📖 Übersicht

Diese Sammlung enthält **fortgeschrittene IC10 Automatisierungsskripte** für:

- 🏭 Produktionsketten
- 🌬️ Atmosphärenkontrolle
- 🚀 Raketensteuerung
- 🤖 CargoLarre Logistiksysteme
- 🌱 Gewächshaus-Automation
- 📦 Lager & Silosysteme

---

## 🧠 Architektur-Prinzipien

Diese Scripts folgen konsistenten Design-Regeln:

### 🔹 Modularität
Jedes System ist unabhängig nutzbar

### 🔹 Performance-Optimierung
- Minimale Loops
- Keine unnötigen Scans
- Vermeidung des 128-Line Limits

### 🔹 Klare Rollenverteilung
- Scanner / Controller / Executor getrennt
- Beispiel: CargoLarre (Database + Driver)

---

## 📂 Struktur

### 🏭 Core Base Systems
- Base Atmo Controll
- Base LightControll
- Tank Controll
- Gas Filtration

### 🌱 Greenhouse
- Atmosphärensteuerung
- Growlight Timer
- LArRE Automation

### 🤖 Larre Systeme
- Vollautomatische Logistik
- Multi-Machine Versorgung
- Queue-System

### 🚀 Rocket Controlling
- Auto Mining
- Orbit Scanning
- Raketenlogik

### 📦 Silos & Storage
- Sortierung
- Anzeige
- Autolathe Steuerung

---

## ⚙️ Voraussetzungen

- IC Housing
- Verkabeltes Device Network
- Grundverständnis von:
  - `d0–d5`
  - `alias`
  - `loop / yield`
  - `sensor / logic`

---

## 🚀 Nutzung

1. Script kopieren
2. In IC laden
3. Pins verbinden
4. System starten

---

## ⚠️ Wichtige Hinweise

- Viele Scripts erwarten **exakte Device-Namen**
- Positionierung (z. B. Larre) ist kritisch
- Einige Systeme sind **aufeinander abgestimmt**

---

## 🔥 Highlight: CargoLarre System

- 2-Chip Architektur
- Queue-System
- Multi-Vending Support
- Fail-Safe Mechaniken

👉 Siehe Ordner: `Larre Base Controll`

---

## 🧩 Erweiterungen

- Priorisierungssysteme
- Logging Displays
- Netzwerkübergreifende Steuerung

---

## 🙌 Contributions

Pull Requests willkommen!