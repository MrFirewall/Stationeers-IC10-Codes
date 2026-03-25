# 🚀 CargoLarre Logistik-System

### 2-Chip Architektur für vollautomatische Materialversorgung

![Status](https://img.shields.io/badge/Status-Stable-brightgreen)
![System](https://img.shields.io/badge/System-2--Chip-blue)
![Automation](https://img.shields.io/badge/Automation-Full-orange)

---

## 📖 Übersicht

Das **CargoLarre Logistik-System** automatisiert die komplette Materialversorgung deiner Basis.

* Überwacht **5 Produktionsmaschinen**
* Verwaltet **17 verschiedene Legierungen**
* Steuert einen **CargoLarre-Roboterarm**
* Versorgt Maschinen **präzise und effizient**

👉 Ziel: **Maximale Performance ohne Spielabstürze**

---

## 🧠 Systemarchitektur

### Zwei-Chip-Prinzip

| Rolle                   | Beschreibung                     |
| ----------------------- | -------------------------------- |
| 🧠 **IC-2 (Datenbank)** | Scannt Netzwerk & plant Aufträge |
| 💪 **IC-1 (Fahrer)**    | Führt Bewegungen des Larre aus   |

➡️ Vorteil:
**Keine Performance-Probleme durch große Berechnungen**

---

## ✨ Features

### 🔍 Smartes Kategorien-Scanning

Das System weiß genau, wo welche Materialien liegen:

| Kategorie  | Maschine            |
| ---------- | ------------------- |
| Basic      | Ba_Ingots_Vending   |
| Alloy      | Al_Ingots_Vending   |
| SuperAlloy | SuAl_Ingots_Vending |

➡️ Spart massiv Rechenleistung

---

### 📦 Warteschlangen-System (Stack)

* Speichert mehrere Aufträge intern
* Arbeitet sie **sequenziell** ab
* Kein erneutes Scannen notwendig

---

### 🛡️ Stabilität & Sicherheit

* Schutz vor leeren Vending Machines
* Vermeidung des **128-Zeilen-Limits**
* Sicheres Handling aller Aufträge

---

### 🗑️ Auto-Müllentsorgung

* Wartet **2 Sekunden nach Einwurf**
* Schließt automatisch den **Bin Chute**

---

## 🛠️ Setup-Anleitung

---

### 1️⃣ Vending Machines benennen

⚠️ **Exakte Schreibweise erforderlich (keine Leerzeichen!)**

```txt
Ba_Ingots_Vending
Al_Ingots_Vending
SuAl_Ingots_Vending
```

**Material-Zuordnung:**

* **Basic**: Eisen, Kupfer, Gold, Blei, Nickel, Silizium, Silber
* **Alloy**: Stahl, Electrum, Solder, Invar, Constantan
* **SuperAlloy**: Waspaloy, Stellite, Inconel, Hastelloy, Astroloy

---

### 2️⃣ Stations-IDs (CargoLarre)

```txt
Station 0   = Home / Idle

Station 1   = SuAl_Ingots_Vending
Station 2   = Al_Ingots_Vending
Station 3   = Ba_Ingots_Vending

Station -1  = Autolathe
Station -2  = Hydraulic Pipe Bender
Station -4  = Electronics Printer
Station -5  = Tool Manufactory
Station -6  = Rocket Manufactory
```

💡 **Hinweis:** Station `-3` ist für zukünftige Erweiterungen reserviert

---

### 3️⃣ IC-2 (Datenbank) Verkabelung

```txt
d0 = Autolathe
d1 = Hydraulic Pipe Bender
d2 = (frei)
d3 = Electronics Printer
d4 = Tool Manufactory
d5 = Rocket Manufactory
```

---

### 4️⃣ IC-1 (Fahrer) Verkabelung

```txt
d0 = IC-2 (Datenbank-Kommunikation)
```

➡️ Alle anderen Pins bleiben leer

---

## 📡 Kommunikation (100er-Regel)

Die Chips kommunizieren über die **Setting-Anzeige**.

---

### 🔢 Statuswerte

| Wert | Bedeutung             |
| ---- | --------------------- |
| 1–17 | Scanner aktiv         |
| ≥100 | Auftrag gesendet      |
| 0    | Auftrag abgeschlossen |

---

### 🧮 Auftragsformel

```txt
100 + (VendingID * 10) + Zielmaschine
```

**Beispiel:**

```txt
134 = Vending 3 → Maschine -4
```

---

## 🔄 Ablauf eines Auftrags

1. Datenbank scannt Maschinen
2. Fehlendes Material erkannt
3. Auftrag wird berechnet
4. Fahrer erhält Signal
5. Larre:

   * fährt zur Vending Machine
   * entnimmt Material
   * liefert zur Zielmaschine
6. Rückkehr zur Home-Position

---

## 🐛 Fehlercodes

```txt
10 = Idle / bereit
30 = Fahre zur Vending Machine
40 = Fahre zur Zielmaschine
70 = Auftrag abgeschlossen
99 = FEHLER
```

---

### ❗ Fehlercode 99 – Ursachen

* Item konnte nicht ausgeworfen werden
* Slot blockiert
* Larre falsch positioniert

---

## 📌 Tipps

* Achte auf **exakte Positionierung** der Vending Machines
* Halte die **Stations-IDs konsistent**
* Nutze freien Slot `-3` für Erweiterungen
* Teste das System zunächst mit wenigen Maschinen

---

## 🧩 Erweiterungsmöglichkeiten

* Packaging Machine (Station -3)
* Weitere Materialkategorien
* Priorisierungssystem für Aufträge
* Logging / Debug-Ausgabe

---

## 📜 Lizenz

Frei nutzbar für deine Base – Anpassung empfohlen 😉

---

## 🙌 Credits

Erstellt für effiziente Automatisierung in komplexen Produktionssystemen.
Wenn du Verbesserungen hast: **Pull Request willkommen!**
