# Flo Desktop 1.0.1 — QA Verification Report

**Release Tag:** `desktop-v1.0.1`  
**Product Version:** `1.0.1.0` (Windows 64-bit x64)  
**Date:** 2026-11-17  
**Installer Binary:** `Flo-Desktop-Setup.exe` (`1,844,736` bytes)

---

## 1. Binary & Version Verification

| Binary | Size (bytes) | FileVersion / ProductVersion | CRT Linkage |
|---|---:|---|---|
| `Flo-Desktop-Setup.exe` | `1,844,736` | `1.0.1.0` | Static (`/MT`) — zero `VCRUNTIME140.dll` / `MSVCP140.dll` imports |
| `FloDesktopUninstall.exe` | `273,920` | `1.0.1.0` | Static (`/MT`) — zero `VCRUNTIME140.dll` / `MSVCP140.dll` imports |
| `FloDesktop.exe` | `1,062,400` | `1.0.1.0` | Dynamic (`/MD`) — requires Visual C++ Runtime x64 |

---

## 2. Automated Prerequisite & Installer Harness (`--test-prereqs`)

Command: `Flo-Desktop-Setup.exe --test-prereqs` → **Exit Code `0`** (`RESULT: ALL PREREQ CHECKS PASSED`)

| # | Scenario | Verification Mode | Result | Notes |
|---|---|---|---|---|
| 1 | All prerequisites already present | Live OS, GPU, WGC, VC++ x64, MF probes | **PASS** | Windows 11 x64 (`Build 26300`), `AMD Radeon RX 6600 (Feature Level 11.0+)`, WGC `Available`, VC++ `v14.51.36247`, MF `Available`, Media Feature Pack `Not Required`; zero redundant installs |
| 2 | Visual C++ Redistributable missing | Controlled `SystemProbeEnv` | **PASS** | `vcredist_x64` flagged `Missing`; Media Feature Pack `Not Required` |
| 3 | Windows N edition with Media Feature Pack missing | Controlled `SystemProbeEnv` (`isWindowsN=true`) | **PASS** | `mf` and `media_pack` flagged `Missing`; targets DISM `Media.MediaFeaturePack~~~~0.0.1.0` |
| 4 | No internet connection | Live WinHTTP against unreachable host | **PASS** | Clean failure (`err=12007`, `ERROR_WINHTTP_NAME_NOT_RESOLVED`) |
| 5 | Download failure | Live WinHTTP HTTP 404 | **PASS** | Clean HTTP `404` rejection; no partial file left behind |
| 6 | Invalid download or signature | Live `VerifyDownloadedInstaller` + live Microsoft download probe | **PASS** | Unsigned dummy PE & mismatched SHA-256 rejected; live `https://aka.ms/vs/17/release/vc_redist.x64.exe` verified `HTTP 200`, `WinVerifyTrust`, `Microsoft Corporation` signer |
| 7 | User cancels UAC | Code inspection (`RunElevatedProcess` `ERROR_CANCELLED`) | **Not executed interactively** | Handled via `ERROR_CANCELLED` in `ShellExecuteExW`; requires interactive desktop UAC prompt |
| 8 | Prerequisite installation failure | Code inspection (`RunElevatedProcess` non-zero exit code) | **Not executed interactively** | Handled for exit codes outside `{0, 1638, 3010, 1641}` without proceeding to Flo install |
| 9 | Restart-required result (`3010`) | Live HKCU `PendingResume` persistence round-trip | **PASS** | Persists resume state without forcing Windows restart |
| 10 | Unsupported Windows version | Controlled `SystemProbeEnv` (`osBuild=17763`) | **PASS** | Blocked cleanly as `Unsupported` |
| 11 | Unsupported GPU capability | Controlled `SystemProbeEnv` (`hasD3D11Gpu=false`) | **PASS** | Blocked cleanly as `Unsupported`; never auto-installs GPU drivers |
| 12 | User cancels before/during prerequisite install | Controlled `cancelFlag=true` + `CleanupTempDownloads()` | **PASS** | Aborts cleanly without installing Flo or leaving temp files |
| 13 | Insufficient disk space | Controlled `SystemProbeEnv` (`20 MB < 150 MB`) | **PASS** | Blocked cleanly before installation |

---

## 3. UI Rendering, Install, Upgrade & Uninstall Verification

- **UI QA Render (`Flo-Desktop-Setup.exe --qa-render`):** Exit Code `0`; rendered `SystemCheck`, missing-prerequisite, and `RebootRequired` screens cleanly.
- **Clean Silent Install (`/S /D=...`):** Exit Code `0`; installed `FloDesktop.exe` (`1.0.1.0`), `FloDesktopUninstall.exe` (`1.0.1.0`), `EULA.txt`, `README.md`, `RELEASE_NOTES.md`, `INSTALLATION_GUIDE.md`, and `THIRD_PARTY_NOTICES.md`.
- **Upgrade Install (`/S /D=...` over existing directory):** Exit Code `0`; preserved existing user recording files cleanly.
- **Silent Uninstall (`FloDesktopUninstall.exe /S`):** Exit Code `0`; removed `FloDesktop.exe` and application files while preserving user recording files.
- **Windows N Live DISM Execution:** Not executed on a live Windows N VM (verified via controlled Windows N probe on this Windows 11 Pro host).
