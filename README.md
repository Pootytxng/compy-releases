# Compy

**The PC optimizer that shows its receipts.**

Compy reads your PC's hardware and recommends safe, reversible Windows optimizations in plain
English. Every change it applies is snapshotted first, so it can be rolled back.

**[⬇ Download the latest release](https://github.com/Pootytxng/compy-releases/releases/latest)**

> This repository hosts Compy's installers and update manifest. **The source for this software is
> closed.** Bug reports and feature requests are welcome in
> [Issues](https://github.com/Pootytxng/compy-releases/issues).

---

## What it does

- **Reads your actual hardware** — CPU, GPU, memory, storage and network adapter — and tailors its
  recommendations to the machine in front of it, rather than applying a generic checklist.
- **Explains every recommendation in plain English**, including what it changes and why.
- **Snapshots before it changes anything.** Every applied change writes a receipt, and every receipt
  can be rolled back from inside the app.
- **Finds leftovers from other people's tweak guides** — including settings a "disable X for FPS"
  guide changed and never put back — and tells you what it found.
- **Tells you when it has nothing useful to say.** If a reading is unavailable on your hardware,
  Compy says so instead of guessing.

## What it will never do

These are design constraints enforced in the code, not promises in a README:

- **No kernel driver.** Compy installs no driver and requires none.
- **No game injection.** Nothing is injected into any running game. FPS is read from outside the
  game; the overlay is a separate window (borderless/windowed only). That is the anti-cheat design.
  It is not a promise that a given anti-cheat will never notice an overlay or event tracing.
- **No upload of your PC.** Hardware, sessions, and the Trust Ledger stay on your disk. Compy does
  make **one automatic network call:** a signed update check against this repository (see
  **Updates**). That request carries none of your data. GitHub still sees ordinary connection
  metadata such as your IP, under GitHub's terms. You can switch the check off in
  Settings → About. Full wording is in the [Privacy Policy](https://compy-bd6.pages.dev/privacy.html).
- **It will not touch your security.** Windows Defender, the Windows Firewall, the Security Health
  service, Windows Update and the Base Filtering Engine can never be suspended or disabled by Compy.
  That boundary is enforced by a test that names each of those services individually.
- **No irreversible changes.** If Compy cannot describe how to undo something, it does not do it.

## Install

1. Download `Compy_<version>_x64-setup.exe` from the
   [latest release](https://github.com/Pootytxng/compy-releases/releases/latest).
2. Run it. Compy installs for the current user only — **no administrator prompt at install time.**
3. Launch Compy from the Start menu.

Compy asks for administrator permission only at the moment it applies a change that genuinely needs
it, and it tells you which change that is.

### Requirements

- Windows 10 (64-bit) or Windows 11
- The Microsoft Edge WebView2 runtime. It ships with current Windows; if it is missing, the installer
  fetches it from Microsoft during setup, which needs a working internet connection.

### A note on the SmartScreen warning

Compy's installer is **not yet code-signed**, so Windows SmartScreen may warn you that the publisher
is unknown. That warning is about the absence of a paid certificate, not about anything found in the
file. You can verify the download yourself before running it:

```powershell
Get-FileHash .\Compy_0.9.26_x64-setup.exe -Algorithm SHA256
```

`v0.9.26` should return
`4B72D68120F2A2601D87B814ACCDB25C0E18B20AA79ADB63C9040BF9A9294E98`. Each release lists its own
hash on its release page.

## Updates

Compy checks this repository for a newer version when it starts, and about every four hours while it
stays open. The check fetches `latest.json` from GitHub (`github.com`, then GitHub's release-asset
host). It sends no hardware inventory, sessions, or settings.

**Nothing downloads until you choose Update now.** The installer must then verify against the public
key built into Compy. That signature is Compy's own updater key, **not** a Windows Authenticode
publisher certificate — SmartScreen will still warn until the installer is code-signed.

Turn automatic checks off in **Settings → About**. **Check now** in the same row runs a single check
when you ask. Turning checks off never weakens signature verification.

## Uninstall

Settings → Apps → Installed apps → **Compy** → Uninstall. Or run the uninstaller from
`%LOCALAPPDATA%\Compy`.

Rolling back changes and uninstalling are separate things: **roll back your applied changes from
inside Compy before uninstalling** if you want the machine returned to how it was. History stays in
`%APPDATA%\Compy` by design so rollback records survive a reinstall. Delete that folder yourself if
you want everything gone.

## Reporting a problem

Open an [issue](https://github.com/Pootytxng/compy-releases/issues). Please include your Compy
version, your Windows version, and what you expected to happen. Compy can export a diagnostics
bundle for you from Settings — it never attaches anything to a report without you seeing it first.

## Legal

- [End User Licence Agreement](https://compy-bd6.pages.dev/eula.html)
- [Privacy Policy](https://compy-bd6.pages.dev/privacy.html)

Compy is proprietary software. © 2026 Pootytxng. All rights reserved.
