# Plan Measure — Windows desktop build

This branch packages the existing Plan Measure web application as a native Windows desktop application using Tauri 2.

## What stays the same

The Plan Measure measuring engine, PDF workflow, calibration, line/polyline/polygon tools, projects, autosave, classifications, exports and local IndexedDB storage are unchanged.

## Offline behaviour

The production application is bundled locally and does not load the Plan Measure website. It works without an internet connection after installation.

The NSIS installer embeds the Microsoft WebView2 offline installer so the app can also be installed on a Windows PC that is offline.

## Installation

GitHub Actions builds two Windows files:

- an NSIS setup `.exe` — recommended
- the raw `plan-measure.exe` application binary

Use the setup EXE. It installs for the current Windows user and does not require an all-users / Program Files install.

The installer is currently unsigned, so Windows SmartScreen may show an Unknown Publisher warning. Code signing can be added later if needed.

## Build on GitHub

Open **Actions → Build Windows Desktop → Run workflow** on the `windows-desktop` branch.

When the build finishes, download the **plan-measure-windows** artifact.

## Local development

Requirements:

- Node.js 24
- Rust stable
- Windows WebView2 development/runtime components

Then run:

```powershell
npm ci
npm install --no-save @tauri-apps/cli@2
npx tauri dev
```

To create the installer:

```powershell
npx tauri build
```

The installer is written to:

```text
src-tauri\target\release\bundle\nsis\
```

## Licence

Plan Measure remains MIT licensed. The original LICENSE file is retained unchanged.
