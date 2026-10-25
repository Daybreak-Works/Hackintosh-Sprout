# Roadmap and first-beta acceptance

**Current state: `26.1.1-alpha.14`, unstable. All gates below are OPEN unless an evidence-linked future record closes them.** This document creates no beta, release tag or scheduled hardware test.

## Next work

First re-establish the exact alpha.14 media, hashes and backup. Then investigate Bluetooth/internal USB, followed by a physical USB map. Later subjects include Apple services, microphone/jack, webcam, sustained Wi-Fi, Ethernet when a cable is available, sleep/wake, CPU/thermals, storage, internal dual boot/NVRAM, recovery, applications/security and controlled updates.

The old roadmap called these alpha.15–alpha.28+ slots. They are tentative work items, not executed versions. Failed hypotheses can change the order and numbering. Do not install proposed Bluetooth firmware or BlueToolFixup merely because it appears on the roadmap; first verify the actual device, upstream version and license.

## Gates

| Gate | Requirement | Current position |
| --- | --- | --- |
| G0 — Traceability | Exact same-build OpenCore, OS/build, kext/ACPI/patch revisions, hashes, config changes, backups and evidence; first-beta verifier implemented/tested | OPEN: active full EFI/state not recovered; verifier absent |
| G1 — Boot and recovery | [Boot campaign](TESTING.md), safe internal Fedora/Sequoia selection, working rescue USB and demonstrated restore | OPEN: desktop success does not meet the campaign |
| G2 — Data integrity | Verified configuration and data backups; safe storage validation and file restoration; Fedora preserved | OPEN |
| G3 — Daily graphics/function | Graphics under load, screen, audio output, input, Wi-Fi and ordinary apps usable on the candidate | OPEN: isolated successes only |
| G4 — Peripherals | Bluetooth, mic, camera if present, USB map and essential connectors; supported exceptions explicitly accepted | OPEN |
| G5 — Power | Repeatable shutdown/restart/sleep/wake with peripheral recovery and no panic/data loss | OPEN |
| G6 — Security/services | Document SIP/AMFI/FileVault posture, privacy, account/App Store limitations, update strategy and recovery | OPEN |
| G7 — Final regression | Entire required campaign including ≥48-hour soak on the exact candidate, no pending EFI changes and no P0/P1 defects | OPEN |

All gates must pass before `26.1.1-beta.1`. P0/P1 cannot be waived into a normal beta. A P2 feature may be excluded from a clearly named limited scope only with evidence, a documented consequence/workaround and explicit human acceptance; no excluded feature may be advertised as functional. The historical external Apple activation-limit exception does not certify account services.

## Mandatory verifier deliverables for beta.1

- [ ] Implement `scripts/verify_installation.sh` to the contract in [INSTALLATION_VERIFICATION.md](INSTALLATION_VERIFICATION.md).
- [ ] Validate syntax, parser fixtures and error handling; run on the actual candidate machine with the real USB and private manifest.
- [ ] Demonstrate wrong OS, missing/mismatched baseline, undersized/full USB, unavailable command and malformed input cases without destructive operations.
- [ ] Confirm no EFI/NVRAM/disk/config changes, no network uploads and no sensitive public report fields.
- [ ] Produce the sanitized machine report and completed human [installation verification record](../templates/INSTALLATION_VERIFICATION_REPORT.md).
- [ ] Record verifier revision, candidate code/config hashes, OS build, date/timezone, operator, manual evidence and exceptions.
- [ ] Re-run relevant checks after any candidate change; stale results cannot approve a different build.
- [ ] Human maintainer signs the release record and confirms G0–G7 before tagging/publishing beta.1.

The planned verifier must be developed and exercised during preparation of the first beta candidate, then ship with beta.1. Waiting until after publication would defeat this gate. An empty file, a documentation-only placeholder or a script that always exits zero is not an implementation.

## Release record

Use a release record containing exact scope, immutable commit/config identifiers, test report links, all known issues, accepted limitations, USB requirement, recovery instructions and upstream/license inventory. Beta means a defined experimental scope passed the recorded campaign; it does not mean Apple support, legal authorization, universal HP compatibility or a warranty.
