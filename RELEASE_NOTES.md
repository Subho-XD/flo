# Flo 2.0.1 Release Notes

**Product:** Flo  
**Version:** 2.0.1 (Universal Distribution Milestone)  
**Release Date:** November 11, 2026  
**Platform:** Windows 10/11 (64-bit)  
**Supported Adobe Applications:** Adobe Photoshop & Adobe InDesign (2024–2026)  

---

## Highlights & Key Enhancements

### 1. Photoshop Secondary-Window & Dialog Capture
- **Comprehensive Dialog Inclusion:** Resolved missing Photoshop-owned pop-up dialogs (Color Picker, Layer Style & Blending Options dialogs, context menus, and tool utility windows) during recording sessions.
- **Direct3D 11 Pipeline Integration:** Configured Windows Graphics Capture session with `IncludeSecondaryWindows(true)`. Secondary and modal windows owned by Photoshop are composited directly into the Direct3D 11 frame pool, producing complete workflow recordings.

### 2. InDesign Non-Interfering Passive Recording & Stability
- **Focus Preservation:** Eliminated keyboard focus-stealing when opening or restoring the floating toolbar. Uses `ShowWindow(SW_SHOWNOACTIVATE)` and `SWP_NOACTIVATE` so active text editing, typography formatting, and object manipulation remain uninterrupted.
- **Smooth Creative Flow:** Disabled aggressive idle-pause during text typing and layout adjustments.
- **Optimized Event Subscriptions:** Pruned noisy DOM event listeners (`afterContextChanged`) in the InDesign UXP plugin, replacing them with a passive 2-second heartbeat observer for live document metadata.

### 3. Per-Monitor High-DPI Display Scaling
- **Adaptive Layout Rendering:** Fully responsive Direct2D vector UI across 100% (96 DPI), 125% (120 DPI), 150% (144 DPI), 175% (168 DPI), and 200% (192 DPI).
- **Dynamic Monitor Migration:** Handles `WM_DPICHANGED` messages to recalculate window bounds and Direct2D render targets on the fly when moved between displays with mismatched scaling.
- **Zero UI Clipping:** Floating toolbar physical dimensions scale proportionally with monitor DPI while drawing targets remain in logical 96-DPI device-independent pixels (DIPs), completely eliminating edge truncation.
- **Sub-Pixel Hit Testing:** Cursor hit-testing converts physical coordinates to DIPs for accurate button clicks and menu interactions.

### 4. Custom Region Capture Precision
- **1:1 Physical Pixel Capture:** Preserves guaranteed 1:1 physical capture pixels for Windows Graphics Capture (WGC) direct GPU texture cropping.
- **Independent Visual HUD:** Floating control pill, dimension badge ("W × H px"), and action controls scale visually with monitor DPI without altering underlying recording coordinates.

### 5. Flo UI Capture Exclusion
- **Automatic Interface Exclusion:** Enables `WDA_EXCLUDEFROMCAPTURE` on all Flo-owned windows (expanded toolbar, compact toolbar, confirmation dialogs, and custom region overlay).
- **Clean Exported Video:** The Flo interface remains fully visible and interactive on your desktop, but is excluded from the exported MP4 recording.

### 6. Hardware-Accelerated H.264 MP4 Export
- **Media Foundation GPU Encoding:** Leverages hardware MFT video encoders (NVIDIA NVENC, Intel Quick Sync, AMD VCE/AMF) for low-overhead screen capture.
- **Configurable Bitrates:** Supports 35 Mbps, 40 Mbps, 45 Mbps, and 50 Mbps presets.
- **Live Timelapse:** Captures workflow frames at intervals from 250ms to 5s.

---

## Distribution Packages & Installation Options

Flo 2.0.1 is distributed through three primary installation methods:

1. **Flo_Setup.exe (Recommended Unified Installer):**
   - Direct2D hardware-accelerated Win32 setup wizard.
   - Automatically detects installed Adobe Photoshop and Adobe InDesign versions.
   - Provisions Flo Native Companion to `%LOCALAPPDATA%\Flo\bin\` and registers Adobe UXP plugins via Adobe UPIA (`UnifiedPluginInstallerAgent.exe`).
   - Clean uninstaller registered in Windows Installed Apps, preserving user-recorded videos.

2. **Flo_Photoshop.ccx (Independent Photoshop Extension):**
   - Standalone UXP Hybrid Addon package for Adobe Photoshop.
   - Embeds native Direct3D 11 / Windows Graphics Capture runtime (`creative_recorder_addon.uxpaddon`).
   - Installs via Adobe Creative Cloud desktop or UPIA.

3. **Flo_InDesign.ccx & Flo_InDesign_Companion_Setup.exe (Independent InDesign Extension):**
   - Standalone UXP Extension for Adobe InDesign.
   - **Prerequisite:** InDesign requires the native companion runtime (`Flo_InDesign_Companion_Setup.exe`) to perform screen recording and Direct3D compositing.

---

## Release Asset Checksums (SHA-256)

| Asset File | Size (Bytes) | SHA-256 Checksum |
| :--- | :--- | :--- |
| `Flo_Setup.exe` | 1,215,488 | `e30c18956270f52348b93791a3b4a4e53710b22e8e8a3737248b4d9846655d0c` |
| `Flo_Photoshop.ccx` | 163,790 | `34aea729cd308436e151d602e498f76f3794b8e439ba74975360633909af2457` |
| `Flo_InDesign.ccx` | 12,344 | `5a1528260d2a874d4c23a27513b0913073be9735e52cfcb7c8b0b56f8c4f7afa` |
| `Flo_InDesign_Companion_Setup.exe` | 815,616 | `4cdda4153951564d6c7cdd5de0ae4dedddc70b2841323bfdecc4e3eee6143e50` |
