# 43. Android Obfuscation and Reverse Engineering Assessment

<sub><b>ADVANCED</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Images and sample observations are fictional UI illustrations. Perform tests only in an isolated lab you control or under written authorization.

## Objective

Review release obfuscation and symbol exposure while verifying that sensitive data and authorization are not protected only by obscurity.

## Lab and prerequisites

- Dedicated Android Studio Emulator or test device with disposable profile and snapshot.
- Owner-provided training APK, synthetic data, and an isolated test network.
- **Tools:** JADX, Apktool, R8 mapping file (owner-controlled), MobSF.
- Confirm scope, package/build hash, device/API level, account roles, tool versions, test window, and stop conditions.
- Do not touch production accounts, real user data, or third-party applications.

## Step 1 — Baseline and target verification

Record package identity, APK SHA-256, signing/build details, device serial, Android API level, and normal app behavior. Confirm the target package before running commands.

```bash
adb devices -l
adb shell getprop ro.build.version.release
adb shell pm list packages | grep -F 'com.example.training'
```

## Step 2 — Inspect the implementation

Use the listed tools to map relevant manifest declarations, code paths, native components, or platform behavior. Record file/class/method references and identify the expected security property. Preserve an untouched APK copy and emulator snapshot.

## Step 3 — Controlled assessment procedure

1. Record build type, minification settings, and availability of mapping files in the private build pipeline.
2. Inspect the training APK for readable class/method names, debug artifacts, embedded endpoints, and secrets.
3. Compare a debug and release build using the same benign feature path.
4. Check whether obfuscation materially changes analysis effort, while separately validating server-side controls.
5. Keep mapping files private and out of public repositories.

Example lab command:

```bash
unzip -l app-training.apk | grep -E 'classes[0-9]*\.dex|mapping.txt'
```

Adapt it to the test APK and tool version. Do not execute against unrelated devices, services, or accounts. Stop if the test affects data outside the agreed scope.

## Step 4 — Expected observations and validation

A release-hardening review listing symbol exposure, debug artifacts, embedded secrets, and build configuration gaps.

Exposed implementation details may simplify reverse engineering, but obfuscation alone cannot prevent abuse. Validate observations against source/configuration, runtime behavior, attacker prerequisites, and actual data/action impact. Distinguish confirmed behavior from theoretical paths, tool alerts, and false positives.

## Step 5 — Remediation and retest

Enable R8 for release builds, remove debug artifacts and embedded secrets, protect mapping files, and enforce security server-side.

Retest the corrected build with the same device/API level and equivalent test conditions. Record build hashes, timestamps, before/after results, residual risk, and platform-specific limitations.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not actual tool output or evidence of a real assessment.

![Project 43 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 43 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 43 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization, scope, exclusions, and stop conditions.
- APK/build hash, package, device/API level, tool versions, and test identities.
- Reproducible commands/actions, source references, timestamps, and sanitized logs/screenshots.
- Expected versus observed behavior, validated impact, confidence, and limitations.
- Remediation owner, retest evidence, and residual risk. Keep secrets and private APKs out of Git.

## Framework references

- Android Developers — R8; OWASP MASVS-RESILIENCE
- [OWASP MASVS](https://mas.owasp.org/MASVS/)
- [OWASP MASTG](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Written scope and authorization confirmed
- [ ] Isolated device, app, and synthetic data prepared
- [ ] Test performed safely
- [ ] Evidence sanitized and labeled
- [ ] Impact independently validated
- [ ] Remediation and retest documented
