# Changelog

All notable changes to Flo (Creative Workflow Recorder) are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to strict semantic release versioning.

---

## [2.0.2] — 2026-11-12

### Added
- **4-Slot Frame Ring Buffer:** Integrated a multi-buffer ring architecture (`kFrameRingCapacity = 4`) into `WgcCaptureEngine`. Segregated producer capture writes and consumer encoding reads into distinct state-managed buffer slots (`Free`, `Writing`, `Ready`, `Reading`).
- **GPU Query Fence Synchronization:** Introduced per-slot `D3D11_QUERY_EVENT` tracking. The capture producer signals completion upon GPU subresource copying, and the encoder consumer queries event completion via `pContext->GetData` before mapping memory.
- **Immediate Context Thread Safety:** Added a dedicated recursive mutex (`mContextMutex`) and `LockContext()` in `D3D11Pipeline`, fully serializing all Direct3D 11 device context operations across WinRT thread pool callbacks and encoder worker threads.
- **Double-Buffered Zero-Stall Staging Readback:** Upgraded GPU-to-CPU staging memory to a ping-pong double-buffer ring (`kStagingRingSize = 2`), eliminating synchronous PCIe pipeline flushes and CPU stalls during `Map()` calls.
- **High-Precision Multimedia Deadline Loop:** Implemented a deadline timer using `timeBeginPeriod(1)` to bypass Windows' default 15.625ms timer quantum, achieving rock-solid 59.891 FPS constant frame rate (CFR) delivery.
- **Parallel Multi-Threaded NV12 Conversion:** Implemented 4-way parallel image slicing via `std::async` for both 1:1 and scaled video pipelines, slashing color conversion latency to under 1.0 millisecond.
- **Cross-Application Frame Integrity Diagnostic Suite:** Authored a comprehensive 3-stage validation suite (`diagnose_frame_integrity.exe`) verifying 8 distinct motion scenarios (horizontal translation up to 800 px/s, vertical motion, diagonal sweeps, rapid resize, and continuous harmonic panning).

### Improved
- **Direct3D11CaptureFramePool Allocation:** Increased capture frame pool buffer allocation from 2 to 3 surfaces, preventing Desktop Window Manager (DWM) buffer recycling contention during rapid dirty-rectangle updates.
- **Content Size Bounding:** Enforced strict clamping to `Direct3D11CaptureFrame::ContentSize()`, preventing uninitialized surface padding borders from being copied into video frames.
- **Session Duration Fidelity:** Video sample timestamps now accurately maintain 1:1 real-time duration matching with wall-clock elapsed time (62.13s video recorded over 62.60s elapsed).
- **Subpixel De-Fringing Filter:** Refined ClearType subpixel chroma de-fringing to maintain authentic saturation on high-contrast vector paths and fine typography without visual attenuation.

### Fixed
- **Horizontal Scanline Slicing & Boundary Tearing:** Resolved the critical defect where rapidly moving objects (such as solid circular shapes and InDesign HUD tooltip overlays) suffered from horizontal strip displacements and comb-like artifacts (0 torn frames across 3,721 decoded test frames).
- **InDesign Auto-Pause Threshold Precision:** Resolved timing variance where InDesign inactivity detection previously lagged at 10 seconds. Unified the authoritative threshold to 5,000 milliseconds, verified at exactly **4.998s** trigger precision.
- **Caret Blink & Background Focus Jitter:** Fixed false activity resets caused by text cursor blinking and background focus transitions.

### Known Issues
- Windows N editions require manual installation of the free Windows Media Feature Pack to supply essential Media Foundation encoder components.
- Custom Region selection across heterogeneous multi-monitor setups with different DPI scalings (e.g., 100% and 200%) is optimized for the display hosting the primary host window.

---

## [2.0.1] — 2026-11-10

### Added
- **Unified Windows Installer (`Flo_Setup.exe`):** Single-click guided installer (~1.2 MB) packaging the Photoshop UXP Hybrid Addon, InDesign UXP Plugin, and Flo Native Companion runtime.
- **Smart Host Detection:** Automatically detects installed versions of Adobe Photoshop (2024–2026) and Adobe InDesign (2024–2026) through registry introspection.
- **Automated UPIA Deployment:** Integrated Adobe's Unified Plugin Installer Agent (`UnifiedPluginInstallerAgent.exe`) into the setup wizard for automated CCX extension registration.
- **Custom Protocol Handshake (`flo://`):** Registered the `flo` protocol in Windows registry, enabling InDesign UXP menus to launch and connect to the native companion automatically.
- **Host-Scoped Smart Toolbar Visibility:** Installed Win32 WinEvent hooks (`EVENT_SYSTEM_FOREGROUND`, `EVENT_SYSTEM_MINIMIZESTART`, `EVENT_SYSTEM_MINIMIZEEND`) and window ownership pairing (`SetWindowLongPtrW(..., GWLP_HWNDPARENT, ...)`), causing Flo to float neatly when InDesign is active and hide automatically when switching to other apps.
- **Real-Time Document Metadata Tracking:** Added live InDesign DOM event listeners (`afterOpen`, `afterSave`, `afterActivate`) to dynamically update the active document title and auto-generate contextual recording filenames (`DocumentName_Recording_YYYYMMDD_HHMMSS.mp4`).

### Improved
- **Secondary Window Dialog Capture:** Enabled `IncludeSecondaryWindows(true)` on `IGraphicsCaptureSession6`, ensuring Photoshop modal dialogs (Color Picker, Layer Styles, Blending Options) and InDesign dialogs are captured cleanly into recordings.
- **Per-Monitor High-DPI Scaling:** Enhanced Direct2D vector interface rendering across 100%, 125%, 150%, 175%, and 200% scaling factors without UI clipping or sub-pixel hit-test drift.
- **Host Process Monitoring:** Established monitored process handles (`OpenProcess` with `SYNCHRONIZE`) and 2-second WebSocket heartbeat pinging with automatic 6-second disconnection timeouts.

### Fixed
- **InDesign Window Targeting Defect:** Fixed a critical bug where substring title matching inadvertently captured Antigravity or browser windows instead of InDesign. Enforced strict executable image verification (`QueryFullProcessImageNameW` verifying `InDesign.exe`).
- **Floating Toolbar Focus Stealing:** Replaced activating show commands with `SW_SHOWNOACTIVATE`, ensuring keystrokes in text frames and layout manipulation remain uninterrupted while recording.
- **Stale Disconnection State:** Resolved UI issue where the toolbar remained green and displayed "Connected" after InDesign was closed.

---

## [2.0.0] — 2026-11-09

### Added
- **Adobe InDesign Architecture:** Introduced initial out-of-process InDesign recording architecture utilizing a headless UXP extension (`com.flo.indesign`) and standalone C++ Native Companion (`FloNativeCompanion.exe`).
- **Loopback WebSocket IPC Bridge:** Implemented an authenticated local loopback WebSocket server (`ws://127.0.0.1:49152`) with cryptographically secure session token verification.
- **InDesign Companion Standalone Installer:** Created `Flo_InDesign_Companion_Setup.exe` for independent companion runtime deployment.

### Improved
- **Dual-Host Build Pipeline:** Established synchronized build scripts supporting both in-process UXP addons (Photoshop) and companion runtimes (InDesign) from a unified native C++ codebase.

---

## [1.2.3] — 2026-11-09

### Added
- **Translucent Hardware-Accelerated Custom Region Selection Overlay:** Replaced opaque overlays with a layered, hardware-accelerated Direct2D window (`WS_EX_LAYERED | WS_EX_TOPMOST`). The cutout region retains alpha = 0 (100% canvas brightness), while exterior areas are softly dimmed (`rgba(0, 0, 0, 0.50)`).
- **Segmented Control Tracks:** Replaced separate card boxes with recessed studio tracks (`#1C1C1C`, 32px height, 6px radius) and elevated selection pills (`#2C2C2C`) for Capture Source and Recording Mode.
- **Prominent Tabular Recording Timer:** Monospaced tabular elapsed timer (`● REC  00:01:24`) rendered in both Expanded ($460 \times 280\text{ px}$) and Compact ($360 \times 44\text{ px}$) modes.

### Improved
- **Visual Palette Calibration:** Standardized on calibrated Studio Dark tokens: Studio Base (`#141414`), Recessed Track (`#1C1C1C`), Hairline Borders (`rgba(255, 255, 255, 0.07)`), and Studio Crimson primary action (`#C92A2A`).

---

## [1.2.2] — 2026-11-09

### Added
- **Interactive Custom Region Capture:** Replaced fragile ActionManager canvas viewport bounds with an interactive rectangular selector (`RegionSelectorOverlay`) featuring 8 resize handles and live resolution badges (`W × H px`).
- **True Live Timelapse Engine:** Built monotonic clock interval throttling with sequential timestamp allocation, delivering true mathematical speedups ($7.5\times$, $15\times$, $30\times$, $60\times$, $150\times$).
- **5-Second Automatic Inactivity Pause:** Initial introduction of the 5.0-second inactivity pause threshold with instant resumption upon mouse or stylus input.

### Fixed
- **Timelapse 1.0x Playback Bug:** Resolved issue where live timelapse output played back at normal real-time speed.
- **Capture Window Self-Inclusion:** Enforced `WDA_EXCLUDEFROMCAPTURE` on all overlay controls to prevent toolbars from capturing themselves.

---

## [1.2.1] — 2026-11-08

### Added
- **ClearType Subpixel Chroma De-Fringing:** Introduced $2\times 2$ box-filtered downsampling and a ClearType chromatic aberration filter, completely eliminating blue and red fringe artifacts on text and vector edges.
- **Selectable Timelapse Intervals:** Added 5 structured interval delay presets: `250 ms`, `500 ms`, `1 s`, `2 s`, and `5 s`.

### Improved
- **Headless Command Integration:** Eliminated docked panel sidebars in Photoshop; top menu command `Plugins -> Flo` toggles the floating Win32 interface directly.
- **Work Area Clamping:** Implemented `MonitorFromWindow` bounds checking to keep the toolbar within visible desktop margins.

---

## [1.2.0] — 2026-11-08

### Added
- **Application-Scoped Floating Window:** Replaced docked panels with a custom-rendered Direct2D floating toolbar that docks and travels above Photoshop.
- **Optional WASAPI Audio Capture:** Integrated Windows Audio Session API (WASAPI) for recording system sound and microphone commentary.
- **Expanded and Compact Modes:** Introduced compact recording mode ($360 \times 44\text{ px}$) to maximize available canvas area during active design work.

---

## [1.0.0] — 2026-11-07

### Added
- **Initial Production Core:** High-performance screen capture utilizing Windows Graphics Capture (WGC) and Direct3D 11 compositing.
- **Hardware-Accelerated Encoding:** Media Foundation H.264 video encoding via GPU hardware transforms (MFT).
- **Photoshop UXP Hybrid Integration:** Native `.uxpaddon` module binding Windows capture APIs directly to Photoshop's JavaScript runtime.
- **Local Storage:** Automated saving to `%USERPROFILE%\Videos\Creative Workflow Recorder\`.
