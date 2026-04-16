# Stationeers IC10 Codes

Eine Sammlung von **39 IC10-Automatisierungsskripten** für das Spiel Stationeers, organisiert in funktionale Module. Die Skripte basieren auf einem modularen Konzept mit getrennten Scanner-, Controller- und Executor-Chips.

---

## Inhaltsverzeichnis

- [Übersicht & Architektur](#übersicht--architektur)
- [Ordnerstruktur](#ordnerstruktur)
- [Base](#base)
- [Furnace Controll](#furnace-controll)
- [Greenhouse](#greenhouse)
- [Larre Base Controll](#larre-base-controll)
- [Rocket Controlling](#rocket-controlling)
- [Rocket House](#rocket-house)
- [Silos Controll](#silos-controll)
- [Stammverzeichnis (Einzelskripte)](#stammverzeichnis-einzelskripte)
- [Gemeinsame Geräte-Hashes](#gemeinsame-geräte-hashes)
- [Allgemeine Hinweise](#allgemeine-hinweise)

---

## Übersicht & Architektur

Die Skripte folgen einem **Scanner / Controller / Executor**-Muster:

- **Scanner**: Liest Sensordaten und schreibt in Speicher-Chips
- **Controller**: Wertet Daten aus und entscheidet über Aktionen
- **Executor**: Führt physische Aktionen aus (z. B. LArRE-Arm-Bewegungen)

Die Kommunikation zwischen Chips erfolgt über **Logic Memory**-Bausteine. Geräte werden per **Hash-Adressierung** über das Gerätenetzwerk (d0–d5 Pins) angesprochen.

---

## Ordnerstruktur

```
Stationeers IC10 Codes/
├── Base/
│   ├── Base Atmo Controll.ic10
│   ├── Base LightControll.ic10
│   └── GasTankControll.ic10
├── Furnace Controll/
│   ├── IC1 UI Display.ic10
│   ├── IC2 Database 1.ic10
│   ├── IC3 Database 2.ic10
│   ├── IC4 Furnace Controller New Opt.ic10
│   ├── IC4 Furnace Controller.ic10
│   ├── IC5 Silo Display Controller.ic10
│   ├── Larre_Airlock.ic10
│   ├── Larre_Controll.ic10
│   └── extern Cooling System for Gas.ic10
├── Greenhouse/
│   ├── Atmo Controll.ic10
│   ├── Growlight Timer, Sorter, Stapler.ic10
│   ├── LArRE Arm Controll.ic10
│   ├── LArRE Live-Scanner.ic10
│   └── Soja Atmo Controll.ic10
├── Larre Base Controll/
│   ├── Database.ic10
│   ├── Larre Controll Base Manufactors.ic10
│   └── larre controll.ic10
├── Rocket Controlling/
│   ├── Auto-Mining.ic10
│   ├── Auto-Scanning.ic10
│   ├── Orbit List.ic10
│   ├── R1_Light_LED_Umbilicals.ic10
│   ├── R1_MainLogic.ic10
│   ├── R2_Light_LED_Umbilicals.ic10
│   └── R2_MainLogic.ic10
├── Rocket House/
│   └── Raumlicht Steuerung Rocket House.ic10
├── Silos Controll/
│   ├── Manuel_Silo_Item_Output.ic10
│   ├── Ore Autolathe Controll with Quantity Controll.ic10
│   ├── Silo Displays.ic10
│   └── Silo Logic Sorter.ic10
├── # Kühlkreislauf + Transfer ins Waste-Net.ic10
├── Centrifuge and Recycler.ic10
├── Coal Generator with Autolathe Controll.ic10
├── Gas Filtration Station.ic10
├── Gaskuehlung.ic10
├── Tank Controll.ic10
└── Trader Search System.ic10
```

---

## Base

### Base Atmo Controll.ic10

**Zweck:** Hauptatmosphärenregelung der Basis mit CO2-Management, Heizung/Kühlung, Druckregelung und AutoLathe-Überwachung.

**Was macht das Skript:**
- Hält Druck bei 101 kPa, Temperatur zwischen 20–22 °C
- Überwacht CO2 (max. 5 %), Schadstoffe, Wasserstoff, Methan, Lachgas
- Schützt Kühlwasser vor Einfrieren (Frost-Schutz)
- Stellt AutoLathe bei Fehlern automatisch wieder her

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Pressure Sensor | `-1252983604` | RaumSensor |
| Gas Mixer | `2104106366` | RaumMixer |
| Powered Vent (Abluft) | `-785498334` | AbluftFlur |
| Powered Vent (Zuluft) | `-785498334` | ZuluftFlur |
| Gas Analyzer | `435685051` | RaumAnalysator |
| Coolant Pipe Sensor | `226055671` | KWRohrSensor |
| Valve | `-1280984102` | Ventil |
| Cooler | `-1369060582` | HausKuehler |
| Heater | `24258244` | HausHeizung |
| AutoLathe | `336213101` | AutoLatheWater |

**Zielparameter:**
- Druck: 101 kPa
- Temperatur: 20–22 °C (293,15–295,15 K)
- CO2: max. 5 %
- Kühlwasser-Rohrdruck: 10–48 MPa

---

### Base LightControll.ic10

**Zweck:** Einfache Beleuchtungssteuerung basierend auf Anwesenheitssensoren.

**Was macht das Skript:**
- Schaltet Lichter ein bei erkannter Bewegung oder Anwesenheit
- Binäre Ein/Aus-Steuerung ohne Dimmen

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Occupancy Sensor | `322782515` | — |
| Motion Sensor | `-1713470563` | — |
| Wandleuchte (lang/breit) | `555215790` | basis_wandleuchte_lang_breit |
| Rundes Licht | `1514476632` | aufzug_eg_leicht_rund |

---

### GasTankControll.ic10

**Zweck:** Überwachungs- und Anzeigesystem für 10 verschiedene Gastanks mit Druck- und Temperaturanzeige.

**Was macht das Skript:**
- Überwacht O2, CO2, N2, Schadstoffe, CH4, N2O, H2, Waste, Ice und Basisatmo
- Farbkodierte LED-Anzeigen: Grün = OK, Gelb = Warnung, Rot = Gefahr
- Druckanzeige (Modus 14) und Temperaturanzeige (Modus 4/3)
- Referenzwerte: 50 kPa & 973 K (Standard), 48 kPa (Waste), 10 kPa / 586 K (Basisatmo)

**Benötigte Geräte ingame:**

| Gerät | Hash | Hinweis |
|-------|------|---------|
| Gas Analyzer | `435685051` | Einen Analyzer pro Tank (×10) |
| Gauge (2×2) | — | Manometeranzeigen |
| LED Display | `-246585138` | Digitalanzeigen |

---

## Furnace Controll

Das Schmelzofensystem besteht aus **5 IC-Chips**, die zusammenarbeiten. Aufbaureihenfolge: IC2/IC3 zuerst starten, dann IC4, dann IC1 und IC5.

```
IC1 (UI-Eingabe) ──► IC2/IC3 (Rezeptdatenbank) ──► IC4 (Ofen-Regler)
                                                         |
                                                    IC5 (Silo-Check)
```

---

### IC1 UI Display.ic10

**Zweck:** Benutzeroberfläche für Rezeptauswahl, Mengenangabe und Ofenstatus-Anzeige.

**Was macht das Skript:**
- Navigation durch 18 Rezepte (0 = Aus, 1–17 = Metalle/Legierungen)
- Mengeneingabe per Numpad
- LED-Statusanzeige: Grün = bereit, Rot = aktiv
- Automatische Ausbeute-Berechnung (50g/Einheit Metall, 200g/Einheit Stahl usw.)

**Unterstützte Rezepte:**

| Nr. | Material | Nr. | Material |
|-----|----------|-----|----------|
| 0 | Aus | 9 | Electrum |
| 1 | Eisen | 10 | Invar |
| 2 | Gold | 11 | Constantan |
| 3 | Kupfer | 12 | Solder |
| 4 | Nickel | 13 | Astroloy |
| 5 | Silber | 14 | Hastelloy |
| 6 | Blei | 15 | Inconel |
| 7 | Silizium | 16 | Stellite |
| 8 | Stahl | 17 | Waspaloy |

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Numpad | `-377257892` | Numpad |
| Button Zurück | `1462769197` | BtnPrev |
| Button Weiter | `1462769197` | BtnNext |
| Button Bestätigen | `489382030` | BtnConf |
| Furnace | `545937711` | Smeltery_Furnace |
| Quantity Display | `-246585138` | Quantity |
| Status LED | `1644427753` | furnace_led_status |

---

### IC2 Database 1.ic10

**Zweck:** Primäre Rezeptdatenbank mit Temperatur-, Druck- und Zutatenparametern für Metalle und Basislegierungen.

**Was macht das Skript:**
- Stellt Rezeptparameter für IC4 bereit (MinTemp, MaxTemp, MinDruck, MaxDruck)
- Enthält Rezepte für Eisen, Gold, Kupfer, Nickel, Silber, Blei, Silizium (1–7) und erste Legierungen (8–12)
- Steuert Dispensier-Silos für die jeweiligen Zutaten

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Logic Memory | `-851746783` | Gemeinsamer Speicherchip |
| Silos (je Zutat) | `1155865682` | Ein Silo pro Rohstoff |

---

### IC3 Database 2.ic10

**Zweck:** Sekundäre Rezeptdatenbank für Superlegierungen (Rezepte 13–17).

**Was macht das Skript:**
- Enthält komplexe Mehrstoff-Rezepte: Astroloy (Kobalt+Kupfer+Stahl), Hastelloy, Inconel, Stellite, Waspaloy
- Gleiche Funktionsweise wie IC2, deckt den erweiterten Rezeptbereich ab

**Benötigte Geräte ingame:** Identisch zu IC2 Database 1.

---

### IC4 Furnace Controller New Opt.ic10 *(Empfohlen)*

**Zweck:** Fortgeschrittener PID v2.1-Regler für präzise Temperatursteuerung des Schmelzofens.

**Was macht das Skript:**
- PID-Regelung mit Kp=4, Ki=0,15, Kd=3 und Anti-Windup-Schutz
- Offset-Korrektur (0,5 K) und Totband (0,3 K) gegen Pumpenwettbewerb
- Sicherer Abfahrvorgang: schließt Mixer/Pumpen, kühlt auf < 1800 K ab
- Leitungsheizung für O2 und VOL (Hysterese 292–293 K)

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Furnace | `545937711` | Smeltery_Furnace |
| Gas Mixer | `2104106366` | Smeltery_FuelMixer |
| Fuel Pump | `1310794736` | Smeltery_FuelPump |
| Cold Pump | `1310794736` | Smeltery_ColdPump |
| Heater (O2-Leitung) | `-419758574` | HeizungO2 |
| Heater (VOL-Leitung) | `-419758574` | HeizungVOL |
| Gas Analyzer (O2) | `435685051` | O2-Leitungsanalysator |
| Gas Analyzer (VOL) | `435685051` | VOL-Leitungsanalysator |

---

### IC4 Furnace Controller.ic10 *(Legacy)*

Ältere Version ohne PID-Optimierung, nur für Kompatibilität beibehalten. **Empfohlen: "New Opt"-Version verwenden.**

---

### IC5 Silo Display Controller.ic10

**Zweck:** Zeigt an, ob ausreichend Material für das aktuelle Rezept in den Silos vorhanden ist.

**Was macht das Skript:**
- Vergleicht Silo-Füllstand mit Rezept-Anforderungen pro Rezeptschritt
- LED-Feedback: Grün = alles vorhanden, Rot = Material fehlt
- Zeigt welches spezifische Material gerade fehlt

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| LED / Confirm Button | `489382030` | BtnConf |
| Zutaten-Silos | `1155865682` | Silos mit Rohstoffen |

---

### Larre_Airlock.ic10

**Zweck:** Schleusensteuerung für den LArRE-Arm zur Vermeidung von Gasvermischung beim Ofenzugang.

**Was macht das Skript:**
- Verwaltet Innen- und Außentür der Schleuse automatisch
- Pumpt Atmosphäre vor dem Türöffnen ab
- Bidirektionaler Betrieb (LArRE rein und raus)

**Zustandsmaschine:**
- 0 = Idle | 1 = Außenschleuse pumpen | 2 = Innenschleuse pumpen | 3 = Innen öffnen | 4 = Außen öffnen

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Door (Innen) | `-2131782367` | furnace_larre_arm_door_in |
| Door (Außen) | `-2131782367` | furnace_larre_arm_door_out |
| Powered Vent (Innen) | `-785498334` | furnace_larre_vent_in |
| Powered Vent (Außen) | `-785498334` | furnace_larre_vent_out |
| Gas Sensor | `-1252983604` | furnace_larre_gas_sensor |
| LArRE Arm | `-522428667` | FurnaceLarre |

---

### Larre_Controll.ic10

**Zweck:** LArRE-Arm-Dispatcher für automatische Materialzufuhr zum Schmelzofen aus dem Export-Chute.

**Was macht das Skript:**
- Liest Materialien aus dem Export-Kanal
- Transportiert Material zu Station -5 (Ofen)
- Überwacht Aufnahme/Ablage-Zyklen, erkennt Stalls
- Meldet Statuscodes via LED-Anzeige

**Statuscodes:**

| Code | Bedeutung |
|------|-----------|
| 100 | Bereit |
| 200 | Fährt zum Export |
| 210 | Sammelt Items |
| 300 | Fährt zum Ofen |
| 310 | Lädt Ofen aus |
| 400 | Arm einfahren |
| 410 | Ladung prüfen |
| 500 | Rückkehr zur Basis |
| 600 | Export leer-Check |
| 700 | Fertig |

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| LArRE Arm | `-522428667` | FurnaceLarre |
| Export Chute | `1957571043` | LarreExportChute |
| Logic Memory | `-851746783` | Speicherchip |

---

### extern Cooling System for Gas.ic10

**Zweck:** Externes Kühlsystem zur Herstellung von Kaltgas (Eis-Produktion) für den Schmelzofenbetrieb.

**Was macht das Skript:**
- Aktiviert AutoLathe automatisch mit Eis-Rezept
- Hysterese-basierte Heizung der Leitungen (185–195 K)
- Dispensiert Eis wenn Leitungsdruck < 35 MPa
- Prüft Ofenauslastung vor Dispensierung

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| AutoLathe | `336213101` | ColdGasAutolathe |
| Gas Analyzer | `435685051` | KaltGasAnalyzer |
| LED | `-53151617` | LEDKalt |
| Heater | `-419758574` | ColdGasHeater |
| Vending Machine | `-1577831321` | ColdGasVendingMachine |
| Furnace | `545937711` | ColdGasFurnace |

**Rezept:** Ice (Hash: `-1708395413`)

---

## Greenhouse

### Atmo Controll.ic10

**Zweck:** Hauptatmosphärenregler für das Gewächshaus mit Gasgemisch-Steuerung, CO2-Regelung und Notfall-Spülung.

**Was macht das Skript:**
- Hält Druck bei 101 kPa, Temperatur bei 22 °C
- CO2: 10–20 % für optimales Pflanzenwachstum
- Alarm bei Kontamination (Schadstoff, H2, CH4, N2O > 0,1 %)
- Alarm bei Frost (< 10 °C)
- Automatische Druckentlastung und Spülung

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Powered Vent (Zuluft) | `-785498334` | GrowZuluft |
| Powered Vent (Abluft) | `-785498334` | GrowAbluft |
| Cooler | `-1369060582` | GrowKuehler |
| Heater | `24258244` | GrowHeizung |
| Alarm Light | `576516101` | GrowAlarmLight |
| Pressure Sensor | `-1252983604` | GrowSensor |
| Gas Mixer | `2104106366` | GrowGasMixer |
| Gas Analyzer | `435685051` | GrowGasAnalyse |

**Zielparameter:** 101 kPa, 22 °C, CO2 10–20 %, N2 < 5 %, Rohr < 20 MPa

---

### Soja Atmo Controll.ic10

**Zweck:** Speziell optimierter Atmosphärenregler für Soja-Anbau mit angepassten Parametern.

**Was macht das Skript:** Identisch zu Atmo Controll, aber mit anderen Sollwerten:
- Druck: 75 kPa (Überdruck-Limit: 80 kPa)
- Temperatur: 25 °C (wärmer für Soja)
- CO2: 10–40 % (höheres Maximum)
- N2: mindestens 10 %

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Powered Vent (Zu/Ab) | `-1129453144` | GrowSojaZuluft / GrowSojaAbluft |
| Cooler | `-1369060582` | GrowSojaKuehler |
| Heater | `24258244` | GrowSojaHeizung |
| Pressure Sensor | `-1252983604` | GrowSojaSensor |
| Gas Mixer | `2104106366` | GrowSojaGasMixer |
| Gas Analyzer | `435685051` | GrowSojaGasAnalyse |

---

### Growlight Timer, Sorter, Stapler.ic10

**Zweck:** Wachstumslampen-Zeitsteuerung für Tag-/Nacht-Simulation im Gewächshaus.

**Was macht das Skript:**
- Simuliert Tag-Nacht-Zyklus: Tag = 600 Ticks (≈5 Min.), Nacht = 300 Ticks (≈2,5 Min.)
- Steuert Sortier- und Staplergeräte
- Zähler reset nach vollem Zyklus

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Sorter | `873418029` | SojaLogicSorter |
| Stapler | `-2020231820` | — |
| Growlight | `-1758710260` | SojaGrowLight |

---

### LArRE Arm Controll.ic10

**Zweck:** Vollautomatisierter LArRE-Arm für komplette Pflanzenpflege (Aussäen, Düngen, Ernten, Exportieren).

**Was macht das Skript:**
- Prüft Status aller 10 Hydro-Beete (leer/besetzt/reif/samend)
- Sät Samen aus wenn: Beet leer + Samen vorhanden + Dünger vorhanden
- Erntet reife oder samende Pflanzen automatisch
- Exportiert geerntete Waren zur Ausgabe-Station
- Erkennt Stall-Situationen (kein Fortschritt)

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| LArRE Arm | — | d0-Anschluss (direkt) |
| Hydroponic Units (×10) | `-1841632400` | Pflanzbeete 1–10 |
| Samen-Station | — | Station -1 |
| Export-Station | — | Station -2 |
| Dünger-Station (Dung) | — | Station -3 |

---

### LArRE Live-Scanner.ic10

**Zweck:** Echtzeit-Scanner, der den Status aller 10 Pflanzbeete in einen Memory-Chip schreibt.

**Was macht das Skript:**
- Scannt alle Beete pro Zyklus
- Schreibt Status in Memory: 0=leer, 1=besetzt, 2=besetzt+samend, 3=besetzt+reif
- Formel: `Status = Besetzt × (1 + Reif + Samend)`

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Hydroponic Units (×10) | `-1841632400` | Pflanzbeete 1–10 |
| Logic Memory | `-851746783` | Statusmemory (geteilt mit LArRE Arm Controll) |

---

## Larre Base Controll

Ein 3-Chip-System für automatische Materiallieferung an alle Produktionsmaschinen der Basis.

```
Database.ic10 ──► Larre Controll Base Manufactors.ic10 ──► larre controll.ic10
(Was wird wo       (Welche Route nehmen?)                   (CargoLarre fahren)
 gebraucht?)
```

### Database.ic10

**Zweck:** Scannt 17 Materialtypen in Vending Machines und erstellt eine Lieferwarteschlange für 5 Produktionsmaschinen.

**Was macht das Skript:**
- Durchsucht Vending Machines nach verfügbarem Material
- Erstellt Stack-basierte Dispatch-Queue
- Ordnet Materialien den richtigen Maschinen zu

**17 Materialien:** Eisen, Kupfer, Gold, Blei, Nickel, Silizium, Silber, Stahl, Electrum, Solder, Invar, Constantan, Waspaloy, Stellite, Inconel, Hastelloy, Astroloy

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Vending Machine (Barren) | — | Ba_Ingots_Vending |
| Vending Machine (Legierung) | — | Al_Ingots_Vending |
| Vending Machine (Superleg.) | — | SuAl_Ingots_Vending |
| AutoLathe | `336213101` | d0 |
| Pipe Bender | — | d1 |
| Electronics Printer | — | d2 |
| Tool Manufactory | — | d3 |
| Rocket Manufactory | — | d4 |

---

### Larre Controll Base Manufactors.ic10

**Zweck:** LArRE-Executor der die Befehle aus Database.ic10 ausführt und Materialien physisch transportiert.

**Was macht das Skript:**
- Empfängt Befehle aus Datenbank
- Konvertiert Item-Hash in Reagenz-Hash (für alle 17 Materialien)
- Transportiert Material zur Zielmaschine (Station -1 bis -6)
- Schließt Bin-Schleusen nach erfolgreicher Ablage

**Fehlercodes:** 91 = Item-Hash unbekannt | 93 = LArRE-Aufnahme fehlgeschlagen

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Export Chute | `1957571043` | ExportAlloys |
| CargoLarre | `-1555459562` | — |
| Bins (×5) | `-850484480` | Eine Bin pro Produktionsmaschine |

---

### larre controll.ic10

**Zweck:** Niedrig-Level-CargoLarre-Fahrer, der formatierte Befehle in Fahrbewegungen übersetzt.

**Was macht das Skript:**
- Dekodiert Befehle nach dem 100er-Schema: `100 + VendingID×10 + MachineID`
  - Beispiel: 134 = Vending-Slot 3 → Maschine 4
- Fährt CargoLarre zur Vending, nimmt auf, liefert an Maschine
- Meldet Statuscodes: 10=Idle, 30=zu Vending, 40=zu Maschine, 70=fertig, 99=Fehler

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| CargoLarre | `-1555459562` | — |
| Control Bins | `-850484480` | — |

---

## Rocket Controlling

### R1_MainLogic.ic10

**Zweck:** Hauptlogik-Controller für Rakete 1 (Scan-Rakete) mit automatischem Display-Update und Umbilical-Verwaltung.

**Was macht das Skript:**
- Aktualisiert alle 5 LED-Displays pro Zyklus (Aktuelle Position, Ziel, Zeit, Batterie, Gas)
- Hysterese für Umbilicals: Batterie 95–99 %, Gas 35–40 MPa
- Trennt Umbilicals automatisch bei Raketenstart

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Avionics | `808389066` | R1_Avionics |
| Battery | `-1125305264` | R1_Bat_1 |
| Gas Tank | `-1093860567` | R1_GasTank |
| Scanner | `2014252591` | — |
| LED Displays (×5) | `-1949054743` | RB1_LEDDISPLAY_1 bis _5 |
| Power Umbilical | `1529453938` | RB1_Umbilical_Power |
| Gas Umbilical | `-1814939203` | RB1_Umbilical_Gas |

---

### R1_Light_LED_Umbilicals.ic10

**Zweck:** LED-Statusanzeige für den Verbindungsstatus der Umbilicals von Rakete 1.

**Was macht das Skript:**
- Blau = Rakete im Flug | Grün = Verbunden & bereit | Rot = Problem | Aus = Nicht verbunden
- Blinkt bei Verbindungsproblemen zur Aufmerksamkeit

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Power Umbilical | `1529453938` | RB1_Umbilical_Power |
| Gas Umbilical | `-1814939203` | RB1_Umbilical_Gas |
| Power LED | `1944485013` | RB1_PowerLED |
| Gas LED | `1944485013` | RB1_GasLED |
| Avionics | `808389066` | R1_Avionics |

---

### Auto-Scanning.ic10

**Zweck:** Vollautomatischer Scan-Missions-Controller für Rakete 1 — fliegt selbstständig Ziele an und scannt sie.

**Was macht das Skript:**
- Fliegt automatisch zu Mars L4, L5 und Asteroiden
- Drei Scan-Phasen: Discover (Modus 4) → Survey (Modus 3) → Chart (Modus 5)
- Konfigurierbar über Numpad (Ziele aktivieren/deaktivieren)
- Kehrt automatisch heim wenn: Tank < 15.000 kPa oder Batterie < 20 %

**Scan-Ziele:**

| Zielcode | Beschreibung |
|----------|-------------|
| `4016` | Startplatz (Heimat) |
| `201010116` | Mars L5 |
| `101010116` | Mars L4 |
| `2003010116` | Kolumnare Asteroiden |
| `2002010116` | Eisenhaltige Asteroiden |

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Avionics | `808389066` | R1_Avionics |
| Engine | `-214232602` | R1_Engine |
| Gas Tank | `-1093860567` | R1_GasTank |
| Battery | `-1125305264` | R1_Bat_1 |
| Scanner | `2014252591` | — |
| Config Numpad | `491845673` | Auto-Scan-Conf |
| Power Umbilical | `1529453938` | RB1_Umbilical_Power |
| Gas Umbilical | `-1814939203` | RB1_Umbilical_Gas |

---

### R2_MainLogic.ic10

**Zweck:** Hauptlogik-Controller für Rakete 2 (Mining-Rakete), erweitert um Chute-Verwaltung und Bohrkopf-Anzeige.

**Was macht das Skript:** Wie R1_MainLogic, zusätzlich:
- Anzeige von Bohrkopf-Zustand (Modus 1) und Sammelzähler (Modus 14)
- Chute-Steuerung: öffnet nur wenn Chute-Silo nicht voll
- Integriert Chute-Umbilical in die Hysterese-Logik

**Benötigte Geräte ingame (zusätzlich zu R1):**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Chute Umbilical | `-958884053` | RB2_Umbilical_Chute |
| Chute Silo | `1151864003` | R2_ChuteSilo |
| Mining Drill | `-2087223687` | — |
| Avionics | `808389066` | R2_Avionics |
| Battery | `-1125305264` | R2_Bat_1 |
| Gas Tank | `-1093860567` | R2_GasTank_1 |

---

### R2_Light_LED_Umbilicals.ic10

**Zweck:** LED-Statusanzeige für Rakete 2, mit zusätzlicher Chute-Umbilical-Anzeige.

**Was macht das Skript:** Wie R1-Version, zusätzlich Chute-LED mit gleichem Farbschema.

**Benötigte Geräte ingame:** Wie R1 + Chute Umbilical (`-958884053`) und Chute LED (`1944485013`)

---

### Auto-Mining.ic10

**Zweck:** Vollautomatischer Mining-Missions-Controller für Rakete 2 — sucht, fliegt an und baut Asteroiden ab.

**Was macht das Skript:**
- Scannt verfügbare Asteroiden-Ziele und wählt optimalen an
- Fliegt zu Metall-Asteroiden und aktiviert Mining-Drill
- Kehrt automatisch zurück wenn: Tank < 15.000 kPa, Batterie < 20 %, Chute-Silo voll

**Mining-Zielcodes:**

| Code | Beschreibung |
|------|-------------|
| `2003010116` | Metall-Asteroiden (primär) |
| `2002010116` | Metall-Asteroiden (alternativ) |
| `20030116` | Lokale Metall-Asteroiden |
| `20040116` | Felsen/Gesteinsbrocken |

**Benötigte Geräte ingame:** Alle R2-Geräte (wie R2_MainLogic + Auto-Scanning Numpad `491845673` als `Auto-Mining-Conf`)

---

### Orbit List.ic10

**Zweck:** Referenzdokument mit vorkonfigurierten Orbit-Zielkoordinaten für die Navigation.

**Was macht das Skript:** Enthält keine aktive Logik — ist eine dokumentierte Liste von Orbit-Codes für die manuelle Programmierung der anderen Raketen-Skripte.

---

## Rocket House

### Raumlicht Steuerung Rocket House.ic10

**Zweck:** Kombiniertes Atmosphären- und Beleuchtungs-Management für das Raketen-Hangar-Gebäude.

**Was macht das Skript:**
- Anwesenheitsbasierte Beleuchtung (Ein/Aus je nach Person im Raum)
- Temperaturregelung auf 22 °C
- CO2-Überwachung (max. 1 %) und Schadstoff-Überwachung (Ziel: 0 %)
- Druckregelung auf 101 kPa

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Occupancy Sensor | `322782515` | — |
| Light | `555215790` | — |
| Fuel Mixer Switch | `1220484876` | — |
| Fuel Mixer | `2104106366` | RB1_FuelMixer |
| Pressure Sensor | `-1252983604` | RaumSensorRocket |
| Powered Vent (Zuluft) | `-785498334` | ZuluftRocket |
| Powered Vent (Abluft) | `-785498334` | AbluftRocket |
| Cooler | `-1369060582` | HausKuehler |

---

## Silos Controll

### Silo Displays.ic10

**Zweck:** Echtzeit-Anzeigesystem für die Füllstände aller Material-Silos (30+ Materialtypen).

**Was macht das Skript:**
- Liest Silo-Mengen und zeigt sie auf LED-Displays an
- Speichert Icon-Hashes in Logic Memory für schnellen Zugriff

**Angezeigte Materialien:**
- 8 Basismetalle: Eisen, Gold, Kupfer, Nickel, Silber, Blei, Silizium, Stahl
- 9 Legierungen: Electrum, Invar, Constantan, Solder, Astroloy, Hastelloy, Inconel, Stellite, Waspaloy
- Sondermetalle: Kobalt, Uran, Kohle
- 12 Reineis-Varianten: Steam, Silanol, Pollutant, Ozone, O2, N2O, N2, Volatiles, H2, Hydrazine

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Silos (×30+) | `1155865682` | Ein Silo pro Materialtyp |
| LED Displays | `-246585138` | Füllstandsanzeigen |
| Logic Memory | `-851746783` | Icon-Speicher |

---

### Silo Logic Sorter.ic10

**Zweck:** Initialisiert die Sortierstrecken mit den richtigen Material-Icons für das automatische Routing.

**Was macht das Skript:**
- Konfiguriert alle 30 Sorter-Spuren mit Material-Icons
- Routet eingehende Materialien automatisch zum richtigen Silo

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Sorter | `873418029` | — |
| Stapler | `-2020231820` | — |

---

### Ore Autolathe Controll with Quantity Controll.ic10

**Zweck:** Vollautomatische Erz-Verarbeitung durch AutoLathe mit Mengenkontrolle für 10 Materialien.

**Was macht das Skript:**
- Prüft Silo-Füllstand kontinuierlich (Aktivierung: < 590, Maximum: 600)
- Startet AutoLathe automatisch bei Bedarf, hält es an bei vollem Silo
- Rezept-Wiederherstellung nach Fehlern (Recipe-Hash bleibt erhalten)

**Verwaltete Materialien:** Eisen, Kupfer, Gold, Silizium, Kohle, Blei, Nickel, Silber, Kobalt, Uran

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| AutoLathe | `336213101` | — |
| Sorter | `1585641623` | — |
| Silos (×10) | `1155865682` | Ein Silo pro Erz |

---

### Manuel_Silo_Item_Output.ic10

**Zweck:** Manueller Silo-Dispenser mit vollständiger UI-Steuerung für alle 17 Material-Typen.

**Was macht das Skript:**
- Rezeptauswahl per Prev/Next-Buttons (0–17)
- Mengeneingabe per Numpad
- Pulsierendes Öffnen/Schließen des Silos bis Zielmenge erreicht
- ExportCount-Feedback zur präzisen Mengenkontrolle

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Silo | `1155865682` | — |
| Button (Prev/Next) | `1462769197` | — |
| Button (Confirm) | `489382030` | — |
| Numpad | `-377257892` | BaseSilo_Numpad |
| Logic Memory | — | Statusmemory |

---

## Stammverzeichnis (Einzelskripte)

### # Kühlkreislauf + Transfer ins Waste-Net.ic10

**Zweck:** Temperaturgesteuerter Kühlkreislauf mit automatischem Gastransfer aus dem Produktionsnetzwerk ins Waste-Netz.

**Was macht das Skript:**
- Ventil: Öffnet Radiator-Bypass bei > 30 °C, schließt bei < 5 °C
- Pumpe: Aktiv nur im Fenster 0–25 °C, mit Druckhysterese
- Überträgt erhitztes Gas von Netzwerk 1 → Netzwerk 2 (Waste)

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Furnace | `545937711` | ice_furnace |
| Gas Analyzer | `435685051` | ice_analyzer |
| Valve | `-1280984102` | ice_valve (Radiator-Bypass) |
| Pump | `1310794736` | ice_pump |

**Temperaturgrenzen:**
- Kühlung ein: 30 °C (303,15 K) | Kühlung aus: 5 °C (278,15 K)
- Pumpe aktiv: 0–25 °C

---

### Centrifuge and Recycler.ic10

**Zweck:** Automatisierter Zentrifugenbetrieb mit Dual-Timer-System und Timeout-Schutz gegen festsitzende Chargen.

**Was macht das Skript:**
- Erkennt Fehlerzustand und öffnet automatisch
- Wartet 15 Sekunden nach Öffnen bevor Schließen (Eject-Timer: 180 Ticks)
- Timeout-Schutz nach 15 Minuten (1800 Ticks) für feststeckende Reagenzien
- Recycler läuft parallel

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Centrifuge | `690945935` | — |
| Recycler | `-1633947337` | — |

---

### Coal Generator with Autolathe Controll.ic10

**Zweck:** Kohlebasierte Stromerzeugung mit vollautomatischer AutoLathe-Steuerung und Vakuumkammer-Verwaltung.

**Was macht das Skript:**
- Überwacht Kohle-Silo (Aktivierung: < 500, Maximum: 600)
- Hält AutoLathe-Rezept aufrecht ohne Rezeptverlust bei Stopp
- Batterie-Hysterese: Generator ein bei < 50 %, aus bei > 99 %
- Vakuumkammer-Druckverwaltung

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| AutoLathe | `336213101` | AutoLatheCoal |
| Stapler | `-2020231820` | — |
| Silo | `1155865682` | Kohle-Silo |
| Pressure Sensor | `-1252983604` | VakuumSensor |
| Powered Vent | `-785498334` | VakuumVent |
| Coal Generator | `813146305` | — |
| Batteries | `-1388288459` | — |

**Rezept:** Kohle (Hash: `1724793494`)

---

### Gas Filtration Station.ic10

**Zweck:** Vollautomatisches Abgasfiltrationssystem mit dynamischer Temperaturanpassung je nach enthaltenem Gas.

**Was macht das Skript:**
- Filtert dynamisch: O2, CO2, N2, Schadstoff, CH4, N2O, H2
- Passt Zieltemperatur automatisch an: CO2 → 243 K, N2O → 203 K, Schadstoff → 143 K, Wasser → 278 K
- Notabschaltung bei > 50 °C
- Betrieb erst ab > 0,0001 kPa Gasdruck

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Filter | `-348054045` | — |
| Turbo Pump | `1310794736` | Volumenpumpe0 |
| Heater | `-419758574` | — |
| Gas Analyzer | `435685051` | waste_analyzer |

---

### Gaskuehlung.ic10

**Zweck:** Gaskühlung und Pumpensteuerung mit Temperatur-Hysterese und Überhitzungsschutz.

**Was macht das Skript:**
- Heizung: Hysterese-basiert rund um 0 °C (273,15 K)
- Pumpe: Aktiv nur bei 0–20 °C Betriebsfenster
- Abschaltung bei > 20 °C als Überhitzungsschutz

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Gas Analyzer | `435685051` | d0 (direkt) |
| Pump | `1310794736` | d3 (direkt) |
| External Temp Sensor | — | d4 (direkt) |
| Heater | `-419758574` | — |
| Powered Vent | `-785498334` | KaelteVent |

---

### Tank Controll.ic10

**Zweck:** Reineis-Produktionssystem für 6 verschiedene Gastanks mit automatischer AutoLathe-Steuerung und Überdruck-Schutz.

**Was macht das Skript:**
- Überwacht Tanküberdrücke (Panik-Grenze: 50.000 kPa)
- AutoLathe: startet bei < 25.000 kPa, stoppt bei > 35.000 kPa
- LED-Farbkodierung: Grün = normal, Rot = Panik
- Max. Temperaturüberwachung: 30 °C

**Verwaltete Tanks:** O2, N2, CO2, Volatiles, Pollutant, N2O

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Gas Analyzer (×6) | `435685051` | TankO2, TankN2, TankCO2, TankVol, TankPol, TankN2O |
| LED Display | `-1949054743` | — |
| AutoLathe (O2) | `336213101` | — |
| AutoLathe (Volatiles) | `336213101` | — |
| Backpressure Device | `-1149857558` | — |

---

### Trader Search System.ic10

**Zweck:** Vollautomatisches Scan-System zur Ortung von Handelsposten über rotierende Satellitenschüssel.

**Was macht das Skript:**
- Rotiert Schüssel in Scan-Muster: Horizontal 0–1620° (4,5 Umdrehungen), Vertikal Sinus-Kurve
- 4 Suchmodi mit verschiedenen Radien (100–300) per Dial wählbar
- Signalstärken-basiertes Einrasten auf stärkstes Signal
- Horizontale Fein-Ausrichtung nach Kontaktfund

**Benötigte Geräte ingame:**

| Gerät | Hash | Bezeichnung im Spiel |
|-------|------|----------------------|
| Satellite Dish | `1913391845` | — |
| Satellite Pad | `-2066405918` | — |
| Dial | `554524804` | Modus-Wahl (0–3) |

---

## Gemeinsame Geräte-Hashes

Diese Geräte werden in mehreren Skripten verwendet:

| Gerät-Typ | Hash | Hauptverwendung |
|-----------|------|----------------|
| Gas Analyzer | `435685051` | Alle Atmosphären-/Tank-Systeme |
| Logic Memory | `-851746783` | Inter-Chip-Kommunikation |
| Powered Vent | `-785498334` | Alle Atmosphären-Systeme |
| Gas Mixer | `2104106366` | Atmosphärenregelung |
| Pump (Volumen) | `1310794736` | Gas-Pumping, Kühlung |
| Pressure Sensor | `-1252983604` | Druckmessung überall |
| Heater (Raum) | `24258244` | Raumheizung |
| Cooler | `-1369060582` | Raumkühlung |
| Heater (Leitung) | `-419758574` | Leitungsheizung |
| Silo | `1155865682` | Materiallagerung |
| AutoLathe | `336213101` | Erz-/Materialverarbeitung |
| Valve | `-1280984102` | Gasventile |
| LED Display (Standard) | `-246585138` | Mengen-/Statusanzeigen |
| LED Display (Rakete) | `-1949054743` | Großformatige Displays |
| Export Chute | `1957571043` | LArRE-Übergabestellen |
| LArRE Arm | `-522428667` | Arm-basierte Automatisierung |

---

## Allgemeine Hinweise

### Geräte-Benennung

Geräte werden über **Namensuche im Netzwerk** identifiziert. Der exakte Name muss ingame am Gerät gesetzt werden. Beispiele:
```
Smeltery_Furnace
RaumSensor
GrowKuehler
R1_Avionics
```

### IC-Chip-Anschlüsse (d0–d5)

Jeder IC10-Chip hat **6 direkte Geräteanschlüsse** (d0–d5). Weitere Geräte werden per Hash-Adressierung über das Netzwerk gefunden. `db` referenziert immer den eigenen Chip.

### Inter-Chip-Kommunikation

Viele Systeme nutzen **Logic Memory**-Chips als gemeinsamen Datenspeicher. Mehrere IC-Chips lesen und schreiben koordiniert auf denselben Memory-Chip. Die Memory-Slots müssen im Skript korrekt zugewiesen sein.

### Tick-Rate

Alle Skripte sind auf **2 Ticks/Sekunde** (Standard IC10-Rate) ausgelegt:
- 120 Ticks = 1 Minute
- 1800 Ticks = 15 Minuten

### PID-Regler (Schmelzofen)

Der Ofenregler IC4 New Opt verwendet einen PID-Algorithmus:
- **P** (Proportional, Kp=4): Reagiert auf aktuellen Fehler
- **I** (Integral, Ki=0,15): Korrigiert bleibende Regelabweichungen
- **D** (Differential, Kd=3): Dämpft Überschwingung
- **Anti-Windup** (IMax=40): Begrenzt I-Anteil bei Sättigungseffekten

### Empfohlene Aufbaureihenfolge

1. **Basis-Infrastruktur:** Silos, AutoLathe, Base Atmo Controll
2. **Silo-System:** Silo Displays + Silo Logic Sorter + Ore AutoLathe Controll
3. **Schmelzofensystem:** IC2 + IC3 starten, dann IC4, dann IC1 + IC5
4. **Furnace LArRE:** Erst Airlock testen, dann Larre_Controll aktivieren
5. **Greenhouse:** Atmo-Skripte zuerst, dann Live-Scanner, dann LArRE Arm
6. **Raketen-System:** Umbilicals + LED-Skripte einrichten vor Auto-Flug aktivieren
7. **Basis-Logistik (Larre Base):** Database + Manufactors + larre controll gemeinsam starten

---

*Stationeers IC10 Automatisierungssammlung | Getestet auf Moxuna-Planeten*
