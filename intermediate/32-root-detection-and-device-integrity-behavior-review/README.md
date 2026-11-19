# 32. Root Detection and Device Integrity Behavior Review

<sub><b>INTERMEDIATE</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Images and sample observations are fictional UI illustrations. Use only your own lab app/device or a target covered by written authorization.

## Objective

Evaluate root/jailbreak and device-integrity signals, their false-positive behavior, and whether security controls are applied proportionately.

## Lab and prerequisites

- Android Studio Emulator or dedicated test device with a disposable test profile.
- An intentionally vulnerable training APK and synthetic test data.
- **Tools:** Android Emulator, ADB, JADX, MobSF.
- Confirm authorization, package/build hash, device serial, Android API level, test accounts, and test window.
- Keep the emulator on an isolated network and snapshot it before runtime changes.

## Step 1 — Prepare the target

Install the training APK and verify package identity. Record device/API level, tool versions, baseline behavior, and the exact component under review. Do not use personal or production accounts.

```bash
adb devices -l
adb shell getprop ro.build.version.release
adb shell pm list packages | grep -F 'com.example.training'
```

## Step 2 — Inspect the implementation

Use JADX/Apktool or the relevant platform tool to identify manifest declarations, configuration, and code paths. Record class/method names and the expected security control. Do not alter or redistribute third-party APKs.

## Step 3 — Perform the controlled test

1. Identify root/integrity checks in source and document which signals are used.
2. Establish a clean emulator baseline and record OS/build properties.
3. Use only emulator configurations explicitly provided for the lab to compare clean and modified states.
4. Observe warning, restricted-function, and telemetry behavior without bypassing protections on third-party apps.
5. Check that the server independently protects sensitive actions regardless of device signals.

Example starting point:

```bash
adb shell getprop ro.build.tags && adb shell id
```

Adapt the command to your own emulator and tool version. Confirm the target package and scope before execution.

## Step 4 — Validate and interpret

Expected training output: A device-state matrix showing detection signals, app response, false positives, and server-side enforcement.

Weak checks can be bypassed, while overly aggressive checks may block legitimate users or expose sensitive device details. A static alert or isolated log line is a lead, not a confirmed vulnerability. Validate prerequisites, reachability, affected data/action, actual impact, and positive controls. Record **confirmed**, **not observed**, **false positive**, or **needs further validation**.

## Step 5 — Remediation and retest

Treat device integrity as a risk signal, use platform integrity APIs where suitable, minimize collected data, and enforce authorization server-side.

Repeat the same test on the corrected build and supported Android versions. Record before/after behavior, build hash, timestamp, and residual limitations.

## Simulated tool screenshots

> Project-specific fictional training illustrations, not genuine tool output or evidence of a real assessment.

![Project 32 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 32 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 32 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization/scope record; package, build hash, device/API level, and tool versions.
- Reproducible commands/actions and timestamps.
- Sanitized logs, screenshots, source/configuration references, and test account roles.
- Expected versus observed behavior, validated impact, limitations, remediation owner, and retest outcome.
- Never commit credentials, tokens, private keys, personal data, or proprietary APKs without permission.

## Framework references

- Android Developers — Play Integrity API; OWASP MASVS-RESILIENCE
- [OWASP MASVS](https://mas.owasp.org/MASVS/)
- [OWASP MASTG](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Scope and authorization recorded
- [ ] Lab package/build and device identified
- [ ] Test completed safely
- [ ] Evidence sanitized and labeled
- [ ] Finding validated and severity justified
- [ ] Remediation and repeatable retest documented
