# 25. Mobile Local Authentication and Biometric Security

<sub><b>INTERMEDIATE</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Screenshots and sample observations are fictional UI illustrations. Run tests only against your own lab app/device or a target covered by written authorization.

## Objective

Assess local PIN/password and biometric flows, fallback behavior, session binding, and server-side authorization after local unlock.

## Lab and prerequisites

- Android Studio Emulator or dedicated test device with a disposable test profile.
- An intentionally vulnerable training APK and synthetic test data.
- **Tools:** Android Studio Emulator, ADB, JADX, MobSF.
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

1. Map login, local unlock, biometric prompt, fallback, timeout, and logout flows.
2. Inspect BiometricPrompt configuration and whether cryptographic operations are bound to biometric authentication.
3. Test enrolled and unenrolled emulator states, cancellation, lockout, fallback, and app background/foreground transitions.
4. Verify that local unlock does not replace server-side authorization or extend expired sessions.
5. Record whether sensitive operations require fresh authentication and whether tokens are invalidated on logout.

Example starting point (adapt to the local app and tool version):

```bash
adb shell dumpsys biometric | head -80  # emulator diagnostics where supported
```

The command is a lab example. Confirm the exact target and package before execution; do not run it against an unrelated device or service.

## Step 4 — Validate and interpret

Expected training output: An authentication-state matrix covering biometric enrollment, fallback, cancellation, timeout, reauthentication, and session behavior.

Weak fallback or local-only trust can permit access to sensitive app functions after device or session state changes. A manifest flag, static-analysis alert, or isolated log entry is a lead—not a confirmed vulnerability. Validate attacker prerequisites, reachability, affected data/action, actual impact, and relevant positive controls. Record **confirmed**, **not observed**, **false positive**, or **needs further validation**.

## Step 5 — Remediation and retest

Use platform BiometricPrompt with crypto-bound keys where appropriate, secure fallback, short session lifetimes, server-side authorization, and token invalidation.

Repeat the same test on the corrected build and supported Android versions. Record before/after behavior, build hash, timestamp, and residual limitations. Do not close a finding solely because a configuration value changed; verify the security property.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not genuine ADB/JADX/Burp/Frida output or evidence of a real assessment.

![Project 25 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 25 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 25 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization and scope record; package, build hash, device/API level, and tool versions.
- Reproducible commands/actions and timestamps.
- Sanitized logs, screenshots, relevant source/configuration references, and test account roles.
- Expected versus observed behavior, validated impact, limitations, and remediation owner.
- Retest outcome and residual risk. Never commit credentials, tokens, private keys, personal data, or proprietary APKs without permission.

## Framework references

- Android Developers — Biometric authentication; OWASP MASVS-AUTH; OWASP MASWE
- [OWASP Mobile Application Security Verification Standard (MASVS)](https://mas.owasp.org/MASVS/)
- [OWASP Mobile Application Security Testing Guide (MASTG)](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Scope and authorization recorded
- [ ] Lab package/build and device identified
- [ ] Static and/or dynamic test completed safely
- [ ] Evidence sanitized and labeled as real or simulated
- [ ] Finding validated and severity justified
- [ ] Remediation and repeatable retest documented
