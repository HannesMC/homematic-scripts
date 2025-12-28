# Rollladen & Jalousie Steuerung

[🇬🇧 English Version](README.md) | 🇩🇪 Deutsche Version

Skripte für die automatisierte Steuerung von HomeMatic IP Rollläden und Jalousien.

---

## 📋 Skripte in diesem Ordner

### shutter-control-up.hms
**Zweck:** Öffnet Rollläden/Jalousien (setzt LEVEL auf 100%)

**Unterstützte Geräte:**
- HmIP-BROLL (Rollladen-Aktor)
- HmIP-BBL (Jalousie-Aktor)
- HmIP-FROLL (Rollladen-Aktor Unterputz)
- HmIP-FBL (Jalousie-Aktor Unterputz)

**Funktionsweise:**
- Erkennt automatisch alle Aktoren basierend auf konfigurierten Filtern
- Filterung nach Gewerken, Räumen und Gerätetypen
- Steuert nur Kanal 4 (Haupt-Aktor-Kanal)
- Setzt LEVEL-Datenpunkt auf 1.0 (100% = vollständig offen/hoch)

---

### shutter-control-down.hms
**Zweck:** Schließt Rollläden/Jalousien (setzt LEVEL auf 0%)

**Gleiche Funktionen wie UP-Skript, setzt aber LEVEL auf 0.0 (0% = vollständig geschlossen/runter)**

---

## ⚙️ Konfigurationsvoraussetzungen

### 1. CCU-Einrichtung

**Gewerke zu Geräten zuweisen:**
```
CCU WebUI → Einstellungen → Geräte & Kanäle
→ Gerät auswählen → Gewerke-Tab
→ Zu Gewerk hinzufügen (z.B. "Rolläden-EG")
```

**Räume zu Geräten zuweisen (optional):**
```
CCU WebUI → Einstellungen → Geräte & Kanäle
→ Gerät auswählen → Räume-Tab
→ Zu Raum hinzufügen (z.B. "Wohnzimmer")
```

### 2. Skript-Konfiguration

Bearbeite den Konfigurationsbereich in jedem Skript:

```javascript
// Beispiel: Alle Rollläden im Erdgeschoss steuern
string sGewerke = "Rolläden-EG";
string sRaeume = "";  // Leer = alle Räume
string sTypen = "HmIP-BROLL,HmIP-BBL";  // Gerätetypen
string sExclude = "";  // Bestimmte Geräte ausschließen
```

### 3. Testen

**Immer zuerst mit Dry-Run testen:**
```javascript
boolean bDryRun = true;  // Simulationsmodus
boolean bDebug = true;   // Zeigt, was passieren würde
```

**Dann für Produktivbetrieb aktivieren:**
```javascript
boolean bDryRun = false;  // Befehle ausführen
boolean bDebug = false;   // Weniger ausführlich
```

---

## 🎯 Verwendungsbeispiele

### Beispiel 1: Morgenroutine - Alle Rollläden EG öffnen

**Skript:** `shutters-groundfloor-up.hms`
```javascript
string sGewerke = "Rolläden-EG";
string sRaeume = "";
string sTypen = "HmIP-BROLL";
```

**CCU-Programm:**
```
Name: Morgen - Rollläden EG öffnen
WENN: Zeit ist 07:00 (Montag-Freitag)
DANN: Skript ausführen: shutters-groundfloor-up.hms
```

---

### Beispiel 2: Abends - Schlafzimmer-Rollläden schließen

**Skript:** `shutters-bedroom-down.hms`
```javascript
string sGewerke = "";
string sRaeume = "Schlafzimmer 1,Schlafzimmer 2";
string sTypen = "HmIP-BROLL";
```

**CCU-Programm:**
```
Name: Abend - Schlafzimmer-Rollläden schließen
WENN: Zeit ist 22:00
DANN: Skript ausführen: shutters-bedroom-down.hms
```

---

### Beispiel 3: Taster-Steuerung - Wohnzimmer-Rollläden

**Skript HOCH:** `shutters-living-up.hms`
```javascript
string sGewerke = "";
string sRaeume = "Wohnzimmer";
string sTypen = "HmIP-BROLL,HmIP-BBL";
```

**Skript RUNTER:** `shutters-living-down.hms`
```javascript
// Gleiche Konfiguration, aber rTargetLevel = 0.0
```

**CCU-Programme:**
```
Name: Taster - Wohnzimmer HOCH
WENN: Wandtaster "Wohnzimmer" → Kanal 1 → KURZER_TASTENDRUCK
DANN: Skript ausführen: shutters-living-up.hms

Name: Taster - Wohnzimmer RUNTER
WENN: Wandtaster "Wohnzimmer" → Kanal 2 → KURZER_TASTENDRUCK
DANN: Skript ausführen: shutters-living-down.hms
```

---

### Beispiel 4: Sonnenschutz - Südseiten-Jalousien

**Skript:** `blinds-south-down.hms`
```javascript
string sGewerke = "Jalousien-Süd";
string sRaeume = "";
string sTypen = "HmIP-BBL";
```

**CCU-Programm:**
```
Name: Sonnenschutz - Süd-Jalousien schließen
WENN: Helligkeitssensor > 10000 Lux
UND:  Zeit zwischen 10:00 und 18:00
DANN: Skript ausführen: blinds-south-down.hms
```

---

## 📁 Empfohlene Skript-Organisation

Erstelle separate Skripte für jedes Steuerungsszenario:

```
shutters/
├── shutters-groundfloor-up.hms     (Rollläden EG hoch)
├── shutters-groundfloor-down.hms   (Rollläden EG runter)
├── shutters-firstfloor-up.hms      (Rollläden OG hoch)
├── shutters-firstfloor-down.hms    (Rollläden OG runter)
├── blinds-office-up.hms            (Jalousien Büro hoch)
├── blinds-office-down.hms          (Jalousien Büro runter)
├── shutters-bedroom-down.hms       (nur abends)
└── blinds-south-down.hms           (Sonnenschutz)
```

**Warum separate Skripte?**
- Jedes CCU-Programm kann nur EIN Skript ausführen
- Einfach zu warten und zu debuggen
- Klare Benennung zeigt Zweck
- Unterschiedliche Konfigurationen pro Bereich möglich

---

## 🔧 Erweiterte Funktionen

### Bestimmte Geräte ausschließen

Geräte nach Namen ausschließen (nützlich für Sonderfälle):

```javascript
string sExclude = "Rolladen Küche,Jalousie Büro Fenster 2";
```

### Mehrere Gewerke/Räume

Mehrere Filter kombinieren:

```javascript
// Rollläden in mehreren Räumen steuern
string sRaeume = "Wohnzimmer,Küche,Esszimmer";

// Mehrere Gewerke steuern
string sGewerke = "Rolläden-EG,Jalousien-EG";
```

### Alle Geräte eines Typs steuern

Filter leer lassen, um alle zu steuern:

```javascript
string sGewerke = "";  // Alle Gewerke
string sRaeume = "";   // Alle Räume
string sTypen = "HmIP-BROLL";  // Nur Rollläden
```

---

## ⚠️ Fehlerbehebung

**Problem: Keine Geräte werden gesteuert**
- Prüfe, ob Gewerke in der CCU zugewiesen sind
- Überprüfe Schreibweise der Gerätetypen (Groß-/Kleinschreibung beachten!)
- Aktiviere `bDebug = true` um zu sehen, was passiert

**Problem: Manche Geräte funktionieren nicht**
- Prüfe Batteriestatus der Geräte
- Überprüfe, ob Kanal 4 existiert (sollte automatisch bei Rollladen-Aktoren vorhanden sein)
- Prüfe CCU-Geräteprotokoll auf Fehler

**Problem: Skript wird ausgeführt, aber nichts passiert**
- Stelle sicher, dass `bDryRun = false` (nicht im Simulationsmodus)
- Prüfe, ob LEVEL-Datenpunkt verfügbar ist
- Überprüfe, ob Gerät nicht im manuellen Modus ist

---

## 📝 Hinweise

- Skripte steuern nur **Kanal 4** (Haupt-Aktor-Kanal)
- **LEVEL 1.0 = 100% = Vollständig offen/hoch**
- **LEVEL 0.0 = 0% = Vollständig geschlossen/runter**
- Zwischenwerte (0.0-1.0) sind möglich, werden von diesen Skripten aber nicht verwendet
- Skripte behandeln Duplikate automatisch (gleiches Gerät wird nicht zweimal gesteuert)
- Englische CCU-Begriffe: "Functions" = Gewerke, "Rooms" = Räume

---
