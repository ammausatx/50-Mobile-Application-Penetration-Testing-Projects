# 50 Mobile Application Penetration Testing Projects

A practical, progressive collection of 50 Android mobile application security testing projects, organized into Beginner, Intermediate, and Advanced levels.

> **Training-lab use only.** Test only applications and devices you own or are explicitly authorized to assess. All screenshots and terminal/tool outputs in this repository are **SIMULATED TRAINING EXAMPLES — NOT REAL TEST EVIDENCE**. Replace them with verified lab evidence before reporting real findings.

## Learning paths

- [Beginner (01–15)](beginner/README.md) — Android fundamentals, APK inspection, traffic capture, storage, and platform controls.
- [Intermediate (16–35)](intermediate/README.md) — component exposure, WebViews, network security, authentication, API behavior, and runtime testing.
- [Advanced (36–50)](advanced/README.md) — advanced instrumentation, reverse engineering, cryptography, anti-tampering, and full mobile assessment.

## Project walkthrough format

Every project contains a project-specific walkthrough with prerequisites, lab setup, commands, actions, expected observations, analysis, remediation, three embedded simulated tool screenshots (lab setup, test execution, and result review), evidence guidance, and retest criteria.

Screenshots illustrate realistic-looking tool workflows but do not claim that a tool was actually run or that a real vulnerability was found.

## Suggested lab

Use an isolated Android emulator or dedicated test device, Android Studio Emulator, Android SDK Platform Tools (ADB), JADX, Apktool, MobSF, Burp Suite, Frida, and deliberately vulnerable training apps such as DIVA, InsecureBankv2, or OWASP MSTG crackmes. Use a separate test network and synthetic accounts/data.

## Safety and evidence

1. Confirm written authorization and define the app, package, device, accounts, endpoints, and test window.
2. Use only lab APKs, test accounts, and non-production data.
3. Never publish credentials, signing keys, tokens, personal data, or private certificates.
4. Keep simulated output labeled; never present it as a real scan or assessment result.
5. Record tool versions and preserve reproducible evidence for real work.

## Repository structure

- `beginner/` — Projects 01–15
- `intermediate/` — Projects 16–35
- `advanced/` — Projects 36–50
- `PROJECT_INDEX.md` — all 50 linked walkthroughs
- each project folder's `screenshots/` — three project-specific simulated SVG illustrations
- `_assets/` — shared visual assets

See [PROJECT_INDEX.md](PROJECT_INDEX.md), [CONTRIBUTING.md](CONTRIBUTING.md), and [REPORT_TEMPLATE.md](REPORT_TEMPLATE.md).
