# Installation verification report template

**Template only. No installation verified. Beta approval: FALSE.** Complete for the exact first-beta candidate after implementing the verifier specified in [INSTALLATION_VERIFICATION.md](../docs/INSTALLATION_VERIFICATION.md).

## Candidate and automatic inspection

| Field | Value |
| --- | --- |
| Candidate version / immutable commit | NOT SET |
| Operator / reviewer / timestamp with timezone | NOT SET |
| Hardware/BIOS / OS version/build | NOT VERIFIED |
| Verifier revision / hash | NOT IMPLEMENTED |
| Config / component manifest digests | NOT VERIFIED |
| Actual boot-medium provenance | UNKNOWN |
| USB profile: OpenCore/online-Recovery or full installer | NOT SET |
| USB total / usable / free / required payload bytes | NOT MEASURED |
| Minimum capacity / payload-fit check | NOT TESTED |
| Backup / restore evidence | NOT VERIFIED |
| Machine JSON report / exit code | NOT AVAILABLE |
| Automatic FAIL / UNKNOWN / WARN items | NOT ASSESSED |

## Manual campaign

| Required test | Result | Evidence / timestamp |
| --- | --- | --- |
| 5 cold boots / 5 restarts | NOT TESTED | NONE |
| Fedora round trips / rescue USB / EFI restore | NOT TESTED | NONE |
| Graphics/video load | NOT TESTED | NONE |
| Speakers / ≥60 s microphone / jack | NOT TESTED | NONE |
| Wi-Fi endurance / reconnects / available Ethernet | NOT TESTED | NONE |
| Bluetooth pairing / reconnect | NOT TESTED | NONE |
| USB map / webcam in two apps | NOT TESTED | NONE |
| 5 sleep/wake cycles / CPU/thermal observations | NOT TESTED | NONE |
| Safe storage checks / backup-file restoration | NOT TESTED | NONE |
| Security posture / services / update recovery | NOT TESTED | NONE |
| ≥48-hour varied-use soak | NOT TESTED | NONE |

## Gates and decision

G0: OPEN. G1: OPEN. G2: OPEN. G3: OPEN. G4: OPEN. G5: OPEN. G6: OPEN. G7: OPEN.

- P0/P1 defects: NOT ASSESSED; cannot approve until resolved.
- Accepted P2 exceptions, consequence/workaround and human acceptance: NONE RECORDED.
- Changes after last check / required reruns: NOT ASSESSED.
- Privacy and rights review of public attachments: PENDING.
- Human maintainer decision and date: PENDING.
- Beta approved: **FALSE**.

A zero verifier exit code is not a substitute for this evidence and decision. Do not remove an unknown by relabelling it PASS. Keep private identifiers out of the public copy.
