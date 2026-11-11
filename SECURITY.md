# Security Policy

## Reporting Security Vulnerabilities

We take the security and privacy of Flo and our creators seriously. If you believe you have discovered a security vulnerability or security-related defect in Flo, please report it directly and privately.

**Do not file public GitHub issues for security vulnerabilities.**

### Contact

Please send vulnerability reports privately to:
- **Email:** [ghoruisubho1999@gmail.com](mailto:ghoruisubho1999@gmail.com)
- **Subject:** `[SECURITY] Flo Vulnerability Report - <Short Description>`

### What to Include

To help us investigate and triage your report promptly, please include:
- The version of Flo and the specific integration affected (Photoshop or InDesign).
- The Windows version and build number.
- A concise summary and step-by-step description to reproduce the vulnerability.
- A proof-of-concept (PoC) script or detailed technical explanation, if applicable.
- Any relevant logs or diagnostics.

> **Privacy Warning:** Please do not attach confidential client documents, unredacted personal files, private recording videos, system credentials, or access tokens in your report.

### Vulnerability Response Timeline

- **Acknowledgment:** Within 48 hours of receiving your report.
- **Triage & Assessment:** Initial assessment and status update within 5 business days.
- **Remediation & Patch:** Fixes for confirmed security vulnerabilities will be released promptly in an updated official release.

## Supported Versions

Only the latest official release receives active security patches and updates:

| Version | Supported | Status |
| :--- | :---: | :--- |
| **2.0.x** | Yes | Current official release stream |
| **1.x** | No | Deprecated |

## Privacy and Local Data Handling

Flo is designed with local data privacy as a core principle:
- Recordings are processed and saved locally on your Windows computer in the configured storage folder.
- Flo does not transmit your creative documents, designs, or video recordings to external remote servers.
- The InDesign integration uses local loopback communication (`localhost`) between its UXP extension and the local companion process; this communication does not accept external network connections.
