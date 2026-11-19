# 23. Android WebView Security Assessment

<sub><b>INTERMEDIATE</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Screenshots and sample observations are fictional UI illustrations. Run tests only against your own lab app/device or a target covered by written authorization.

## Objective

Review WebView configuration, navigation boundaries, JavaScript settings, file access, mixed content, and safe browsing behavior.

## Lab and prerequisites

- Android Studio Emulator or dedicated test device with a disposable test profile.
- An intentionally vulnerable training APK and synthetic test data.
- **Tools:** JADX, Apktool, ADB, Android Studio Emulator.
- Confirm authorization, package name, APK version/hash, device serial, Android API level, test accounts, and allowed test window.
- Keep the emulator on a host-only or otherwise isolated test network. Snapshot before runtime changes.

## Step 1 — Prepare the target

Install the training APK and verify its identity. Record package/build, device/API level, tool versions, and baseline behavior. Use synthetic accounts and data; do not connect personal or production accounts.

```bash
adb devices -l
adb shell getprop ro.build.version.release
adb shell pm list packages | grep -F 'com.example.training'
```

## Step 2 — Inspect the implementation

Use JADX/Apktool or the relevant platform tool to identify the manifest, components, configuration, and code paths associated with the feature. Record file/class/method names and the expected security control. Do not modify or republish third-party APKs.

## Step 3 — Perform the controlled test

1. Identify WebView instances and record their loading sources and navigation rules.
2. Review JavaScript, file/content access, mixed-content, Safe Browsing, and debugging settings.
3. Inspect URL allowlists and redirect handling; confirm external navigation opens in a trusted browser when appropriate.
4. Use a local test page to validate allowed navigation and benign script behavior; do not load hostile external content.
5. Check whether sensitive native functionality is exposed to untrusted web content.

Example starting point (adapt to the local app and tool version):

```bash
jadx -d jadx-out app-training.apk && grep -R -n 'setJavaScriptEnabled\|setAllowFileAccess\|addJavascriptInterface' jadx-out
```

The command is a lab example. Confirm the exact target and package before execution; do not run it against an unrelated device or service.

## Step 4 — Validate and interpret

Expected training output: A WebView configuration matrix with navigation controls, enabled capabilities, bridge exposure, and tested trust boundaries.

An overly permissive WebView can expose local files, sensitive native methods, or authenticated app context to untrusted content. A manifest flag, static-analysis alert, or isolated log entry is a lead—not a confirmed vulnerability. Validate attacker prerequisites, reachability, affected data/action, actual impact, and relevant positive controls. Record **confirmed**, **not observed**, **false positive**, or **needs further validation**.

## Step 5 — Remediation and retest

Disable unused capabilities, restrict navigation to exact trusted origins, block unsafe file access, validate redirects, and avoid JavaScript bridges unless strictly required.

Repeat the same test on the corrected build and supported Android versions. Record before/after behavior, build hash, timestamp, and residual limitations. Do not close a finding solely because a configuration value changed; verify the security property.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not genuine ADB/JADX/Burp/Frida output or evidence of a real assessment.

![Project 23 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 23 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 23 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization and scope record; package, build hash, device/API level, and tool versions.
- Reproducible commands/actions and timestamps.
- Sanitized logs, screenshots, relevant source/configuration references, and test account roles.
- Expected versus observed behavior, validated impact, limitations, and remediation owner.
- Retest outcome and residual risk. Never commit credentials, tokens, private keys, personal data, or proprietary APKs without permission.

## Framework references

- Android Developers — WebView; OWASP MASVS-PLATFORM; OWASP WebView Cheat Sheet
- [OWASP Mobile Application Security Verification Standard (MASVS)](https://mas.owasp.org/MASVS/)
- [OWASP Mobile Application Security Testing Guide (MASTG)](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Scope and authorization recorded
- [ ] Lab package/build and device identified
- [ ] Static and/or dynamic test completed safely
- [ ] Evidence sanitized and labeled as real or simulated
- [ ] Finding validated and severity justified
- [ ] Remediation and repeatable retest documented
