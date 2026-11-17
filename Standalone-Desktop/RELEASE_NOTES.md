# Flo Desktop 1.0.1 — Release Notes

**Release Tag:** `desktop-v1.0.1`  
**Platform:** Windows 10 / Windows 11 (64-bit x64)  
**Installer:** `Flo-Desktop-Setup.exe`

---

## Dependency-Aware Installer & Prerequisite Verification

Flo Desktop `1.0.1` is a patch release upgrading `Flo-Desktop-Setup.exe` and `FloDesktopUninstall.exe` to automatically detect, verify, and install missing system prerequisites before installing Flo Desktop:

- **Pre-Install System Check (`Checking your system`):** Runs immediately after EULA acceptance and verifies Windows 10/11 x64 (`>= 10.0.18362`), Direct3D 11 hardware adapter (`11_1`–`10_0`), Windows Graphics Capture (`GraphicsCaptureSession::IsSupported()`), Microsoft Visual C++ 2015–2022 Runtime (x64), Media Foundation (`mfplat.dll` / `MFStartup`), Windows N/KN Media Feature Pack (when applicable), and `150 MB` minimum free disk space.
- **Standalone Static-CRT Installer (`/MT`):** `Flo-Desktop-Setup.exe` and `FloDesktopUninstall.exe` have zero `VCRUNTIME140.dll` / `MSVCP140.dll` runtime imports, ensuring setup launches cleanly even when Visual C++ Runtime x64 is absent.
- **Official Microsoft Prerequisite Acquisition & Verification:** Downloads missing Visual C++ Runtime x64 from Microsoft over HTTPS (`https://aka.ms/vs/17/release/vc_redist.x64.exe`), verifies `WinVerifyTrust` and `Microsoft Corporation` Authenticode signature before elevated execution, and installs the Windows Media Feature Pack via `dism.exe` on Windows N editions only. GPU drivers are never auto-installed.
- **Safe Failure, Cancel & Reboot-Resume Handling:** Never proceeds to Flo Desktop installation if a mandatory prerequisite is unsupported, cancelled, or fails; persists `PendingResume` state on `3010` reboot-required without forcing a restart; and preserves existing Flo Desktop recordings and Adobe editions.
- **Version Metadata Alignment:** Updated `FloDesktop.exe`, `Flo-Desktop-Setup.exe`, and `FloDesktopUninstall.exe` version resources to `1.0.1.0` so **About → Check for Updates** accurately reflects the installed `1.0.1` release.

---

# Flo Desktop 1.0.0 — Release Notes

**Release Tag:** `desktop-v1.0.0`  
**Platform:** Windows 10 / Windows 11 (64-bit x64)  
**Installer:** `Flo-Desktop-Setup.exe`

---

## First Public Standalone Desktop Release

Flo Desktop `1.0.0` is the first public release of the standalone native Windows screen recorder. It runs independently without requiring Adobe Photoshop, InDesign, or any Adobe companion software.

### Key Capabilities

- **Native Windows Application:** Built in native C++17 with Direct3D 11, Direct2D, Windows Graphics Capture, Media Foundation, and WASAPI.
- **Monitor Capture:** Record an individual display or combine multiple displays into a single recording.
- **Separate Multi-Display Recording:** Capture multiple connected displays simultaneously as independent MP4 files organised in a session folder.
- **Applications & Games Capture:** Select an active desktop application or game window to record.
- **Custom Region Capture:** Select a custom rectangular screen area on the desktop before starting capture.
- **Recording Modes:** Capture real-time **Normal Video** or frame-sampled **Live Time-Lapse** recordings.
- **H.264 & HEVC Encoding:** Select H.264 or HEVC encoding according to your GPU, driver, and Windows Media Foundation support.
- **Configurable Audio:** Enable and adjust **System Audio** and **Microphone** inputs independently, with selectable AAC audio bitrates.
- **Floating Recording Controls:** Compact capsule recording bar with ready, recording, paused, and saved states plus Quick Settings.
- **Recordings Library & Local Storage:** Browse, search, filter, play, rename, and manage recordings saved locally to your chosen folder.
- **Built-in Online Update Checker:** Use **About → Check for Updates** to check GitHub for newer `desktop-v*` releases and open the official `Flo-Desktop-Setup.exe` download link in your browser.

---

## Verification & Package Integrity

- Verify the downloaded `Flo-Desktop-Setup.exe` against `SHA256SUMS.txt` attached to this release.
- See [README.md](README.md) for installation, system requirements, privacy details, and support contact (`ghoruisubho1999@gmail.com`).
- Use is governed by the [End User License Agreement](EULA.txt).
