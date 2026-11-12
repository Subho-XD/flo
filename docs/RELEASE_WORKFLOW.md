# Flo — Release Management & Documentation Workflow

This document establishes the mandatory documentation and release management protocol for Flo. Every new build prepared for distribution must follow this standardized checklist to maintain product consistency, cryptographic integrity, and release transparency.

---

## 1. Release Lifecycle Stages

Every release cycle consists of two strictly guarded phases:

```text
┌─────────────────────────────────┐       ┌─────────────────────────────────┐
│   STAGE A: Local Engineering   │       │   STAGE B: Remote Publication   │
│   - Code implementation         │       │   - Create Git tag              │
│   - Diagnostic stress tests     │  ───> │   - Publish GitHub Release      │
│   - Local staging & checksums   │       │   - Verify downloaded assets    │
│   - Documentation updates       │       │   - Sync remote branches        │
│   - USER APPROVAL GATE          │       │                                 │
└─────────────────────────────────┘       └─────────────────────────────────┘
```

> [!IMPORTANT]
> **Strict Approval Gate:** Stage B (remote publication, git tagging, or GitHub release creation) must NEVER be executed without explicit user confirmation of Stage A verification findings.

---

## 2. Pre-Release Engineering Verification Checklist

Before preparing release documentation or staging distribution assets:

1. **Verify Clean Compilations:**
   - [ ] Compile `FloNativeCompanion.exe` with zero warnings and zero errors.
   - [ ] Compile `creative_recorder_addon.uxpaddon` with zero warnings and zero errors.
   - [ ] Ensure binaries target Release x64 with `/O2` optimization and `/std:c++17`.
2. **Execute Full Automated Test Suites:**
   - [ ] Execute `diagnose_frame_integrity.exe` (sustained 60s+ 8-scenario motion stress test). Verify 0 torn frames, 0 px displacement, and rock-solid 60 FPS CFR delivery.
   - [ ] Execute `test_indesign_integration.exe` (all 8 host integration tests must pass).
   - [ ] Execute `diagnose_autopause_timing_suite.exe` (verify exact 5.000s inactivity threshold and seamless auto-resume).
3. **Validate Version Strings:**
   - [ ] `src/plugin/manifest.json` version string.
   - [ ] `src/indesign_plugin/manifest.json` version string.
   - [ ] Installer resource scripts (`FloSetup.rc`, `FloCompanionSetup.rc`).

---

## 3. Documentation Update Protocol

Before staging or publishing any release:

### A. Review Git & Code Changes
- Review all source code commits and PR diffs since the previous release tag.
- Categorize changes into:
  - **Added:** New user-facing features, tools, or integrations.
  - **Improved:** Performance optimizations, UI enhancements, or architectural refactorings.
  - **Fixed:** Resolved bugs, visual defects, or race conditions.
  - **Known Issues:** Any remaining environmental limitations or platform notes.

### B. Update `CHANGELOG.md`
- Insert the new version entry at the top of [CHANGELOG.md](file:///F:/Recorder%20Extension/CHANGELOG.md).
- Use format: `## [X.Y.Z] — YYYY-MM-DD`.
- Ensure entries reflect verified facts rather than assumptions or unreleased plans.

### C. Update `README.md`
- Inspect [README.md](file:///F:/Recorder%20Extension/README.md) for any drift:
  - Verify release badge points to the new version tag.
  - Verify download links point to the current release assets.
  - Update system requirements if dependencies changed.
  - Update usage guides or feature descriptions if new modes were added.
  - Verify planned integrations remain clearly marked as *Planned*.

### D. Prepare Technical Diagnostic Reports
Staged alongside the release binaries in `distribution/Flo_X.Y.Z_Candidate/`:
- `BUILD_REPORT.md`: Toolchain, compiler flags, and artifact inventory.
- `TEST_REPORT.md`: Matrix of all automated and live integration test results.
- `FRAME_INTEGRITY_COMPARISON.md`: Before/after defect investigation and diagnostic findings.
- `PHOTOSHOP_CAPTURE_DIAGNOSTICS.md`: Photoshop-specific capture pipeline verification.
- `INDESIGN_CAPTURE_DIAGNOSTICS.md`: InDesign-specific companion and auto-pause verification.

---

## 4. Local Packaging & Checksum Generation

1. Package standalone `.ccx` extensions:
   ```powershell
   .\tools\package_indesign_plugin.ps1 -Version "X.Y.Z"
   .\tools\package_production_plugin.ps1 -Version "1.X.X"
   ```
2. Build standalone setup executables:
   ```cmd
   call tools\installer\build_companion_setup.bat
   call tools\installer\build_flo_setup.bat
   ```
3. Stage distribution files in `distribution\Flo_X.Y.Z_Candidate\`:
   - `Flo_Setup.exe`
   - `Flo_InDesign_Companion_Setup.exe`
   - `Flo_InDesign.ccx`
   - `Flo_Photoshop.ccx`
   - Diagnostic Markdown reports
4. Generate authoritative `SHA256SUMS.txt`:
   ```powershell
   Get-FileHash -Path <files> -Algorithm SHA256
   ```

---

## 5. GitHub Release Publication Protocol (Stage B)

Once explicit user approval is granted:

1. **Publish GitHub Release:**
   ```powershell
   gh release create vX.Y.Z `
     --repo Subho-XD/flo `
     --target main `
     --title "Flo X.Y.Z — <Descriptive Title>" `
     --notes-file <PathToReleaseNotes> `
     <AssetPaths>
   ```
2. **Download & Verify Remote Assets:**
   - Download the published assets to an isolated verification folder:
     ```powershell
     gh release download vX.Y.Z --repo Subho-XD/flo --dir tools\temp\verify
     ```
   - Calculate SHA-256 hashes of downloaded files and verify a 100% match against `SHA256SUMS.txt`.
3. **Commit & Push Documentation Updates:**
   - Commit updated `README.md`, `CHANGELOG.md`, and workflow documentation to the repository.
