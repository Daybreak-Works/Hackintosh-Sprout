<p align="center">
  <img src="assets/images/sequoia-banner.png" alt="Sequoia — HP86F3-Hackintosh: macOS compatibility research" width="100%">
</p>

# HP86F3-Hackintosh — Sequoia

Experimental macOS Sequoia compatibility research for the HP All-in-One 22-dd0xxx with motherboard HP 86F3, AMD Athlon Silver 3050U and Radeon Raven2.

**Status: UNSTABLE ALPHA. Latest evidenced physical test: `26.1.1-alpha.14`. No beta or stable release exists.** Documentation snapshot: 2026-10-25, America/Santiago. This repository is a research record, not a complete EFI distribution, an Apple-supported installation or a guarantee of compatibility.

The tested machine reached the Sequoia desktop. The latest terminal photographs show Metal 3, 2 GB reported VRAM, 1920×1080 and loaded Lilu/NootedRed/AppleALC. Sustained graphics, power, peripherals, recovery and dual-boot reliability remain incompletely tested. The full active EFI and its private state files were not recovered; the documentation alone cannot reproduce an exact working installation.

## Start here

| Document | Contents |
| --- | --- |
| [Version history](docs/VERSION_HISTORY.md) | alpha.1–alpha.14, errors, hypotheses, changes, results and rollback limits |
| [Latest evidence](docs/LATEST_EVIDENCE.md) | Latest terminal observations, user declarations, source hashes and evidence gaps |
| [Project gallery](docs/GALLERY.md) | Real desktop captures with privacy redactions and evidence limits |
| [Guided installer](docs/INSTALLER.md) | Planned USB/preferences wizard, staging, backups, target protection and acceptance |
| [Hardware and software](docs/HARDWARE.md) | Actual test machine, recorded versions and compatibility limits |
| [Known issues](docs/KNOWN_ISSUES.md) | Current defects, possible remedies and evidence needed to close them |
| [Terminal and system tools](docs/SYSTEM_TOOLS.md) | Proposed minor patch for alpha.14: Fedora tool equivalents, MacPorts setup, shell plugins and pending validation |
| [Package-manager subproject](docs/PACKAGE_MANAGER.md) | Separate planned multi-architecture manager: x86_64 first, arm64 next; scope, milestones and acceptance |
| [Testing procedure](docs/TESTING.md) | Backups, one-change experiments, recovery and repeatable acceptance tests |
| [Roadmap and beta gates](docs/BETA_ACCEPTANCE.md) | Pending work and mandatory G0–G7 release criteria |
| [Installation verification](docs/INSTALLATION_VERIFICATION.md) | Required verifier to implement and validate for the first beta |
| [Naming conventions](docs/NAMING.md) | Standard filenames, test IDs, dates and historical-name mapping |
| [Evidence provenance](docs/SOURCES.md) | Original source descriptions and SHA-256 fingerprints |
| [AI disclosure](AI_DISCLOSURE.md) | AI assistance, direct human supervision and limitations |
| [Legal notice](LEGAL.md) | License restrictions, liability limits and excluded materials |
| [Third-party notices](THIRD_PARTY_NOTICES.md) | Upstream attribution and redistribution review |
| [Security](SECURITY.md) | Privacy, safe reporting and sensitive files |
| [Contributing](CONTRIBUTING.md) | Evidence and publication requirements |
| [Changelog](CHANGELOG.md) | Repository documentation changes, separate from physical test versions |

## Required USB for Sequoia

**Keep a dedicated USB for the Sequoia OpenCore/online-Recovery workflow: minimum 5 GB usable capacity, with an 8 GB or larger device recommended. The recorded project setup used an 8 GB USB.** The requested 5–8 GB range concerns this boot/recovery medium, not the full macOS installer or a macOS system disk. The 5 GB lower bound is a project requirement, not a separately tested capacity guarantee: measure the selected payload and available space before preparing media, and use a larger device if it does not fit.

For a **full bootable macOS installer, use 32 GB or larger**. Apple's [bootable-installer documentation](https://support.apple.com/en-us/101578) states that 32 GB has sufficient space for any macOS installer. A 5–8 GB USB must not be advertised as holding the full Sequoia installer. Apple's instructions concern supported Macs and do not establish support for this HP.

Keep the known-working rescue USB available throughout testing. Preparation can erase the selected USB; positively identify the device and back up its contents first. Preserve Fedora's partitions, EFI and boot entries. The historical approximately 80 GiB APFS allocation is an observation, not a recommended minimum or permission to repartition another machine.

> **Host OS note:** Linux is recommended over Windows as the host environment for this project's preparation and installation workflow. The host-side work was carried out entirely in Fedora Workstation 44 on this same HP All-in-One 22-dd0xxx (HP 86F3). The maintainer is not familiar with the equivalent Windows-based procedures, which have not been developed or verified in this project.

## Latest recorded configuration

| Item | Recorded value / limitation |
| --- | --- |
| Project version | `26.1.1-alpha.14`; project numbering, not an Apple OS version |
| OS | Sequoia 15.8.1 according to saved reports; capture a fresh `sw_vers` and build number before another test |
| Bootloader | OpenCore 1.0.8 DEBUG on separate USB |
| Last successful change | Re-enable the existing NootedRed and move it before AppleALC, preserving `Lilu < NootedRed < AppleALC` |
| Current confidence | Desktop and graphics objective observed; global stability unproven |
| Next proposed work | Audit the real alpha.14 baseline; then investigate Bluetooth/internal USB |

The relative kext order above is not the full `Kernel/Add` list and is not a universal prescription for other hardware. No new physical alpha test was performed while writing this documentation.

The maintainer has scoped the terminal/system-tool additions and Siri investigation as a **minor patch to alpha.14**. The [terminal and system tools plan](docs/SYSTEM_TOOLS.md) is prepared for physical testing; no package installation or new release is claimed. Native “Hey Siri” remains a separate, unresolved investigation: no working boot argument, system-file patch or native wake-word activation has been verified on this HP.

## Guided installer — planned

Develop an [option-driven Sequoia installer](docs/INSTALLER.md) with USB selection, media profile and preferences, local staging, backups, a change preview and explicit confirmation before writes. Installed macOS is the primary new workflow, with the established Fedora workflow retained for preparation/recovery. The installer is not implemented or tested.

The future selector must protect system/data/source disks and must never identify an erase target solely by an external flag or a remembered disk number.

The [gallery](docs/GALLERY.md) includes the maintainer's desktop capture with the serial number and weather location redacted. It is a visual record, not a stability certification.

## Separate package-manager development track

The [multi-architecture package manager](docs/PACKAGE_MANAGER.md) is a separate planned subproject, with x86_64 support for AMD/Intel as the first target and native arm64 support as the next milestone. Its proposed first prototype uses a project-owned CLI over MacPorts; an independent package backend requires a later feasibility decision.

No manager implementation, installation or architecture test exists yet. This development track has its own milestones and eventual versions; it is not part of the current alpha.14 minor patch and does not add a first-beta acceptance gate. Sequoia hardware stabilization remains the priority.

## First-beta installation verifier

Before publishing `26.1.1-beta.1`, the project **must create, review and test `scripts/verify_installation.sh`**, as specified in [INSTALLATION_VERIFICATION.md](docs/INSTALLATION_VERIFICATION.md), and attach a sanitized installation-verification report to that exact release candidate. The script must inspect the installed system, configuration provenance and rescue-media requirements without modifying EFI, NVRAM or disks. Manual boot, audio, sleep, recovery and sustained-use tests remain mandatory.

**The verifier is not implemented in this alpha documentation commit.** Its absence blocks beta promotion. Neither this README, a template nor an automated PASS alone certifies an installation. The future file's name is reserved and must not be replaced by an always-successful placeholder.

## Branches

| Branch | Scope |
| --- | --- |
| [`main`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/main) | Default branch; documentation only |
| [`Sequoia`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/Sequoia) | Sequoia-specific development and documentation; this branch |
| [`Tahoe`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/Tahoe) | Not developed yet; work begins after Sequoia reaches its first accepted beta or the Sequoia project is completed |

Keep implementation changes in the relevant macOS branch. Copy or cherry-pick reviewed documentation to `main` without bringing implementation files with it. Branch names are case-sensitive. Repository files use English; maintainer discussion may use Spanish.

## Scope and notices

This extremely complex firmware/ACPI/AMD/driver project uses **OpenAI ChatGPT/Codex as a supervised technical assistant** for research, interpretation, drafting and code preparation. The human maintainer directs the work, operates the physical machine and decides whether evidence supports a test or release. AI assistance is not hardware testing or legal review; see [AI_DISCLOSURE.md](AI_DISCLOSURE.md).

Apple's macOS Sequoia license restricts use on non-Apple-branded computers. Calling this work educational or experimental does not remove those restrictions. This repository supplies no Apple installer, recovery image, proprietary extracted kext, firmware, activation credential or complete private EFI. Read [LEGAL.md](LEGAL.md) before relying on the material. No affiliation with Apple, HP, AMD or upstream projects is claimed.

The banner artwork and generation process are documented in [assets/README.md](assets/README.md).
