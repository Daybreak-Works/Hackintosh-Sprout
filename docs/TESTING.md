# Testing and recovery procedure

This preserves the working method used by the project. It is not a sequential installer recipe. Historical scripts target specific baselines and must not be run in numeric order against an arbitrary EFI.

## Before an experiment

1. Identify the real last-working configuration and selected USB. Read-only audit first: exact OpenCore version, OS version/build, config hash, kext/ACPI hashes, active boot arguments and target devices. An old report is not a substitute for the active files.
2. Make and verify an independent copy of the complete working EFI and private configuration/state. Record the hash manifest and backup location privately. Confirm the recovery USB actually boots.
3. Preserve Fedora's data, ESP and boot entries. Disk numbers and mount paths can change between operating systems; do not rely on a copied `/dev/diskN` or `/dev/sdX` from a previous session.
4. Check plist syntax and run `ocvalidate` from the matching OpenCore version on the original and candidate. A validator pass checks its scope; it is not a hardware or legal approval.
5. Write the hypothesis, exact files/keys to change, expected observations, failure criteria and rollback procedure using the [test record template](../templates/TEST_RECORD.md).
6. Limit a test to one or two related subsystems. Preserve the relative Lilu/NootedRed/AppleALC order unless the order itself is the explicit comparison.

Missing alpha.13/alpha.14 state JSON or a hash mismatch is a reason to re-establish the baseline, not fabricate state or disable old script checks. A historical script's default audit mode is safer to inspect than its `--apply`, but even an audit's implementation and assumptions must be reviewed.

## During and after a test

1. Prepare long operations in Fedora. Keep commands for macOS Recovery short and individually understandable.
2. Apply only the reviewed variant. Record the timestamp with timezone, selected boot entry/medium and version being tested.
3. Record direct output where possible; otherwise label a photograph transcription or human declaration. Include negative results and uncertainty. Preserve originals privately before redaction.
4. Stop when the specified failure criterion occurs. Return to the verified baseline using the separate recovery path. Do not erase APFS, alter Fedora or reset all NVRAM as an unplanned troubleshooting shortcut.
5. Compare hashes and relevant active state after rollback. A file restored successfully does not by itself prove that the next boot selected it.
6. Publish a sanitized record, update issue status and version history, and only then allocate the executed alpha number. An aborted or failed physical attempt remains a real result; a plan alone does not consume a number.

## Read-only evidence collection

The following commands are intended for **the installed macOS system**, when available. They are examples for future collection, not commands executed in this documentation session. Capture command, output, exit status and time. Output can contain private information and must be reviewed before publication.

```sh
sw_vers
uname -r
system_profiler SPDisplaysDataType
kmutil showloaded
system_profiler SPAudioDataType
system_profiler SPBluetoothDataType
system_profiler SPUSBDataType
diskutil list
csrutil status
fdesetup status
```

Some commands may be unavailable, require permission or produce incomplete output in Recovery. Record that as unavailable/unknown, not PASS. Do not publish complete `system_profiler`/USB/disk reports without removing serials, UUIDs, addresses and personal volume names. Never dump all NVRAM or account data into a public issue.

## Minimum regression campaign

These are project acceptance targets, not external certification standards.

| Area | Required exercise | Passing observation |
| --- | --- | --- |
| Boot | 5 cold boots and 5 consecutive restarts | Correct system, no panic/restart loop; exact selected EFI identified |
| Fedora / rescue | Fedora before and after tests; recovery USB boot independent of internal EFI | Fedora intact and a practical restore path available |
| Graphics | Display capabilities; 30 min 1080p playback and 30 min GUI/graphics activity | No white wallpaper regression, artifacts, freezes or unexplained restart |
| Audio | Speakers after boot/wake; ≥60 s mic recording; jack if present | Audible clean recording and correct output switching |
| Wi-Fi | ≥60 min normal desktop use; 10 reconnects; available 2.4/5 GHz networks | No unexplained essential connectivity loss; band-specific limits recorded |
| Bluetooth | Pair real peripheral; reconnect after restart and sleep | Actual profile operation, not enumeration alone |
| USB / camera | All accessible ports, internal devices and supported speeds; two camera apps | Correct map, reconnect and real camera capture |
| Sleep | 5 sleep/wake cycles | Display/audio/input/network recover; no panic or data loss |
| CPU / thermals | Record idle and sustained-load observations | No unexplained throttling/freeze; assess against valid hardware specifications rather than invented limits |
| Storage | Backed-up scratch-file copy/hash checks; supported health checks | No unexplained mismatch; no testing on irreplaceable data |
| Recovery | Restore known EFI and selected files from backup | Restoration demonstrated, with evidence tied to the backup |
| Updates / security | Inventory posture and limitations; controlled update only after recovery proven | Clear changes, usable rollback and repeated relevant regression checks |
| Soak | ≥48 hours of varied recorded use | No panic, unexplained data loss or unresolved P0/P1 defect |

If hardware or service access prevents a test, mark it NOT TESTED and state the limitation. A limited-scope beta may accept specific P2 exceptions through the process in [BETA_ACCEPTANCE.md](BETA_ACCEPTANCE.md); missing essential checks cannot be turned into PASS.

## Updates and rollback

Download and installation are separate decisions. Do not enable unattended installation until backup, dependency compatibility and rollback have been demonstrated. Retain a known-working rescue EFI across upgrades. Do not assume an APFS snapshot alone reverses firmware, EFI, NVRAM or all OS-update effects. Identify the layer being restored and verify it independently.
