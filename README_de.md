# HomeMatic Scripts

[🇬🇧 English](README.md) | 🇩🇪 Deutsch

Dieses Repository dient als **persönliche Sammlung** meiner HomeMatic-Skripte für verschiedene Automatisierungsaufgaben.

> [!WARNING]
> 🚨 **Haftungsausschluss:** Diese Skripte wurden für meinen persönlichen Gebrauch erstellt und werden "wie besehen" ohne jegliche Garantie zur Verfügung gestellt.  
> **Nutzung auf eigene Gefahr.** Der Autor übernimmt keine Verantwortung für Probleme, die durch die Verwendung dieser Skripte entstehen.

---

## Über dieses Repository

- ✅ **Öffentlich verfügbar** – Jeder kann die Skripte einsehen und nutzen
- ⛔ **Keine aktive Wartung** – Updates erfolgen nach Bedarf und ohne Zeitplan
- ⛔ **Kein Support** – Dieses Repo dient ausschließlich als persönliche Ablage
- ⛔ **Keine Issues/Pull Requests** – Es handelt sich um persönliche Skripte ohne Community-Entwicklung

Wenn du diese Skripte nützlich findest, kannst du sie gerne an deine Bedürfnisse anpassen. Bitte habe aber Verständnis dafür, dass ich keinen Support leisten und keine Beiträge annehmen kann.

---

## Struktur

Die Skripte sind nach Anwendungsfall organisiert:

```
├── shutters/           # Rollladen-Steuerung
├── heating/            # Heizungsautomatisierung
├── lighting/           # Lichtsteuerung
├── notifications/      # Benachrichtigungs- und Alarm-Skripte
├── security/           # Sicherheitsautomatisierung
├── utilities/          # Hilfsskripte & gemeinsame Funktionen
└── examples/           # Beispiel-Konfigurationen
```

---

## Verwendung

1. Skript auswählen und Code kopieren
2. In HomeMatic CCU einfügen (Programme & Verknüpfungen → Skript)
3. Variablen und Geräte-IDs an eigene Umgebung anpassen
4. Gründlich testen bevor es produktiv genutzt wird

---

## Wichtige Hinweise

- Alle Skripte sind für **HomeMatic IP** / **HomeMatic CCU3** entwickelt
- Geräte-IDs und Kanal-Nummern müssen angepasst werden
- Einige Skripte setzen Systemvariablen voraus
- Zeitpläne und Schwellwerte sind individuell anzupassen
- Skripte verwenden deutsche Variablennamen und Kommentare (aus meiner Installation)

---

## Technische Voraussetzungen

- HomeMatic CCU3 (oder kompatibel)
- HomeMatic IP Geräte
- Grundverständnis von HomeMatic-Scripting (HM-Script/TCL)
- Kenntnisse über eigene Geräteadressen und Kanäle

---

## Skript-Kategorien

### 🪟 Shutters (Rollläden)
Automatisierte Rollladensteuerung basierend auf Zeit, Sonnenstand oder Wetterbedingungen.

**Dokumentation:** [shutters/README_de.md](shutters/README_de.md)

**Beispiel-Skripte:**
- Zeitgesteuerte Steuerung (hoch/runter)
- Sonnenpositions-basierte Steuerung
- Windschutz-Automatik

---

**Dokumentation:** [heating/README_de.md](heating/README_de.md)

**Beispiel-Skripte:**
- Fenster-offen-Erkennung (Heizung automatisch ausschalten)
- Nachtabsenkung
- Anwesenheitsbasierte Steuerung

---

### 💡 Lighting (Beleuchtung)
Automatisierte Lichtsteuerung mit Bewegungsmeldern und Dämmerungserkennung.

**Dokumentation:** [lighting/README_de.md](lighting/README_de.md)

**Beispiel-Skripte:**
- Dämmerungsautomatik
- Bewegungsmelder-basierte Beleuchtung
- Treppenhauslicht mit Timer

---

### 🔔 Notifications (Benachrichtigungen)
Alarm-Skripte für niedrige Batterien, offene Fenster und Systemereignisse.

**Dokumentation:** [notifications/README_de.md](notifications/README_de.md)

**Beispiel-Skripte:**
- Batterie-Warnung bei niedrigem Stand
- Fenster-offen-gelassen-Erinnerung
- Alarm-Benachrichtigungen

---

### 🔒 Security (Sicherheit)
Anwesenheitssimulation und Alarmanlagen-Automatisierung.

**Dokumentation:** [security/README_de.md](security/README_de.md)

**Beispiel-Skripte:**
- Anwesenheitssimulation (zufällige Licht-/Rollladensteuerung)
- Alarm-Aktivierung

---

### 🛠️ Utilities (Hilfsskripte)
Gemeinsame Funktionen, Systemvariablen-Helfer und wiederverwendbare Code-Snippets.

**Dokumentation:** [utilities/README_de.md](utilities/README_de.md)

**Beispiel-Skripte:**
- Systemvariablen-Verwaltung
- Gemeinsame Funktionen
- Logging-Helfer

---

## Erste Schritte

### 1. Navigiere zur gewünschten Kategorie
Wähle einen Ordner basierend auf deinem Anwendungsfall (z.B. `shutters/` für Rollladensteuerung).

### 2. Lies die Dokumentation
Jeder Ordner enthält eine `README_de.md` mit:
- Detaillierter Erklärung der Skripte
- Voraussetzungen und benötigte CCU-Konfiguration
- Verwendungsbeispiele
- Fehlerbehebungstipps

### 3. Passe das Skript an
- Kopiere das Skript in die CCU
- Passe Geräte-IDs, Gewerke und Räume an
- Teste mit `bDryRun = true` (Simulationsmodus)
- Aktiviere für Produktivbetrieb

### 4. Erstelle CCU-Programme
Die Skripte laufen nicht automatisch - du musst CCU-Programme erstellen:

```
WENN: [Trigger - z.B. Taster, Zeit, Sensor]
DANN: Skript ausführen: [dein-skript.hms]
```

---

## Häufig gestellte Fragen (FAQ)

### Warum werden Skripte nicht automatisch ausgeführt?
HomeMatic-Skripte sind passive Aktionen. Du musst CCU-Programme erstellen, die die Skripte bei bestimmten Ereignissen (Taster, Zeit, Sensor) ausführen.

### Warum brauche ich mehrere Skripte?
Jedes CCU-Programm kann nur EIN Skript ausführen. Für maximale Flexibilität (verschiedene Bereiche, verschiedene Aktionen) brauchst du separate Skripte.

### Wie finde ich meine Geräte-IDs?
In der CCU: **Einstellungen → Geräte & Kanäle** → Klicke auf ein Gerät → Die Kanal-IDs werden angezeigt.

### Was sind Gewerke?
"Gewerke" (auf Englisch "Functions" oder "Trades") sind CCU-interne Gruppierungen von Geräten nach Funktion (z.B. "Rolläden-EG", "Heizung-OG"). Du kannst sie unter **Einstellungen → Geräte & Kanäle** zuweisen.

### Funktionieren die Skripte mit der CCU2?
Die meisten Skripte sollten funktionieren, sind aber für CCU3 mit HomeMatic IP optimiert. Teste mit `bDryRun = true` zuerst.

---

## Best Practices

### ✅ Empfohlener Workflow:

1. **Immer mit Dry-Run testen**
   ```javascript
   boolean bDryRun = true;  // Simulation
   boolean bDebug = true;   // Ausgabe anzeigen
   ```

2. **Skripte sinnvoll benennen**
   ```
   ❌ Schlecht: script1.hms, test.hms
   ✅ Gut: shutters-groundfloor-up.hms, heating-bedroom-auto.hms
   ```

3. **Dokumentiere Anpassungen**
   Füge Kommentare im Skript ein, wenn du Werte änderst:
   ```javascript
   string sGewerke = "Rolläden-EG";  // Nur EG, nicht OG
   ```

4. **Regelmäßige Backups**
   Exportiere deine Skripte regelmäßig aus der CCU.

5. **Versionierung**
   Nutze Git/GitHub um Änderungen nachzuvollziehen.

---

## Fehlerbehebung

### Problem: "Gewerk nicht gefunden"
**Lösung:** Prüfe die exakte Schreibweise in der CCU (Groß-/Kleinschreibung beachten!)

### Problem: Skript läuft, aber nichts passiert
**Lösung:** 
- Prüfe `bDryRun = false` (nicht im Simulationsmodus)
- Aktiviere `bDebug = true` und prüfe die Logs
- Überprüfe, ob Geräte online sind

### Problem: Nur manche Geräte werden gesteuert
**Lösung:**
- Prüfe, ob alle Geräte dem Gewerk zugeordnet sind
- Überprüfe Gerätetyp-Filter (`sTypen`)
- Prüfe Ausschluss-Liste (`sExclude`)

---

## Lizenz

Dieses Projekt steht unter der [**GPL-3.0 Lizenz**](LICENSE).  
Details siehe LICENSE-Datei.

---

## Kontakt

Für allgemeine Fragen zu HomeMatic oder den Austausch über Automatisierung kannst du mich gerne erreichen – aber bitte beachte, dass ich keinen Support für diese Skripte leiste.

---

## Danksagung

- **HomeMatic/eQ-3** für das flexible Smart-Home-System
- **HomeMatic-Community** für unzählige Inspirationen und Hilfestellungen
- **Alle, die diese Skripte nutzen** – Viel Erfolg mit eurer Automatisierung!

---

**Hinweis:** Diese Skripte spiegeln mein persönliches Setup und meine Anforderungen wider. Sie erfordern möglicherweise erhebliche Anpassungen, um in deiner Umgebung zu funktionieren. Teste immer in einer sicheren Weise, bevor du sie in produktiven Systemen einsetzt.