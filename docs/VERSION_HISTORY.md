# Sequoia experimental version history

Snapshot: 2026-10-24. **Every `26.1.1-alpha.*` entry is unstable.** `26.1.1` is the project's year/version/subversion scheme, not macOS 26 or an Apple release. Alpha numbers count physical tests; proposals and documentation commits do not increment them. Historical 8A/8B are variants of one comparison.

Sources are indexed in [SOURCES.md](SOURCES.md). `DIRECT-LOG` means an original text record, `PHOTO-TRANSCRIPTION` means visible terminal/UI evidence, `USER-REPORTED` means a human observation preserved in project notes, `REPORT-SUMMARY` means a recovered report, and `HYPOTHESIS`/`PLANNED` are not successful tests. There is no complete per-version terminal transcript for the early tests.

## Version index

| Version | Main objective | Latest supported outcome |
| --- | --- | --- |
| alpha.1 | Initial EFI | Specific attribution incomplete |
| alpha.2 | Initial ACPI/hardware diagnosis | Specific attribution incomplete |
| alpha.3 | FixHPET / AMD baseline | Preparatory changes; full boot not demonstrated |
| alpha.4 | PCI initialization | Earlier boot blockage passed |
| alpha.5 | USB ownership | Failed to restore input |
| alpha.6 | USB Reset | Interactive Recovery |
| alpha.7 | SATA | HDD visible in Recovery |
| alpha.8 / 8A / 8B | Wi-Fi; audio introduced in 8B | Internet in Recovery; desktop reliability unproven |
| alpha.9 | GPU inspection | Drivers/services seen; Metal not established at that stage |
| alpha.10 | Audio inspection | Driver loading established; playback not yet tested |
| alpha.11 | Bluetooth enumeration | USB device visible; no functional pairing |
| alpha.12 | Installation / internal OS boot | Download error, later progress, then restart loop |
| alpha.13 | Reversible GPU A/B | First desktop; slow UI and white background |
| alpha.14 | NootedRed enablement/order | Desktop, wallpaper, Metal 3 / 2 GB VRAM observed |

Full project prefix for each row: `26.1.1-`. The outcome column describes the individual objective, never whole-system certification.

## alpha.1 — Initial EFI

- **Problem:** no usable macOS environment was established. No unequivocally alpha.1-labelled error or complete terminal record survives.
- **Hypothesis:** AMD CPU patches, UEFI drivers and machine-specific configuration were required. The exact causal blocker is unknown.
- **Changes:** an initial OpenCore DEBUG/Recovery baseline was prepared. Essential components appear in later inventories, but their precise first-introduction dates cannot be assigned reliably.
- **Latest evidence:** `REPORT-SUMMARY`, S01. Later cumulative configuration is not proof of each alpha.1 operation.
- **Possible remedy / next check:** establish a reproducible, validated baseline with a complete inventory and exact boot evidence; do not invent a missing panic.
- **Result and rollback:** incomplete historical attribution. Recovery depends on the original USB backup; no verified alpha.1 rollback artifact is published here.

## alpha.2 — ACPI investigation

- **Problem:** early initialization remained incomplete; no uniquely labelled alpha.2 log survives.
- **Hypothesis:** HP ACPI, the embedded controller and timer/IRQ descriptions needed investigation.
- **Changes:** DSDT/seven OEM SSDT extraction and analysis are documented. Activation of any individual injection in this exact version is not securely attributable.
- **Latest evidence:** `REPORT-SUMMARY`, S01 and S10–S12.
- **Possible remedy / next check:** derive narrowly scoped injections from the actual firmware; preserve OEM tables and the real EC unless a demonstrated reason requires otherwise.
- **Result and rollback:** analysis progress, not a complete boot. Remove only the identified experimental injections from a backed-up EFI; never replace firmware tables from an unrelated machine.

## alpha.3 — FixHPET and AMD preparation

- **Problem:** boot still stopped during early initialization.
- **Hypothesis:** HPET/PIC/TMR/RTC IRQ conflicts and AMD power-management expectations contributed.
- **Recorded changes:** `SSDT-EC-USBX-HP86F3.aml`, `SSDT-HPET.aml`, HPET `_STA`/`_CRS` renames, IRQ corrections and `DummyPowerManagement=True`. NootedRed remained enabled in the next test's prerequisite configuration.
- **Latest evidence:** `REPORT-SUMMARY`, S01, based on the later PCI test's baseline and ACPI reports. This is not a contemporaneous complete alpha.3 log.
- **Possible remedy:** retain the validated preparation while isolating the next boot blocker; do not claim these ACPI edits alone solved PCI initialization.
- **Result and rollback:** preparatory progress. Restore the pre-change EFI if reproducing a regression; original bytes must be available before applying a new variant.

## alpha.4 — PCI initialization

- **Problem:** boot stalled near `SMCRTC: start`; the last visible line is a location, not a proven root cause.
- **Hypothesis:** PCI/MMIO initialization on Raven2.
- **Recorded change:** add `npci=0x2000`, preserving the existing FixHPET/AMD baseline; the historical script also checked the Above 4G Decoding situation.
- **Latest evidence:** `REPORT-SUMMARY`, S01: the previous blockage was passed, while USB input remained unresolved. No new direct terminal capture has been recovered specifically for this version.
- **Possible remedy:** retain the tested setting on this baseline pending regression checks; do not add it blindly to other configurations.
- **Result and rollback:** partial objective passed. Restore previous boot arguments if the comparison regresses, recording actual NVRAM behavior rather than assuming a plist edit changed active arguments.

## alpha.5 — USB ownership experiment

- **Problem:** Recovery displayed, but directly connected keyboard and mouse did not respond.
- **Hypothesis:** firmware-to-OS USB ownership handoff.
- **Recorded change:** `ReleaseUsbOwnership=False` to `True`; `XhciPortLimit=False` retained.
- **Latest evidence:** `USER-REPORTED` via S01: keyboard/mouse still failed.
- **Possible remedy:** reverse this unsuccessful change and investigate board-specific USB/ACPI enumeration.
- **Result and rollback:** failed its objective; alpha.6 restored `ReleaseUsbOwnership=False`. The Genesys hub in topology is not evidence of an external user-installed hub.

## alpha.6 — USB Reset

- **Problem:** Recovery lacked working input.
- **Recorded changes:** restore `ReleaseUsbOwnership=False`; add board-derived `SSDT-USB-Reset.aml` for the relevant XHC controllers/ports. Preserve the other working settings.
- **Latest evidence:** `USER-REPORTED`/`REPORT-SUMMARY`, S01: keyboard and mouse worked in Recovery, and NVMe was visible.
- **Possible remedy:** preserve this baseline, then map physical/internal USB ports and test reconnect, speed and sleep separately.
- **Result and rollback:** interactive Recovery, but SATA remained absent. An original test-6 EFI backup was referenced in the source; its availability and integrity have not been re-established here.

## alpha.7 — SATA detection

- **Problem:** the Seagate HDD did not appear in Recovery although Fedora detected it; controller `1022:7901`.
- **Hypothesis:** missing AHCI device matching.
- **Recorded change:** add codeless `AMDSata.kext`, otherwise retaining the test-6 baseline.
- **Latest evidence:** `REPORT-SUMMARY`, S01/S09: disk visibility in Recovery. Historical config SHA-256: `c2024d1aa23392dae23882981a326f8cbcdf49b36fd4e2fcd9daf4a3a1eab3dd`; this is not the current alpha.14 config hash.
- **Possible remedy:** retain the matching injector and perform safe, backed-up storage validation later.
- **Result and rollback:** physical disk detection passed. No ext4 read/write or endurance claim. Restore the verified pre-AMDSata EFI if this isolated change causes trouble; do not format the data HDD as a diagnostic step.

## alpha.8 — Wi-Fi; variants 8A/8B

- **Problem:** RTL8821CE initially had no usable Wi-Fi; 5 GHz association was unreliable.
- **Hypothesis:** an experimental driver/supporting stack could provide connectivity; router channel/security, driver behavior and signal remain separate variables.
- **Recorded changes:** 8A introduced RTL88WiFi and supporting components, including AMFIPass, IOSkywalkFamily, IO80211FamilyLegacy and a Skywalk block. 8B added AppleALC and `alcid=55`.
- **Latest evidence:** `USER-REPORTED` via S01: Wi-Fi passed in Recovery. This does not establish desktop endurance, sleep recovery or a precise tested revision for every dependency.
- **Possible remedy:** preserve the working combination while measuring controlled 2.4/5 GHz reconnect behavior. Audit the exact dependency versions and security effects before further changes.
- **Result and rollback:** network objective partially passed. Return to the verified alpha.7 or the appropriate 8A/8B backup for isolation. Apple-derived Wi-Fi binaries mentioned historically are not included or licensed for redistribution by this repository.

## alpha.9 — GPU inspection

- **Problem:** visible Recovery graphics did not establish hardware acceleration.
- **Investigation:** inspect loaded NootedRed/AMDRadeonX6000 and IOAccelerator services. No unique EFI mutation is established for this test.
- **Latest evidence:** `REPORT-SUMMARY`, S01 records driver/services being present; no Metal result was established at that stage.
- **Possible remedy:** test the installed OS and capture display capabilities plus real graphics load. If boot failure recurs, isolate GPU changes reversibly.
- **Result and rollback:** inconclusive for acceleration; read-only inspection itself needs no rollback. Later alpha.14 evidence supersedes this limited graphics status for the later configuration.

## alpha.10 — Audio inspection

- **Problem:** speakers, microphone and jack had not been physically validated.
- **Investigation:** AppleALC/AppleHDA/Lilu loading; the audio additions came from 8B, not necessarily from a new alpha.10 edit.
- **Latest evidence:** `REPORT-SUMMARY`, S01: Lilu 1.7.2, AppleALC 1.9.8 and AppleHDA loaded. Loading alone did not prove sound output.
- **Possible remedy:** check actual endpoints and TCC permissions, then playback/recording. Investigate the historical layout/path discrepancy only after observing a real endpoint failure; change one layout at a time.
- **Result and rollback:** software presence established. Later alpha.13 speaker success is a separate user-reported test. Any new layout experiment requires a config/list backup.

## alpha.11 — Bluetooth enumeration

- **Problem:** no demonstrated pairing or usable Bluetooth profiles; webcam also untested.
- **Investigation:** USB enumeration identified Realtek `0bda:b00a` as a Bluetooth radio. No working firmware/driver intervention was demonstrated.
- **Latest evidence:** `REPORT-SUMMARY`, S01; S03 later records Bluetooth as non-operational. Presence on USB is the only positive result.
- **Possible remedy:** identify the internal USB path and exact supported device/firmware matching before considering an upstream driver. BlueToolFixup is an investigation candidate, not an installed or proven solution here.
- **Result and rollback:** enumeration only. No mutation-specific rollback is needed for the inspection; later driver tests need their own baseline and reversible plan.

## alpha.12 — Download, installation and restart loop

- **Problems:** `PKDownloadError 8` during download, then repeated restarts while booting the installed Sequoia entry. Other installer messages were recorded without demonstrated causal connection.
- **Hypotheses:** unstable download/connection for the first symptom; GPU/kernel/ACPI or an incomplete installation phase for the boot symptom. Neither is a proven single cause.
- **Recorded actions:** Sequoia APFS around 80 GiB on NVMe; change of Internet connection, after which installation progressed. The picker showed `macOS Installer` and later `Sequoia`.
- **Latest evidence:** S01/S02/S03 summarize the sequence. The latest recovered boot log to reach the handoff, S07, ends `77:017 00:064 AAPL: #[EB|LOG:EXITBS:START] 2026-10-23T20:18:05`. The later S08 ends earlier in console setup. The files are associated with this period; exact one-to-one variant attribution is unavailable.
- **Possible remedy:** preserve APFS/Fedora, capture a real panic if available, and isolate GPU enablement without deleting the installation. A 404 from an unrelated Apple root URL does not prove the actual installer package is reachable or intact.
- **Result and rollback:** the historical catalogue did not yet establish a desktop; later reports establish subsequent installation success. Restore a known-working EFI, not an arbitrary filesystem snapshot, and assess any storage recovery separately. `EXITBS:START` alone is not a panic or a diagnosis.

## alpha.13 — First installed desktop

- **Problem:** alpha.12 restart loop.
- **Hypothesis and comparison:** disable NootedRed to isolate GPU involvement; a separate no-acceleration variant was proposed but must not be recorded as executed without evidence.
- **Recorded action:** the later roadmap says the successful run had NootedRed disabled. The contemporaneous S02 report explicitly lacked the final `--apply disable` transcript and initially left this attribution open. Preserve that distinction; no missing transcript is fabricated.
- **Latest evidence:** `PHOTO-TRANSCRIPTION`/`USER-REPORTED` summarized in S02/S03: Setup Assistant and desktop, good speaker output, slow UI and white wallpaper. S03 records a basic 7 MB framebuffer in that phase.
- **Additional errors:** microphone uncertain; new Apple Account creation encountered an account-creation limit. This is different from the local user account, which had been created successfully.
- **Possible remedy:** retain the booting baseline and inspect graphics. Alpha.14 then tested NootedRed ordering. Investigate microphone independently; do not rotate machine identities or reset NVRAM to bypass account restrictions.
- **Result and rollback:** first desktop, partial hardware validation. Preserve this fallback before re-enabling acceleration; the private state JSON and exact current EFI were not recovered.

## alpha.14 — NootedRed ordering and acceleration

- **Problem:** alpha.13 had poor graphics/white wallpaper with the GPU driver disabled in the later account of the sequence.
- **Hypothesis:** the existing NootedRed could work when enabled before AppleALC, after Lilu.
- **Recorded change:** S04 re-enables the same NootedRed entry and moves it to preserve relative `Lilu < NootedRed < AppleALC`. Other kext entries remain; this is not a full load list. The script deliberately leaves boot arguments, AMD patches, ACPI, Wi-Fi, SATA and APFS unchanged.
- **Latest direct observation:** S05/S06 terminal photographs show Metal 3, 2 GB VRAM, 1920×1080 and loaded Lilu 1.7.2 / NootedRed 0.8.10 / AppleALC 1.9.8. See [LATEST_EVIDENCE.md](LATEST_EVIDENCE.md) for selected transcription and its limits. A functioning wallpaper is visible and reported in S03.
- **Possible remedy:** preserve this exact baseline and run the graphics/audio/boot regression suite before further driver changes. Success is consistent with the order hypothesis but does not prove universal causality or suitability for other machines.
- **Result and rollback:** the graphics/desktop objective passed observationally. No benchmark, 48-hour soak, repeated sleep or overall stability pass is established. S04's rollback depends on its verified private backup/state and refuses unexpected baselines; do not bypass those checks.

## Unexecuted work

Bluetooth/internal USB is the next proposed objective, historically called the alpha.15 slot. **It is not an executed alpha.15 or a working Bluetooth solution.** Subsequent numbers may change with failed tests and new hypotheses. Beta.1 remains blocked by [BETA_ACCEPTANCE.md](BETA_ACCEPTANCE.md), including the missing implementation and validation of the installation verifier.
