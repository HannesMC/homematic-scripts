# HomeMatic Scripts

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
├── lighting/           # Light control
├── notifications/      # Alert and notification scripts
├── security/           # Security automation
├── utilities/          # Helper scripts & common functions
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

### 💡 Lighting
Automated light control using motion sensors and twilight detection.

### 🔔 Notifications
Alert scripts for low batteries, open windows, and system events.

### 🔒 Security
Presence simulation and alarm system automation.

### 🛠️ Utilities
Common functions, system variable helpers, and reusable code snippets.

---

## License

This project is licensed under the [**GPL-3.0 License**](LICENSE).  
See the LICENSE file for full details.

---

## Contact

For general questions about HomeMatic or to exchange ideas about home automation, feel free to reach out – but please note that I do not provide support for these scripts.

---

**Note:** These scripts reflect my personal setup and requirements. They may need significant modifications to work in your environment. Always test in a safe manner before deploying to production systems.