# Known issues and possible remedies

Snapshot: 2026-10-24, latest test alpha.14. These are evidence-limited project findings, not universal Hackintosh fixes. See [VERSION_HISTORY.md](VERSION_HISTORY.md) and [SOURCES.md](SOURCES.md). A proposed remedy remains untested until a named physical test records the outcome.

Severity describes impact: P0 data loss or no viable recovery; P1 unreliable boot/sleep, essential graphics/network/storage failure; P2 peripheral/service limitations; P3 cosmetic defects. Unknowns are not automatically confirmed defects. No P0 incident is established by this documentation.

| ID | Symptom / current status | Evidence | Possible remedy / investigation | Required closure evidence |
| --- | --- | --- | --- | --- |
| SEQ-001 | Earlier boot restart loop; latest desktop attempt passed, recurrence risk unresolved (P1 if recurrent) | S01–S03, S07 | Preserve alpha.14; compare exact EFI and actual loaded drivers; obtain panic evidence if reproducible | 5 cold boots, 5 restarts and Fedora round trips on the same build |
| SEQ-002 | White wallpaper/slow graphics in alpha.13; not observed in alpha.14, endurance unknown | S02–S06 | Preserve tested relative kext order; compare display report and workload after any change | 30 min 1080p video + 30 min GUI/graphics load, no corruption/freeze, repeated restart/wake |
| SEQ-003 | Bluetooth visible on USB but not operational in latest roadmap (P2) | S01/S03 | Map internal USB path; inspect exact upstream device match and firmware provenance before a reversible driver test | Pair a real device; reconnect after restart/sleep; record actual profile behavior |
| SEQ-004 | Wi-Fi worked in Recovery; 5 GHz issues and desktop reliability unresolved (P1 if essential networking fails) | S01/S03 | Hold driver versions constant; separate band/channel/security/signal tests; audit security modifications | 60 min desktop connectivity, 10 reconnects and wake recovery; document available bands |
| SEQ-005 | Microphone/jack unverified; speaker success user-reported (P2 if failed) | S02/S03 | Check endpoint, level and app permissions before layout experiments; revalidate speakers after alpha.14 | Listen to ≥60 s recording; verify jack switching and speaker output |
| SEQ-006 | Webcam untested | S03/S09 | Identify USB path and app permissions; inspect detection before adding drivers | Capture with two applications and document permissions |
| SEQ-007 | Apple Account creation limit and other authentication/App Store failures reported (P2) | S02/S03 | Separate account creation, iCloud login and Store download; check exact error, clock, network and service availability | Sanitized error-specific retest or an explicitly accepted service limitation |
| SEQ-008 | Depends on OpenCore USB; internal dual boot not validated (P1 for a release claiming autonomous boot) | S03 | Back up ESP and boot entries; plan internal boot only after a tested USB recovery path | Safe Fedora/Sequoia selection and recovery after a simulated configuration failure |
| SEQ-009 | No complete USB map / speed / reconnect validation | S03 | Map actual external and internal ports, including Bluetooth; do not assume an external hub | Port-by-port inventory, 2.0/3.x where supported, hot-plug and wake |
| SEQ-010 | Sleep, thermal, fan and CPU-power behavior unknown | S03 | Measure before introducing power-management changes; observe full peripheral recovery | 5 sleep/wake cycles, repeatable idle/load observations and no panic/data loss |
| SEQ-011 | APFS/NVMe/SATA integrity, recovery and endurance not established | S03 | Verify backups; safe scratch-file transfers with hashes, supported health reporting and restore exercise | No unexplained data mismatch; successful file and EFI restoration |
| SEQ-012 | Security posture, minor updates and application compatibility incomplete | S03 | Audit SIP/FileVault/AMFI-related state and each exception; stage updates only with rollback | Documented posture, tested recovery, application/regression results on the same build |
| SEQ-013 | Exact current EFI, private state JSON and active component hashes not recovered | Recovery audit / S03/S04 | Read-only collection from actual USB/HDD; stop mutations if baseline cannot be identified | Reproducible private inventory and verified backup; public sanitized manifest |
| SEQ-014 | Ethernet enumerated historically but no cable test | S03 | Keep untested until a real physical link is available | Link, DHCP/routing, sustained traffic and reconnect; no inferred PASS from `en0` |

## Diagnostic boundaries

- A kext appearing in a loaded list is not proof of audio playback, Bluetooth pairing or accelerated workload stability.
- The latest OpenCore log by filename stops earlier than another recovered log. Do not silently substitute the longer record as the chronologically latest one.
- `AAPL: #[EB|LOG:EXITBS:START]` indicates a recorded boot handoff milestone, not a proven kernel panic. No one-line fix is justified solely by that endpoint.
- A successful change of Internet connection after `PKDownloadError 8` supports a network investigation; it does not establish that every such error is caused by RTL88WiFi.
- An Apple Account limit is separate from local login and does not establish a faulty SMBIOS. Do not attempt to evade service limits with repeated identifiers or account creation.
- The exact current security settings are not established. Do not describe the installation as secure, fully protected or FileVault-ready merely because the desktop boots.

## Reopening and closing an issue

Record the version/build, issue ID, narrow change, before/after evidence and rollback. Close only the tested scope; for example, “speaker playback passed on alpha.N” does not close microphone or wake regressions. Record limitations without converting untested components into permanent incompatibilities. P0/P1 defects block beta. A P2 exception needs evidence, an accepted workaround or explicit scope reduction, and human sign-off in the release record.
