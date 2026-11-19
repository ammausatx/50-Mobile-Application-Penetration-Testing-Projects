# 27. Mobile API Object-Level Authorization Assessment

<sub><b>INTERMEDIATE</b> · Android mobile application security testing</sub>

> **SIMULATED TRAINING WALKTHROUGH — NOT REAL TEST EVIDENCE.** Screenshots and sample observations are fictional UI illustrations. Run tests only against your own lab app/device or a target covered by written authorization.

## Objective

Verify that mobile API endpoints enforce user and object authorization independently of client-side identifiers.

## Lab and prerequisites

- Android Studio Emulator or dedicated test device with a disposable test profile.
- An intentionally vulnerable training APK and synthetic test data.
- **Tools:** Burp Suite, ADB, Postman, Android Emulator.
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

1. Capture API calls from two synthetic lab accounts and map object identifiers to owners.
2. Replay only read-only requests using the second account and synthetic records.
3. Compare status, response body, and server logs for owner and non-owner access.
4. Test missing, malformed, and unexpected object identifiers without enumerating real users.
5. Confirm authorization is enforced by the API on every request, not by app navigation.

Example starting point (adapt to the local app and tool version):

```bash
Inspect GET /api/v1/profile and /api/v1/records/{synthetic-id} in Burp
```

The command is a lab example. Confirm the exact target and package before execution; do not run it against an unrelated device or service.

## Step 4 — Validate and interpret

Expected training output: An endpoint/role matrix documenting object ownership, allowed actions, denied cross-user access, and response consistency.

Broken object-level authorization may expose another user's records or permit unauthorized modifications. A static-analysis alert, manifest attribute, or isolated log entry is a lead—not a confirmed vulnerability. Validate attacker prerequisites, reachability, affected data/action, actual impact, and relevant positive controls. Record **confirmed**, **not observed**, **false positive**, or **needs further validation**.

## Step 5 — Remediation and retest

Authorize each object against the authenticated principal on the server, minimize returned fields, and log denied cross-tenant access.

Repeat the same test on the corrected build and supported Android versions. Record before/after behavior, build hash, timestamp, and residual limitations.

## Simulated tool screenshots

> These project-specific images are fictional training illustrations, not genuine tool output or evidence of a real assessment.

![Project 27 lab setup — simulated training illustration](screenshots/01-lab-setup.svg)

![Project 27 test execution — simulated training illustration](screenshots/02-test-execution.svg)

![Project 27 result review — simulated training illustration](screenshots/03-result-review.svg)

## Evidence and deliverables

- Authorization and scope record; package, build hash, device/API level, and tool versions.
- Reproducible commands/actions and timestamps.
- Sanitized logs, screenshots, relevant source/configuration references, and test account roles.
- Expected versus observed behavior, validated impact, limitations, remediation owner, and retest outcome.
- Never commit credentials, tokens, private keys, personal data, or proprietary APKs without permission.

## Framework references

- OWASP API Security Top 10 — BOLA; OWASP MASVS-NETWORK
- [OWASP MASVS](https://mas.owasp.org/MASVS/)
- [OWASP MASTG](https://mas.owasp.org/MASTG/)

## Completion checklist

- [ ] Scope and authorization recorded
- [ ] Lab package/build and device identified
- [ ] Test completed safely
- [ ] Evidence sanitized and labeled
- [ ] Finding validated and severity justified
- [ ] Remediation and repeatable retest documented
