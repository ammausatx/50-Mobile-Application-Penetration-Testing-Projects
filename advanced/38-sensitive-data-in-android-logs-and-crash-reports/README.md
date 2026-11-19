# 38. Sensitive Data in Android Logs and Crash Reports

<sub><b>ADVANCED</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Images and sample observations are fictional UI illustrations. Perform tests only in an isolated lab you control or under written authorization.

## Objective

Check whether app logs, exceptions, analytics, or crash reports contain credentials, tokens, personal information, or sensitive business data.

## Lab and prerequisites

- Dedicated Android Studio Emulator or test device with disposable profile and snapshot.
- Training APK, synthetic data, and a host-only test network.
- **Tools:** ADB logcat, JADX, Android Studio, MobSF.
- Confirm scope, package/build hash, device/API level, account roles, tool versions, test window, and stop conditions.
- Advanced testing must not touch production accounts, real user data, or third-party applications.

## Step 1 — Baseline and target verification

Record package identity, APK SHA-256, signing/build details, device serial, Android API level, and normal app behavior. Confirm the target package before running commands.

```bash
adb devices -l
adb shell getprop ro.build.version.release
adb shell pm list packages | grep -F 'com.example.training'
```

## Step 2 — Inspect the implementation

Use the listed tools to map the relevant manifest declarations, code paths, native components, data stores, or platform behavior. Record class/method/file references and identify the expected security property. Preserve an untouched APK copy and emulator snapshot.

## Step 3 — Controlled assessment procedure

1. Start a clean emulator session and clear prior log buffers.
2. Exercise normal training-app workflows using synthetic accounts and non-sensitive records.
3. Collect only the app's relevant log output and inspect crash/analytics payloads in the lab.
4. Search for secrets, identifiers, request bodies, and verbose stack traces; redact before storing evidence.
5. Repeat on a release-like build and compare debug-only versus production logging.

Example lab command:

```bash
adb logcat -c && adb logcat -d | grep -Ei 'token|password|authorization|email'  # synthetic test session
```

Adapt it to the test APK and tool version. Do not execute against unrelated devices, services, or accounts. Stop if the test affects data outside the agreed scope.

## Step 4 — Expected observations and validation

A sanitized log/crash review with data categories, affected build types, reproduction steps, and redaction notes.

Logs and crash reports may leak authentication material or personal data to local users and third-party telemetry. Validate the observation against source/configuration, runtime behavior, attacker prerequisites, and actual data/action impact. Distinguish confirmed behavior from theoretical attack paths, tool alerts, and false positives.

## Step 5 — Remediation and retest

Remove sensitive logging, use structured redaction, restrict crash-report fields, disable verbose release logs, and apply retention/access controls.

Retest the corrected build with the same device/API level and equivalent test conditions. Record build hashes, timestamps, before/after results, residual risk, and any platform-specific limitations.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not actual ADB/JADX/MobSF/Frida output or evidence of a real assessment.

![Project 38 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 38 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 38 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization, scope, exclusions, and stop conditions.
- APK/build hash, package, device/API level, tool versions, and test identities.
- Reproducible commands/actions, source references, timestamps, and sanitized logs/screenshots.
- Expected versus observed behavior, validated impact, confidence, and limitations.
- Remediation owner, retest evidence, and residual risk. Keep secrets and private APKs out of Git.

## Framework references

- OWASP MASVS-STORAGE; Android Developers — Logcat
- [OWASP MASVS](https://mas.owasp.org/MASVS/)
- [OWASP MASTG](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Written scope and authorization confirmed
- [ ] Isolated device, app, and synthetic data prepared
- [ ] Static/dynamic test performed safely
- [ ] Evidence sanitized and labeled
- [ ] Impact independently validated
- [ ] Remediation and retest documented
