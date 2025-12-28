# HomeMatic Scripts

🇬🇧 English | [🇩🇪 Deutsch](README_de.md)

This repository serves as a **personal collection** of my HomeMatic scripts for various home automation tasks.

> [!WARNING]
> 🚨 **Disclaimer:** These scripts were created for my personal use and are provided "as is" without any warranty.  
> **Use at your own risk.** The author assumes no responsibility for any issues arising from their usage.

---

## About This Repository

- ✅ **Publicly available** – Anyone can view and use these scripts
- ⛔ **No active maintenance** – Updates are made as needed without a schedule
- ⛔ **No support** – This repository serves solely as a personal archive
- ⛔ **No issues/pull requests** – These are personal scripts without community development

If you find these scripts useful, feel free to adapt them to your needs. However, please understand that I cannot provide support or accept contributions.

---

## Structure

Scripts are organized by use case:

```
├── shutters/           # Roller shutter control
├── heating/            # Heating automation
├── lighting/           # Light control
├── notifications/      # Alert and notification scripts
├── security/           # Security automation
├── utilities/          # Helper scripts & common functions
└── examples/           # Example configurations
```

---

## Usage

1. Select a script and copy its code
2. Paste into HomeMatic CCU (Programs & Links → Script)
3. Adapt variables and device IDs to your environment
4. Test thoroughly before using in production

---

## Important Notes

- All scripts are developed for **HomeMatic IP** / **HomeMatic CCU3**
- Device IDs and channel numbers must be adjusted
- Some scripts require system variables to be created
- Time schedules and thresholds are individual and need customization
- Scripts use German variable names and comments (legacy from my setup)

---

## Technical Requirements

- HomeMatic CCU3 (or compatible)
- HomeMatic IP devices
- Basic understanding of HomeMatic scripting (HM-Script/TCL)
- Familiarity with your device addresses and channels

---

## Script Categories

### 🪟 Shutters
Automated roller shutter control based on time, sun position, or weather conditions.

**Documentation:** [shutters/README.md](shutters/README.md) | [🇩🇪 German](shutters/README_de.md)

**Example Scripts:**
- Time-based control (up/down)
- Sun position-based control
- Wind protection automation

---

### 🔥 Heating
Temperature control and optimization based on window states and presence.

**Documentation:** [heating/README.md](heating/README.md) | [🇩🇪 German](heating/README_de.md)

**Example Scripts:**
- Window-open detection (automatically turn off heating)
- Night setback
- Presence-based control

---

### 💡 Lighting
Automated light control using motion sensors and twilight detection.

**Documentation:** [lighting/README.md](lighting/README.md) | [🇩🇪 German](lighting/README_de.md)

**Example Scripts:**
- Twilight automation
- Motion sensor-based lighting
- Stairway timer

---

### 🔔 Notifications
Alert scripts for low batteries, open windows, and system events.

**Documentation:** [notifications/README.md](notifications/README.md) | [🇩🇪 German](notifications/README_de.md)

**Example Scripts:**
- Low battery warnings
- Window-left-open reminders
- Alarm notifications

---

### 🔒 Security
Presence simulation and alarm system automation.

**Documentation:** [security/README.md](security/README.md) | [🇩🇪 German](security/README_de.md)

**Example Scripts:**
- Presence simulation (randomized light/shutter control)
- Alarm activation

---

### 🛠️ Utilities
Common functions, system variable helpers, and reusable code snippets.

**Documentation:** [utilities/README.md](utilities/README.md) | [🇩🇪 German](utilities/README_de.md)

**Example Scripts:**
- System variable management
- Common functions
- Logging helpers

---

## Getting Started

### 1. Navigate to the desired category
Choose a folder based on your use case (e.g., `shutters/` for roller shutter control).

### 2. Read the documentation
Each folder contains a `README.md` with:
- Detailed explanation of the scripts
- Prerequisites and required CCU configuration
- Usage examples
- Troubleshooting tips

### 3. Customize the script
- Copy the script into CCU
- Adjust device IDs, functions, and rooms
- Test with `bDryRun = true` (simulation mode)
- Activate for production use

### 4. Create CCU programs
Scripts don't run automatically - you must create CCU programs:

```
WHEN: [Trigger - e.g., button, time, sensor]
THEN: Execute script: [your-script.hms]
```

---

## Frequently Asked Questions (FAQ)

### Why don't scripts execute automatically?
HomeMatic scripts are passive actions. You must create CCU programs that execute the scripts on specific events (buttons, time, sensors).

### Why do I need multiple scripts?
Each CCU program can execute only ONE script. For maximum flexibility (different areas, different actions) you need separate scripts.

### How do I find my device IDs?
In CCU: **Settings → Devices & Channels** → Click on a device → Channel IDs are displayed.

### What are "Functions" (Gewerke)?
"Functions" (German: "Gewerke" or "Trades") are CCU-internal groupings of devices by function (e.g., "Shutters-GroundFloor", "Heating-FirstFloor"). You can assign them under **Settings → Devices & Channels**.

### Do the scripts work with CCU2?
Most scripts should work but are optimized for CCU3 with HomeMatic IP. Test with `bDryRun = true` first.

---

## Best Practices

### ✅ Recommended Workflow:

1. **Always test with dry-run first**
   ```javascript
   boolean bDryRun = true;  // Simulation
   boolean bDebug = true;   // Show output
   ```

2. **Name scripts meaningfully**
   ```
   ❌ Bad: script1.hms, test.hms
   ✅ Good: shutters-groundfloor-up.hms, heating-bedroom-auto.hms
   ```

3. **Document customizations**
   Add comments in the script when changing values:
   ```javascript
   string sGewerke = "Shutters-GroundFloor";  // Ground floor only, not first floor
   ```

4. **Regular backups**
   Export your scripts from CCU regularly.

5. **Version control**
   Use Git/GitHub to track changes.

---

## Troubleshooting

### Problem: "Function not found"
**Solution:** Check exact spelling in CCU (case-sensitive!)

### Problem: Script runs but nothing happens
**Solution:** 
- Check `bDryRun = false` (not in simulation mode)
- Enable `bDebug = true` and check logs
- Verify devices are online

### Problem: Only some devices are controlled
**Solution:**
- Check if all devices are assigned to the function
- Verify device type filter (`sTypen`)
- Check exclusion list (`sExclude`)

---

## License

This project is licensed under the [**GPL-3.0 License**](LICENSE).  
See the LICENSE file for full details.

---

## Contact

For general questions about HomeMatic or to exchange ideas about home automation, feel free to reach out – but please note that I do not provide support for these scripts.

---

## Acknowledgments

- **HomeMatic/eQ-3** for the flexible smart home system
- **HomeMatic Community** for countless inspirations and support
- **Everyone using these scripts** – Good luck with your automation!

---

**Note:** These scripts reflect my personal setup and requirements. They may need significant modifications to work in your environment. Always test in a safe manner before deploying to production systems.