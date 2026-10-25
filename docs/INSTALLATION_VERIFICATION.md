# First-beta installation verifier specification

**Status: REQUIRED FUTURE IMPLEMENTATION — not an executable verifier.** Reserved file: `scripts/verify_installation.sh`. Implement and validate it during the first beta candidate, before publishing beta.1. Current alpha.14 does not meet beta acceptance. This file records the requirement now so it survives future chat/repository handovers.

## Purpose and limits

Check that the inspected installed Sequoia system and selected boot/recovery media match the declared release baseline, then report automatic findings and unresolved manual tests. It must not install macOS, generate identities, download proprietary files, repair a disk or claim that software inspection proves physical functionality.

Use a reviewed macOS-compatible shell implementation and system tools, with explicitly documented dependencies. The final implementation must fail safely when the environment is unsupported. Do not assume Linux tools, Python availability or a later Bash version on stock macOS without declaring and checking that dependency.

## Planned interface

```text
scripts/verify_installation.sh --efi-path <mounted-efi> --usb-device <device> --manifest <private-baseline> --output-dir <private-report-directory>
```

This is an interface contract, **not a runnable command in the current branch**. Paths/devices must be supplied explicitly and validated. Do not infer a safe target from a friendly volume name. Default behavior inspects only. Report generation may write only to the explicitly selected output directory; never overwrite existing reports silently. Do not automatically mount, erase, repair or modify the supplied devices.

## Required automatic checks

| Check ID | Required observation | Failure / uncertainty treatment |
| --- | --- | --- |
| ENV-001 | Running on Darwin and installed macOS major version 15; exact product/build recorded | Other OS/Recovery/unknown environment is FAIL or UNKNOWN, not a Sequoia PASS |
| BASE-001 | Explicit private manifest schema/version and intended candidate identity | Missing/malformed manifest blocks comparison; no arbitrary fallback baseline |
| EFI-001 | Selected EFI path, config syntax, required files, exact manifest hashes | Missing or changed files FAIL; no silent normalization of evidence |
| EFI-002 | Matching OpenCore `ocvalidate` and successful validation | Missing/mismatched validator UNKNOWN/FAIL, never a synthetic pass |
| EFI-003 | Kext entries/paths/enablement and candidate-specific relative order | Check against the candidate manifest; do not hard-code historical versions as forever required |
| BOOT-001 | Evidence linking active boot to the inspected EFI/config | A mounted valid EFI alone is insufficient; uncertainty blocks provenance PASS |
| GPU-001 | Display, driver and Metal capabilities reported | Missing capability FAIL; presence still needs manual workload validation |
| DEV-001 | Audio, USB, Bluetooth/network/storage enumeration where available | Label enumeration separately from functional tests |
| USB-001 | Explicit external USB identity/type, total bytes and usable/free capacity | Wrong type, ambiguity or missing size is UNKNOWN/FAIL; never select internal storage automatically |
| USB-002 | OpenCore/online-Recovery media has ≥5,000,000,000 usable bytes and sufficient free space for the actual required payload | Below threshold or payload will not fit: FAIL. Recommend ≥8 GB device; warn if below that recommended nominal size |
| USB-003 | If full-installer media is being checked, require declared full-installer profile and ≥32 GB device plus actual payload-fit check | A 5–8 GB OpenCore medium cannot pass as a full-installer medium |
| SAFE-001 | Backup/rescue references present and hashes verifiable where accessible | A recorded path alone does not prove a working restore; manual recovery remains pending |
| SEC-001 | Report readable security posture and unsupported checks | Never change SIP, AMFI-related settings, FileVault or NVRAM |

Capacity units must be explicit: decimal GB versus binary GiB. Report device size, usable filesystem capacity, free space, payload size and the applied profile separately. The 5 GB usable lower bound is the project's requested minimum; the historical tested device was 8 GB. Measure actual capacity instead of interpreting a product label as free space. Do not require an empty device after payload installation; measure the remaining required additions correctly.

## Results and reporting

Every check returns `PASS`, `FAIL`, `WARN`, `UNKNOWN`, `NOT_TESTED` or an explicitly justified `NOT_APPLICABLE`, with an evidence reference and reason. Missing permissions, unsupported parsers, stale data and command failure must not become PASS. Detect both command exit status and malformed/empty output. Do not rely on a pipeline's final command hiding an earlier error.

Produce private `installation-verification.json` (schema version 1) and a readable summary. Minimum fields: run ID, timestamp with offset, verifier revision, candidate version/commit, OS/build, private baseline digest, media profile/capacity, automatic checks, manual-test status, accepted exceptions and `beta_approved: false`. Only a separate human release record can approve a beta; a script must never set approval true automatically.

Proposed exit codes: `0` automatic checks completed with no failures/unknown mandatory checks (not beta certification); `1` failed check; `2` incomplete/unknown mandatory check; `64` invalid arguments; `69` unsupported environment/missing required tool. WARN and pending manual checks remain visible even after exit 0. Document precedence when multiple conditions occur.

## Manual verification remains mandatory

Cold boots, restarts, the selected boot medium, Fedora survival, USB rescue boot, physical audio/microphone/jack, Bluetooth pairing, actual camera capture, network traffic, sleep/wake, storage restore and sustained-use stability require human observation. Attach the completed [report template](../templates/INSTALLATION_VERIFICATION_REPORT.md) and evidence; a checkbox without supporting observation is not proof.

## Safety and privacy

- No `sudo` escalation by default, disk formatting, partition edits, NVRAM writes/resets, driver installs, firmware updates, config edits or network uploads. If a read requires more permission, report the limitation and a narrowly scoped manual alternative.
- Keep original reports private. Public exports must omit serial, MLB, SystemUUID, ROM, disk/display/USB serials, MAC/IP/SSID, account identifiers, tokens, personal paths and volume names. Hashing a sensitive value is not an automatic substitute for removal.
- Preserve original command evidence privately; publish only reviewed selections. Never claim automatic redaction is infallible.
- Avoid following untrusted paths outside explicit input scope, shell interpolation of manifest values, temporary-file races and destructive cleanup. Use structured parsing where supported, bounded execution and explicit failure handling.

## Required verification of the verifier

Use sanitized synthetic fixtures for success, wrong OS, bad/missing manifest, altered config, wrong validator, stale active-boot proof, undersized USB, insufficient payload space, unsupported disk layout, command timeout/failure, malformed output and accidental secret fields. Verify no changes to inputs and only expected report writes. Fixture success tests parsing, not HP compatibility. A real run and the manual campaign on the exact beta candidate are required before release.
