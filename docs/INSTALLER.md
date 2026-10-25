# Guided Sequoia installer

Status: **PLANNED — no installer implementation or installation test exists.**
Requested on 2026-10-25. Project baseline remains `26.1.1-alpha.14 — UNSTABLE ALPHA`.

## Objective and scope

Develop an option-driven installation assistant for this Sequoia project: select a USB, choose preparation preferences, review the planned changes and execute only the confirmed operations. Start with a readable terminal menu; a graphical interface may follow after the same underlying operations are validated.

The maintainer recalls a similar menu-based tool used during early EFI preparation or tests. Its exact identity has not been established from the available records. Reuse the requested interaction pattern without claiming that an existing tool or old script already implements this installer.

This is part of Sequoia development, separate from the [package-manager subproject](PACKAGE_MANAGER.md). It is a planned feature, not a new alpha, beta release or completed automation. Initial hardware scope is the recorded HP 22-dd0xxx / HP 86F3; no universal EFI generator is promised.

## Host environments

| Host | Planned role | Current evidence |
| --- | --- | --- |
| Installed macOS Sequoia | Primary new workflow: inspect media and prepare a candidate without rebooting into Fedora | Maintainer reports access to OpenCore files from macOS; installer NOT_TESTED |
| Fedora Workstation 44 | Preserve the established preparation/recovery workflow and evaluate a Linux adapter | Historical project preparation used Fedora; installer NOT_TESTED |
| Windows | No initial implementation or support commitment | Equivalent procedures are not developed or verified in this project |

Keep operating-system-specific disk operations behind explicit adapters. Do not translate Linux device names or commands directly into macOS commands.

> Host OS note: Linux remains recommended over Windows for the original preparation workflow, which was developed in Fedora 44 on this HP. A macOS-native workflow is now planned; it does not require performing every change from Fedora.

## Proposed menu flow

1. **Inspect the host.** Show OS/build, required tools, permissions, current root/system disk and all candidate media. Start in inspection-only mode.
2. **Choose an operation.** Inspect existing media; prepare a candidate in a local folder; update an existing boot USB; or prepare a new USB. Formatting is a separate, explicit option and is never selected by default.
3. **Select the USB.** Show model, capacity, connection protocol, current partition layout, mount points and a stable device identity in the local session. Recheck that identity immediately before any write. Stop if selection is ambiguous or the device was replaced/disconnected.
4. **Choose the media profile.** OpenCore plus online Recovery, or a full installer when a suitable user-obtained installer is present and the selected host adapter supports it.
5. **Select preferences.** Choose a validated HP hardware profile, source configuration, OpenCore logging level, output location, backup location and supported boot-menu options. Hardware-affecting overrides require an advanced view with their purpose and recovery implications.
6. **Resolve inputs.** Inspect a user-provided private EFI or a reviewed project profile and authorized upstream inputs. Report missing files and incompatible versions. Do not reconstruct unknown private state, rotate identities or fetch unreviewed binaries silently.
7. **Preview and validate.** Display exact target, affected files/partitions, required space, source versions/hashes, backup status and validation results. Prepare files in a staging directory before touching the selected media.
8. **Confirm and apply.** For a write, require confirmation tied to that specific target and plan. Any erase requires a separate explicit confirmation after the destructive effects are displayed.
9. **Verify and report.** Compare copied-file hashes, record results, explain the next manual boot step and preserve recovery instructions. Invoke the project's read-only installation verifier only when it has been implemented and is appropriate to the current stage.

Automated preparation does not imply unattended macOS installation. Disk selection inside Apple's installer, license acceptance, account creation, first boot and hardware validation remain explicit user steps until a separately tested scope says otherwise. Do not claim success merely because files were copied.

## Preferences and boundaries

| Option | Initial design requirement |
| --- | --- |
| USB and output folder | Explicit selection; show existing content and free space; do not assume a fixed disk number |
| Recovery or full-installer profile | Check real payload size, available space and host capability before preparing media |
| Hardware/configuration profile | Record exact profile revision and compatibility boundaries; reject unrecognized hardware rather than applying a generic EFI |
| OpenCore DEBUG/RELEASE and logging | Offer only validated, matching component sets; keep the known-working debug baseline available |
| Boot picker appearance and timeout | Optional, separate from hardware changes; validate the relevant configuration |
| Backup and report location | Outside the target being modified; verify backup readability and sufficient capacity |
| Existing EFI preservation | Produce a change plan; preserve unrelated loaders, especially Fedora; no blanket EFI-directory replacement |
| Identity and security settings | Preserve existing private identity by default; no automatic account-limit workaround, SIP/AMFI reduction or global NVRAM reset |

Do not expose an untested driver collection as a list of recommended switches. Advanced preferences remain unavailable until their dependencies and recovery behavior are understood.

## USB capacity and target protection

For the **OpenCore/online-Recovery profile**, retain the project requirement of at least **5 GB usable**, with **8 GB or larger recommended**; verify the selected payload fits. For a **full bootable macOS installer**, plan for **32 GB or larger** and verify actual requirements. These are different profiles, not interchangeable capacity claims. [Apple's full-installer instructions](https://support.apple.com/en-us/101578) apply to supported Macs and do not certify this HP.

Inspect the selected device's actual partition layout. A volume containing an EFI folder is not necessarily an EFI System Partition. Preserve working media until a separate tested preparation plan is approved.

An `external` flag, a volume name or a disk number alone is never sufficient to select an erase target. Identify and exclude the current root/system physical store, Linux/data partitions and source/rescue media, regardless of that flag. Revalidate device identity before writing because enumeration can change.

## Implementation and acceptance milestones

| Milestone | Deliverable / required evidence | State |
| --- | --- | --- |
| INS-01 — Inventory and menus | Read-only disk discovery, host adapters, preferences and preview; handle missing tools and ambiguous targets | PLANNED |
| INS-02 — Staging | Generate a local candidate, manifest and change report; validate plist syntax and use matching-version `ocvalidate` | PLANNED |
| INS-03 — Existing USB update | Verified backup, minimal file changes, hash verification and documented recovery on expendable test media | PLANNED |
| INS-04 — New USB preparation | Explicit erase flow; reject system/data/source disks; test full/undersized media, disconnects, permission failures and interrupted writes | PLANNED |
| INS-05 — Installation workflow | Test each claimed host/profile through manual installation and reboot, then collect actual hardware and recovery results | PLANNED |

Prototype against synthetic inventories first, including a system disk and a USB both reported as external. Synthetic tests do not validate physical writes. Physical preparation tests require expendable media, a separate working rescue path, verified backups and human operation. A failed/interrupted operation must retain an honest partial/failure result; filesystem-wide atomic rollback must not be promised.

The proposed Python 3 entry point is `scripts/install_sequoia.py`; bootstrap requirements and dependencies must be reviewed before creating it. Preferences should use a versioned, validated configuration format and keep private identity data outside public examples. No placeholder executable is added by this documentation.

The mandatory first-beta verifier remains `scripts/verify_installation.sh`, governed by [INSTALLATION_VERIFICATION.md](INSTALLATION_VERIFICATION.md). It is a separate read-only tool. The wizard's absence does not by itself add a beta gate, but a release claiming to include the wizard must satisfy its acceptance criteria in addition to G0–G7.

## Distribution and supervision

The installer must not bundle Apple installers, recovery images, proprietary frameworks/kexts, vendor firmware, credentials or a complete private EFI. Obtain required inputs through authorized sources under their applicable terms; legal restrictions are not removed by automating preparation. Review each third-party component's license and provenance.

This plan was AI-assisted under direct maintainer instruction. AI drafting and repository validation are not physical installation tests. Apply [LEGAL.md](../LEGAL.md), [AI_DISCLOSURE.md](../AI_DISCLOSURE.md), [SECURITY.md](../SECURITY.md) and the project's [testing procedure](TESTING.md).
