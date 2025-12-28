# Shutter & Blind Control Scripts

🇬🇧 English Version | [🇩🇪 Deutsche Version](README_de.md)

Scripts for automated control of HomeMatic IP shutters and blinds.

---

## 📋 Scripts in This Folder

### shutter-control-up.hms
**Purpose:** Opens shutters/blinds (sets LEVEL to 100%)

**Supported Devices:**
- HmIP-BROLL (Shutter Actuator)
- HmIP-BBL (Blind Actuator)
- HmIP-FROLL (Shutter Actuator Flush-mount)
- HmIP-FBL (Blind Actuator Flush-mount)

**How it works:**
- Automatically detects all actuators based on configured filters
- Filters by Functions (Gewerke), Rooms, and Device Types
- Controls only Channel 4 (main actuator channel)
- Sets LEVEL datapoint to 1.0 (100% = fully open/up)

---

### shutter-control-down.hms
**Purpose:** Closes shutters/blinds (sets LEVEL to 0%)

**Same features as UP script, but sets LEVEL to 0.0 (0% = fully closed/down)**

---

## ⚙️ Configuration Requirements

### 1. CCU Setup

**Assign Functions (Gewerke) to Devices:**
```
CCU WebUI → Settings → Devices & Channels
→ Select device → Functions tab
→ Add to function (e.g., "Shutters-GroundFloor")
```

**Assign Rooms to Devices (optional):**
```
CCU WebUI → Settings → Devices & Channels
→ Select device → Rooms tab
→ Add to room (e.g., "Living Room")
```

### 2. Script Configuration

Edit the configuration section in each script:

```javascript
// Example: Control all shutters in ground floor
string sGewerke = "Shutters-GroundFloor";
string sRaeume = "";  // Empty = all rooms
string sTypen = "HmIP-BROLL,HmIP-BBL";  // Device types
string sExclude = "";  // Exclude specific devices
```

### 3. Testing

**Always test with dry-run first:**
```javascript
boolean bDryRun = true;  // Simulation mode
boolean bDebug = true;   // See what would happen
```

**Then activate for production:**
```javascript
boolean bDryRun = false;  // Execute commands
boolean bDebug = false;   // Less verbose
```

---

## 🎯 Usage Examples

### Example 1: Morning Routine - Open All Ground Floor Shutters

**Script:** `shutters-groundfloor-up.hms`
```javascript
string sGewerke = "Shutters-GroundFloor";
string sRaeume = "";
string sTypen = "HmIP-BROLL";
```

**CCU Program:**
```
Name: Morning - Open Ground Floor Shutters
WHEN: Time is 07:00 (Monday-Friday)
THEN: Execute script: shutters-groundfloor-up.hms
```

---

### Example 2: Evening - Close Bedroom Shutters

**Script:** `shutters-bedroom-down.hms`
```javascript
string sGewerke = "";
string sRaeume = "Bedroom 1,Bedroom 2";
string sTypen = "HmIP-BROLL";
```

**CCU Program:**
```
Name: Evening - Close Bedroom Shutters
WHEN: Time is 22:00
THEN: Execute script: shutters-bedroom-down.hms
```

---

### Example 3: Button Control - Living Room Shutters

**Script UP:** `shutters-living-up.hms`
```javascript
string sGewerke = "";
string sRaeume = "Living Room";
string sTypen = "HmIP-BROLL,HmIP-BBL";
```

**Script DOWN:** `shutters-living-down.hms`
```javascript
// Same config, but rTargetLevel = 0.0
```

**CCU Programs:**
```
Name: Button - Living Room UP
WHEN: Wall Switch "Living Room" → Channel 1 → SHORT_PRESS
THEN: Execute script: shutters-living-up.hms

Name: Button - Living Room DOWN
WHEN: Wall Switch "Living Room" → Channel 2 → SHORT_PRESS
THEN: Execute script: shutters-living-down.hms
```

---

### Example 4: Sun Protection - South Facing Blinds

**Script:** `blinds-south-down.hms`
```javascript
string sGewerke = "Blinds-South";
string sRaeume = "";
string sTypen = "HmIP-BBL";
```

**CCU Program:**
```
Name: Sun Protection - Close South Blinds
WHEN: Brightness Sensor > 10000 lux
AND:  Time between 10:00 and 18:00
THEN: Execute script: blinds-south-down.hms
```

---

## 📁 Recommended Script Organization

Create separate scripts for each control scenario:

```
shutters/
├── shutters-groundfloor-up.hms
├── shutters-groundfloor-down.hms
├── shutters-firstfloor-up.hms
├── shutters-firstfloor-down.hms
├── blinds-office-up.hms
├── blinds-office-down.hms
├── shutters-bedroom-down.hms    (evening only)
└── blinds-south-down.hms         (sun protection)
```

**Why separate scripts?**
- Each CCU program can execute only ONE script
- Easy to maintain and troubleshoot
- Clear naming shows purpose
- Can have different configurations per area

---

## 🔧 Advanced Features

### Exclude Specific Devices

Exclude devices by name (useful for special cases):

```javascript
string sExclude = "Shutter Kitchen,Blind Office Window 2";
```

### Multiple Functions/Rooms

Combine multiple filters:

```javascript
// Control shutters in multiple rooms
string sRaeume = "Living Room,Kitchen,Dining Room";

// Control multiple functions
string sGewerke = "Shutters-GroundFloor,Blinds-GroundFloor";
```

### Control All Devices of a Type

Leave filters empty to control all:

```javascript
string sGewerke = "";  // All functions
string sRaeume = "";   // All rooms
string sTypen = "HmIP-BROLL";  // Only shutters
```

---

## ⚠️ Troubleshooting

**Problem: No devices controlled**
- Check if Functions are assigned in CCU
- Verify device type spelling (case-sensitive)
- Enable `bDebug = true` to see what's happening

**Problem: Some devices not working**
- Check device battery status
- Verify channel 4 exists (should be automatic for shutter actuators)
- Check CCU device log for errors

**Problem: Script executes but nothing happens**
- Ensure `bDryRun = false` (not in simulation mode)
- Check LEVEL datapoint is available
- Verify device is not in manual mode

---

## 📝 Notes

- Scripts only control **Channel 4** (main actuator channel)
- **LEVEL 1.0 = 100% = Fully Open/Up**
- **LEVEL 0.0 = 0% = Fully Closed/Down**
- Intermediate values (0.0-1.0) are possible but not used by these scripts
- Scripts handle duplicates automatically (same device won't be controlled twice)
- German CCU terms: "Gewerke" = Functions/Trades, "Räume" = Rooms

---

## 🔗 Related Scripts

See also:
- `/heating/` - Window-open detection with heating control
- `/security/` - Presence simulation using shutters
- `/examples/` - Template scripts for customization