<p align="center">
  <img src="assets/flo-logo.svg" width="96" height="96" alt="Flo Logo" />
</p>

# Flo

**A straightforward way to record your creative workflow.**

Flo is a high-performance Windows screen recorder tailored specifically for creative professionals working in Adobe Photoshop and Adobe InDesign. Capture your design sessions, produce silky-smooth 60 FPS walkthroughs, or compress hours of detailed creative work into shareable timelapses—all through a compact, non-intrusive floating toolbar that stays neatly above your workspace.

[![Platform](https://img.shields.io/badge/Platform-Windows%2064--bit-blue.svg)](#system-requirements)
[![Adobe Photoshop](https://img.shields.io/badge/Adobe%20Photoshop-2024--2026-31A8FF.svg)](#supported-adobe-applications)
[![Adobe InDesign](https://img.shields.io/badge/Adobe%20InDesign-2024--2026-FF3366.svg)](#supported-adobe-applications)
[![Latest Release](https://img.shields.io/badge/Release-v2.0.2-22C55E.svg)](https://github.com/Subho-XD/flo/releases/tag/v2.0.2)
[![Pricing](https://img.shields.io/badge/Pricing-No%20Subscription-22C55E.svg)](#licensing)
[![License](https://img.shields.io/badge/License-Proprietary%20EULA-orange.svg)](#licensing)

---

## Why Flo?

Recording a creative workflow shouldn't turn into a complicated workflow of its own.

Most general-purpose screen recorders are built for gaming or software demonstrations. They require clunky multi-monitor setups, struggle with color accuracy on high-contrast artwork, clutter your canvas with heavy overlays, and often stamp unwanted watermarks or force ongoing monthly subscriptions.

**Flo was designed from the ground up for designers:**
- **In-Application Workflow:** Flo opens directly from your Adobe `Plugins` menu. No separate external recording app to launch, configure, or manage.
- **Zero Distraction:** Flo floats above your active document, automatically hiding when you switch to your browser, email, or chat, and reappearing as soon as you return to your canvas.
- **Flawless Motion & Color:** Hardware-accelerated Direct3D 11 capture and subpixel ClearType filtering ensure sharp typography, authentic artwork colors, and zero horizontal tearing—even when moving shapes at high speeds.
- **No Watermarks, Local Storage:** Your work belongs entirely to you. Flo never embeds branding, watermarks, or sponsor tags into exported MP4 videos.

---

## Key Features

- **Direct Adobe Integration:** Seamlessly launch and control recordings directly from Photoshop and InDesign menus.
- **Entire Application Capture:** Record your full host application window, including top menus, floating utility panels, and modal pop-ups (such as Color Picker and Layer Styles).
- **Custom Region Capture:** Interactively draw an exact rectangular capture area anywhere on your canvas with live dimension readouts and 1:1 physical pixel precision.
- **Smooth 60 FPS Normal Recording:** Capture real-time brush strokes, vector adjustments, and typographic layouts with constant frame-rate (CFR) fidelity.
- **Live Workflow Timelapse:** Automatically condense long creative sessions into concise video recaps with customizable intervals (250ms, 500ms, 1s, 2s, and 5s).
- **Intelligent Inactivity Auto-Pause (5 Seconds):** Stop worrying about pausing when stepping away. Flo automatically pauses after 5 seconds of inactivity and instantly resumes the moment you touch your canvas, pen tablet, or keyboard.
- **Broadcast-Grade H.264 MP4 Output:** High-bitrate export presets (35 Mbps, 40 Mbps, 45 Mbps, and 50 Mbps) ready for instant playback or importing into Adobe Premiere Pro and After Effects.
- **GPU-Accelerated Performance:** Powered by Windows Graphics Capture (WGC) and Media Foundation hardware encoders (NVENC, Intel Quick Sync, AMD AMF) for minimal CPU load.
- **Floating Controls (Expanded & Compact):** Effortlessly switch between a detailed setup card ($460 \times 280\text{ px}$) and an ultra-minimal recording strip ($360 \times 44\text{ px}$) that never steals keyboard focus.
- **Optional Audio Commentary:** Capture clean system audio or voice commentary alongside your video.
- **Local-First Privacy:** All videos are saved directly to your local computer. No cloud uploads, accounts, or telemetry tracking your creative content.

---

## Supported Adobe Applications

| Application | Version Support | Integration Architecture | Availability |
| :--- | :--- | :--- | :---: |
| **Adobe Photoshop** | 2024 (v25.x), 2025 (v26.x), 2026 (v27.x+) | UXP Hybrid Addon (`.uxpaddon`) | **Available Now** |
| **Adobe InDesign** | 2024 (v19.x), 2025 (v20.x), 2026 (v21.x+) | UXP Extension + Native Companion Bridge | **Available Now** |
| **Adobe Premiere Pro** | — | Native UXP Extension | *Planned* |
| **Adobe After Effects** | — | Native UXP Extension | *Planned* |
| **Adobe Illustrator** | — | Native UXP Extension | *Planned* |

> [!NOTE]  
> Available integrations are thoroughly validated on Windows 10 and Windows 11 across Adobe 2024, 2025, and 2026 releases. Integrations marked as *Planned* are actively undergoing architectural research aligned with Adobe's UXP roadmap.

---

## Recording Modes & Controls

Flo provides two intuitive capture sources and two recording styles:

### 1. Capture Sources

```text
┌──────────────────────────────────────┐  ┌──────────────────────────────────────┐
│       Entire Application Mode        │  │         Custom Region Mode           │
│                                      │  │                                      │
│  Captures full application window,   │  │  Interactively drag a selection box  │
│  including menu bars, floating tool  │  │  over your artwork. Full canvas is    │
│  palettes, layers, and dialogs.      │  │  visible with 1:1 pixel precision.   │
└──────────────────────────────────────┘  └──────────────────────────────────────┘
```

- **Entire Application:** Captures your complete Photoshop or InDesign window. Windows Graphics Capture ensures native dialogs (Color Picker, Layer Styles, File Place dialogs) are composited cleanly into the recording.
- **Custom Region:** Select an arbitrary rectangular area on your screen. The interactive translucent overlay features 8 resize handles, live width/height dimension badges, and an Enter/Space shortcut to confirm. Areas outside your selection are softly dimmed so you can frame your artwork accurately.

### 2. Recording Styles

- **Normal Video (60 FPS):** Records a smooth, real-time video of your process at 60 constant frames per second. Ideal for tutorials, client reviews, and portfolio walkthroughs.
- **Live Timelapse:** Captures workflow frames at structured intervals, assembling a high-speed timelapse directly during recording:
  - `250 ms` interval $\to$ **$7.5\times$ acceleration**
  - `500 ms` interval $\to$ **$15\times$ acceleration**
  - `1 s` interval $\to$ **$30\times$ acceleration**
  - `2 s` interval $\to$ **$60\times$ acceleration**
  - `5 s` interval $\to$ **$150\times$ acceleration**

### 3. Floating Toolbar Controls

```text
┌────────────────────────────────────────────────────────────────────────┐
│  ● REC  00:04:12  │  Document: Branding_Guidelines.indd  │ [ ⏸ ] [ ⏹ ] │
└────────────────────────────────────────────────────────────────────────┘
```

- **Compact Mode:** A slim, 44-pixel strip showing elapsed recording time, active document name, audio level meter, and quick Pause/Resume/Stop controls.
- **Expanded Mode:** Full configuration panel to change capture mode, bitrate preset, timelapse interval, or audio input before starting your session.
- **Automatic Smart Visibility:** Flo attaches cleanly to your Adobe workspace. When you switch to another application, Flo hides automatically to keep your desktop tidy, reappearing as soon as you click back into Photoshop or InDesign.

---

## System Requirements

- **Operating System:** Windows 10 64-bit (version 1903, build 18362 or later) or Windows 11 64-bit.
- **Processor:** Intel Core i5 / AMD Ryzen 5 or higher (x64 native architecture).
- **Graphics Card:** Direct3D 11-capable GPU with hardware H.264 video encoding support:
  - NVIDIA GeForce GTX 900 series or newer (NVENC)
  - Intel HD Graphics 5000 / Iris / UHD / Xe Graphics or newer (Quick Sync)
  - AMD Radeon RX 400 series or newer (AMF/VCE)
- **Adobe Host Application:**
  - Adobe Photoshop 2024 (v25.x), 2025 (v26.x), or 2026 (v27.x+)
  - Adobe InDesign 2024 (v19.x), 2025 (v20.x), or 2026 (v21.x+)
- **Visual C++ Runtime:** Microsoft Visual C++ 2015–2022 Redistributable x64 (`vcruntime140.dll`). *(Included automatically with Windows updates and installer).*
- **Windows N Editions Note:** Windows N editions lack media codecs by default. Install the free [Windows Media Feature Pack](https://support.microsoft.com/en-us/windows/media-feature-pack-for-windows-10-11-n-n-edition-89f41744-8d48-8df0-7634-1c21d8b67272) via Windows Settings $\to$ System $\to$ Optional features.

---

## Installation & Setup

Choose the installation option that best fits your workflow:

### Option 1 — Recommended: Unified Windows Installer

> **Download:** [**Flo_Setup.exe**](https://github.com/Subho-XD/flo/releases/latest/download/Flo_Setup.exe)  
> *Best for users with Photoshop, InDesign, or both.*

1. Download and run `Flo_Setup.exe`.
2. Accept the software agreement.
3. The setup wizard automatically discovers your installed Adobe applications.
4. Click **Install Flo**. The installer registers the plugins with Adobe Creative Cloud via UPIA and configures all required background runtime components.
5. Launch Photoshop or InDesign, go to `Plugins -> Flo`, and start recording.

---

### Option 2 — Photoshop-Only Extension

> **Download:** [**Flo_Photoshop.ccx**](https://github.com/Subho-XD/flo/releases/latest/download/Flo_Photoshop.ccx)  
> *Standalone UXP hybrid plugin for Photoshop.*

1. Download `Flo_Photoshop.ccx`.
2. Double-click `Flo_Photoshop.ccx` to install via Adobe Creative Cloud desktop, or install from the terminal using Adobe's UPIA agent:
   ```cmd
   UnifiedPluginInstallerAgent.exe /install Flo_Photoshop.ccx
   ```
3. Open Adobe Photoshop.
4. Go to `Plugins -> Flo` to display the recording toolbar.

---

### Option 3 — InDesign-Only Extension & Companion Runtime

> **Downloads:**  
> 1. [**Flo_InDesign_Companion_Setup.exe**](https://github.com/Subho-XD/flo/releases/latest/download/Flo_InDesign_Companion_Setup.exe) (Native Companion Runtime)  
> 2. [**Flo_InDesign.ccx**](https://github.com/Subho-XD/flo/releases/latest/download/Flo_InDesign.ccx) (InDesign Extension)

1. Run `Flo_InDesign_Companion_Setup.exe` to deploy the background capture runtime.
2. Double-click `Flo_InDesign.ccx` to install the extension into InDesign.
3. Open Adobe InDesign.
4. Go to `Plugins -> Flo -> Open Flo` to connect to the companion and display the toolbar.

---

## Basic Usage Guide

### Starting a Recording

1. Open your creative document in Adobe Photoshop or Adobe InDesign.
2. Navigate to the top application menu:
   - **In Photoshop:** Click `Plugins -> Flo`
   - **In InDesign:** Click `Plugins -> Flo -> Open Flo`
3. The Flo toolbar will appear floating above your document.
4. Choose your **Capture Source** (`Entire Application` or `Custom Region`).
5. Choose your **Recording Style** (`Normal Video` or `Live Timelapse`).
6. Click the crimson **Start Recording** button.
7. The toolbar smoothly collapses into compact mode and displays your active recording duration.

### Selecting a Custom Region

1. Click `Custom Region` on the Flo toolbar.
2. If you want to change the region, click the `[ Change ]` button.
3. A translucent guide will appear over your screen.
4. Click and drag to define the exact box around your artwork.
5. Use the 8 perimeter handles to adjust your bounds, and press <kbd>Enter</kbd> or click `Confirm` on the floating HUD badge.
6. Click **Start Recording** to begin capturing only that region.

### Pausing & Resuming

- **Manual Pause:** Click the `Pause` button `[ ⏸ ]` on the compact toolbar to temporarily suspend recording. Click `Resume` `[ ▶ ]` to continue.
- **Inactivity Auto-Pause:** When you stop interacting with your document for **5 seconds** (e.g., answering a call or stepping away), Flo automatically pauses your session. As soon as you move your mouse on the canvas, use your drawing stylus, or press a shortcut key, Flo instantly resumes.

### Stopping & Saving

1. Click the `Stop` button `[ ⏹ ]` on the toolbar.
2. Flo immediately finalizes the MP4 file and saves it cleanly to your computer.
3. A brief status message confirms the filename and saved location.

---

## Output Format & Recording Storage

Flo operates with a strict local-first privacy policy. All videos are saved directly to your local computer:

```text
%USERPROFILE%\Videos\Creative Workflow Recorder\
```

- **File Format:** Universally compatible **H.264 MP4** video.
- **Filename Convention:** Named dynamically after your active document and timestamp:
  ```text
  DocumentName_Recording_YYYYMMDD_HHMMSS.mp4
  ```
- **Editor Compatibility:** Drop recordings directly into Adobe Premiere Pro, After Effects, DaVinci Resolve, or share them directly on YouTube, Vimeo, and social platforms.

---

## Current Limitations & Known Issues

- **Windows Platform Exclusivity:** Flo utilizes hardware-accelerated Windows Graphics Capture (WGC) and Direct3D 11 compositing, making it exclusive to Windows 10 and Windows 11. macOS is not currently supported.
- **Windows N Editions:** Windows N editions require the free Microsoft Windows Media Feature Pack to supply essential Media Foundation encoder libraries.
- **Multi-Monitor DPI Differences:** When selecting a Custom Region across multiple monitors with drastically different display scaling (e.g., 100% on one monitor and 200% on another), region selection is optimized for the display containing the primary application window.
- **Audio Capture Scope:** Audio recording currently captures system audio (computer playback) or default microphone input. Multi-track separate channel audio routing is planned for a future update.

---

## Future Roadmap

- [x] **Adobe Photoshop Integration** *(Available in v1.2.x+)*
- [x] **Adobe InDesign Integration** *(Available in v2.0.x+)*
- [x] **Hardware-Accelerated 60 FPS Normal Recording** *(Available)*
- [x] **Live Workflow Timelapse with 5 Intervals** *(Available)*
- [x] **Interactive Custom Region Capture** *(Available)*
- [x] **Host-Scoped Smart Toolbar Visibility** *(Available)*
- [x] **5-Second Inactivity Auto-Pause & Resume** *(Available)*
- [ ] **Adobe Premiere Pro Integration** *(Planned)*
- [ ] **Adobe After Effects Integration** *(Planned)*
- [ ] **Adobe Illustrator Integration** *(Planned)*
- [ ] **Multi-Track Audio Separation** *(Planned)*
- [ ] **Direct Export Presets for Social Platforms** *(Planned)*

---

## Documentation & Changelog

- **[CHANGELOG.md](file:///F:/Recorder%20Extension/CHANGELOG.md):** Complete release history, bug fixes, and feature additions.
- **[BUILD_REPORT.md](file:///F:/Recorder%20Extension/distribution/Flo_2.0.2_RecordingIntegrity_RC/BUILD_REPORT.md):** Technical compiler options, toolchain specifications, and SHA-256 binary checksums.
- **[TEST_REPORT.md](file:///F:/Recorder%20Extension/distribution/Flo_2.0.2_RecordingIntegrity_RC/TEST_REPORT.md):** 20-test acceptance verification matrix.
- **[FRAME_INTEGRITY_COMPARISON.md](file:///F:/Recorder%20Extension/distribution/Flo_2.0.2_RecordingIntegrity_RC/FRAME_INTEGRITY_COMPARISON.md):** Detailed motion defect investigation and side-by-side analysis.

---

## Licensing

Flo is proprietary software distributed by Subho Ghorui.

- **No Subscription:** Flo is distributed without recurring subscriptions or seat fees.
- **Personal and Business Rights:** You are licensed to use Flo for personal creative workflows, studio work, and enterprise production.
- **Full Commercial Rights to Videos:** You retain complete, unencumbered ownership of all videos recorded with Flo. You are free to edit, publish, monetize, and distribute your recordings commercially.
- **Redistribution Prohibited:** Flo is proprietary. Selling, reselling, sublicensing, repackaging, reverse engineering, or redistributing Flo or its companion binaries is strictly prohibited.
- **Governing EULA:** Use of Flo is governed by the [Flo End User License Agreement](file:///F:/Recorder%20Extension/EULA.txt).

---

## Support & Feedback

- **Publisher:** Subho Ghorui
- **Email Support:** [ghoruisubho1999@gmail.com](mailto:ghoruisubho1999@gmail.com)
- **Issue Tracker:** [GitHub Issues](https://github.com/Subho-XD/flo/issues)
- **Releases:** [GitHub Releases](https://github.com/Subho-XD/flo/releases)
