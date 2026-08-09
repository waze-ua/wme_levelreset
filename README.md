# WME Relock

[![Version](https://img.shields.io/badge/version-2026.08.04.001-blue.svg)](https://github.com/waze-ua/wme_relock)
[![Waze Map Editor](https://img.shields.io/badge/Waze-Map%20Editor-33CCFF.svg)](https://www.waze.com/editor)
[![Userscript](https://img.shields.io/badge/userscript-Tampermonkey-green.svg)](https://www.tampermonkey.net/)
[![GitHub](https://img.shields.io/github/stars/waze-ua/wme_relock?style=flat\&logo=github)](https://github.com/waze-ua/wme_relock)

**WME Relock** is a userscript for **Waze Map Editor (WME)** that helps editors find and correct incorrect lock levels on roads and Places according to country- and city-specific rules.

The script continuously scans the current map area, identifies objects whose lock level does not match the configured rules, and provides tools to review and relock them quickly.

---

## ✨ Features

* 🔍 **Automatic lock-level detection**

  * Scans the visible map area for objects with incorrect lock levels.
  * Automatically updates when the map changes.

* 🔒 **Automatic relocking**

  * Apply the recommended lock level to selected objects.
  * Use **Relock All** to process all detected objects.

* 🌍 **Country-specific rules**

  * Different lock-level rules can be configured for different countries.

* 🏙️ **City-specific rules**

  * Individual cities can override the default country rules.

* 🛣️ **Road type support**

  * Supports the main Waze road types.
  * Each road type can have its own lock-level rule.

* 📍 **Places support**

  * Lock levels for Places can also be checked and corrected.

* 🚦 **Routing road type awareness**

  * Optional **Respect routing road type** mode allows the script to take the routing classification into account.

* 🔓 **Higher lock-level detection**

  * Optional **Also relock higher locked objects** mode allows already locked objects with a higher-than-required level to be included.

* ☑️ **Selective processing**

  * Enable or disable individual road/Place types.
  * Quickly enable or disable all types.

* 📊 **Live statistics**

  * Shows how many incorrectly locked objects were found for each type.

* ⚡ **Bulk processing**

  * Relock multiple objects in one operation.
  * Displays operation progress.

* 💾 **Persistent settings**

  * User preferences are saved locally and restored after restarting WME.

* 🧩 **Modern WME integration**

  * Uses the official WME SDK.
  * Does not require jQuery.

---

## 📦 Installation

### Requirements

You need a userscript manager such as:

* [Tampermonkey](https://www.tampermonkey.net/)
* Any other userscript manager compatible with WME userscripts

### Install from Greasy Fork

The recommended installation method is **Greasy Fork**:

**[Install WME Relock](https://greasyfork.org/scripts/457554/wme-relock)**

### Install directly from GitHub

You can also install the latest development version directly from the repository:

**[wme-relock.user.js](https://github.com/waze-ua/wme_relock/blob/master/wme-relock.user.js)**

After installation, open:

**[Waze Map Editor](https://www.waze.com/editor)**

The Relock panel will be added automatically.

---

## 🚀 Usage

After opening WME, the **Relock** panel will appear in the editor interface.

The script automatically scans the current map area and displays objects whose lock level differs from the configured rules.

### Bad locks found

The **Bad locks found** section contains the detected objects grouped by type.

For each type, the script displays the number of objects that can be relocked.

Use the checkboxes to select which types should be processed.

You can also enable or disable all available types at once.

---

## 🔍 Automatic Scanning

WME Relock automatically updates its results when relevant changes occur in the editor, including:

* moving the map;
* changing the zoom level;
* editing map objects;
* cancelling edits.

This means that there is normally no need to manually start a new scan.

---

## 🔒 Relock All

The **Relock All** button applies the recommended lock levels to all selected objects detected by the scanner.

Objects are processed sequentially and the interface displays the current progress.

After the operation is completed, the map is scanned again so that the results reflect the current state.

> ⚠️ **Use this feature carefully.**
> Lock levels may have intentional local exceptions. Always review the detected objects before performing large-scale changes.

---

## 🚦 Respect routing road type

The **Respect routing road type** option allows WME Relock to consider the road type used for routing when determining the appropriate lock level.

This can be useful when the physical road classification and the routing classification do not completely match.

---

## 🔓 Also relock higher locked objects

The **Also relock higher locked objects** option includes objects that already have a lock level higher than the recommended level.

For example, if the configured rule requires lock level `3`, an object locked at level `4` or higher can also be reported.

This option is disabled by default.

> ⚠️ **Use with caution.**
>
> A higher lock level may be intentional because of a local exception, an important road, a complex junction, or another editing policy.

The availability of this option also depends on the editor's WME permissions.

---

## 🌍 Lock Level Rules

Lock-level rules are separated from the main userscript logic.

Rules can be defined for:

* countries;
* cities;
* road types;
* Places.

This makes it possible to adapt WME Relock to local editing standards without changing the core scanning and processing logic.

### Example

A simplified rule set could look like:

| Object type    | Example lock level |
| -------------- | -----------------: |
| Street         |                  1 |
| Primary Street |                  1 |
| Minor Highway  |                  2 |
| Major Highway  |                  3 |
| Ramp           |                  4 |
| Freeway        |                  4 |
| Place          |                  1 |

> The actual values depend on the rules configured for the relevant country and city.

---

## 🏙️ City-specific Rules

A city can have its own lock-level rules that override the default country configuration.

This allows local Waze communities to define exceptions for areas where different editing practices are required.

For example:

```text
Country
 ├── Default rules
 │
 └── City
      ├── Street → custom lock level
      ├── Primary Street → custom lock level
      └── Highway → custom lock level
```

---

## 💾 Settings

User preferences are stored locally in the browser using `localStorage`.

The following settings are preserved between sessions:

* selected road/Place types;
* **Respect routing road type**;
* **Also relock higher locked objects**;
* information/warning panel state.

You do not need to configure the script again after restarting WME.

---

## ⚙️ Processing Limits

To avoid excessive operations in large map areas, the scanner limits the number of objects processed per type and pass.

Currently, up to **150 objects per type/pass** can be handled in one operation.

If more objects are found, run the operation again after the first batch has been processed.

---

## ⚠️ Important

WME Relock is an **automation and assistance tool**. It does not replace knowledge of local Waze editing rules.

Do not blindly relock every object reported by the script.

Always consider:

* local exceptions;
* important or strategic roads;
* manually protected objects;
* complex junctions and interchanges;
* special routing situations;
* objects intentionally assigned a higher lock level.

The **Relock All** function should be used only when you understand the applicable local rules.

---

## 🧩 Technical Details

| Property        | Value                                           |
| --------------- | ----------------------------------------------- |
| Platform        | Waze Map Editor                                 |
| Type            | Userscript                                      |
| JavaScript      | ES2021+                                         |
| API             | WME SDK                                         |
| jQuery          | Not required                                    |
| Storage         | Browser `localStorage`                          |
| Compatible with | Tampermonkey and compatible userscript managers |

---

## 🏗️ Project Structure

The repository contains the userscript and supporting rule/configuration files.

The general architecture separates:

1. **WME integration**
2. **Map object detection**
3. **Lock-level calculation**
4. **Country/city rules**
5. **User interface**
6. **Bulk relocking**
7. **User preferences**

This separation makes it possible to update local rules without changing the core relocking logic.

---

## 🤝 Contributing

Contributions are welcome!

If you would like to improve WME Relock, you can:

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Test the userscript in WME.
5. Create a Pull Request.

### Adding or changing rules

If you want to add support for a new country or city, or change existing lock-level rules, please make sure that the proposed values follow the applicable local Waze editing guidelines.

For rule-related changes, include a short explanation of:

* the affected country/city;
* the affected road or Place type;
* the current rule;
* the proposed rule;
* the reason for the change.

---

## 🐛 Bug Reports

If you find a bug, please create a GitHub Issue:

**[Report a bug](https://github.com/waze-ua/wme_relock/issues/new)**

When reporting a problem, please include:

* browser and version;
* userscript manager;
* WME environment;
* WME Relock version;
* country/city where the issue occurred;
* object type;
* steps to reproduce the problem;
* screenshots or console errors, if available.

---

## 💡 Feature Requests

Have an idea for improving WME Relock?

Open a **[Feature Request](https://github.com/waze-ua/wme_relock/issues/new)** and describe:

* what you would like the script to do;
* why the feature is useful;
* an example of the current problem;
* an example of the expected behavior.

---

## 📜 History

WME Relock originated as a fork of **WME LevelReset** by Broos Gert (2015).

Since then, the project has been substantially modified and extended with:

* country-specific rules;
* city-specific rules;
* Place support;
* additional road types;
* automatic scanning;
* persistent settings;
* bulk relocking;
* progress reporting;
* routing road type support;
* higher-lock detection;
* modern WME SDK integration;
* removal of the jQuery dependency;
* improved error handling and user interface.

---

## 📄 License

See the repository for the current license and copyright information.

---

## 🔗 Links

* **[GitHub Repository](https://github.com/waze-ua/wme_relock)**
* **[WME Relock on Greasy Fork](https://greasyfork.org/scripts/457554/wme-relock)**
* **[Waze Map Editor](https://www.waze.com/editor)**
* **[WME SDK Documentation](https://www.waze.com/editor/sdk/)**
* **[Report an Issue](https://github.com/waze-ua/wme_relock/issues)**

---

## 👤 Maintainer

Maintained by the **Waze Ukraine community**.

For questions regarding local rules or contributions, please use the GitHub repository and issue tracker.
For adding your country settings contact Sapozhnik (coordinator and Global Champ of Ukraine community)


---

⭐ If you find **WME Relock** useful, consider giving the project a star on GitHub.
