# 28. Mobile API Rate Limiting and Abuse Controls

<sub><b>INTERMEDIATE</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Screenshots and sample observations are fictional UI illustrations. Run tests only against your own lab app/device or a target covered by written authorization.

## Objective

Assess API throttling, retry behavior, abuse detection, and resource controls using low-volume tests in a controlled environment.

## Lab and prerequisites

- Android Studio Emulator or dedicated test device with a disposable test profile.
- An intentionally vulnerable training APK and synthetic test data.
- **Tools:** Burp Suite, Postman, ADB, app server logs.
- Confirm authorization, package name, APK version/hash, device serial, Android API level, test accounts, and allowed test window.
- Keep the emulator on an isolated test network. Snapshot before runtime changes.

## Step 1 — Prepare the target

Install the training APK and verify its identity. Record package/build, device/API level, tool versions, and baseline behavior. Use synthetic accounts and data; do not connect personal or production accounts.

```bash
adb devices -l
adb shell getprop ro.build.version.release
adb shell pm list packages | grep -F 'com.example.training'
```

## Step 2 — Inspect the implementation

Use JADX/Apktool or the relevant platform tool to identify the manifest, configuration, and code paths associated with the feature. Record file/class/method names and the expected security control. Do not modify or republish third-party APKs.

## Step 3 — Perform the controlled test

1. Identify one non-destructive endpoint and document its expected normal request rate.
2. Use a dedicated synthetic account and a low request count with deliberate pauses.
3. Observe response codes, Retry-After, rate-limit headers, and server-side logs.
4. Repeat with a second synthetic account only if the test plan explicitly permits it.
5. Stop immediately if latency rises, errors spread, or resource use becomes abnormal.

Example starting point (adapt to the local app and tool version):

```bash
Send a small fixed number of test requests to the local API and inspect 429/Retry-After
```

The command is a lab example. Confirm the exact target and package before execution; do not run it against an unrelated device or service.

## Step 4 — Validate and interpret

Expected training output: A rate-limit behavior record showing threshold, response behavior, reset window, and alert/logging outcome.

Missing controls may enable credential abuse, scraping, enumeration, or resource exhaustion. A static-analysis alert, manifest attribute, or isolated log entry is a lead—not a confirmed vulnerability. Validate attacker prerequisites, reachability, affected data/action, actual impact, and relevant positive controls. Record **confirmed**, **not observed**, **false positive**, or **needs further validation**.

## Step 5 — Remediation and retest

Apply server-side per-account/device/IP limits, adaptive abuse detection, safe retry guidance, and monitoring without relying solely on client delays.

Repeat the same test on the corrected build and supported Android versions. Record before/after behavior, build hash, timestamp, and residual limitations.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not genuine tool output or evidence of a real assessment.

![Project 28 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 28 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 28 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization and scope record; package, build hash, device/API level, and tool versions.
- Reproducible commands/actions and timestamps.
- Sanitized logs, screenshots, relevant source/configuration references, and test account roles.
- Expected versus observed behavior, validated impact, limitations, remediation owner, and retest outcome.
- Never commit credentials, tokens, private keys, personal data, or proprietary APKs without permission.

## Framework references

- OWASP API Security Top 10 — Unrestricted Resource Consumption; OWASP MASVS-NETWORK
- [OWASP MASVS](https://mas.owasp.org/MASVS/)
- [OWASP MASTG](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Scope and authorization recorded
- [ ] Lab package/build and device identified
- [ ] Test completed safely
- [ ] Evidence sanitized and labeled
- [ ] Finding validated and severity justified
- [ ] Remediation and repeatable retest documented
