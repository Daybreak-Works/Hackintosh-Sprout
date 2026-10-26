# Extra development projects

Planning date: 2026-10-26, America/Santiago. This document coordinates software-development work; it records no new physical experiment. The evidenced Hackintosh baseline remains **26.1.1-alpha.14 — UNSTABLE ALPHA**.

## Work register

All five issues are open planning/development tasks. An open issue, checklist or development branch does not mean a feature is implemented or a physical test has passed.

| Priority | Track | GitHub task | Initial deliverable | Requires the HP? |
| --- | --- | --- | --- | --- |
| 1 | Guided installer | [INS-01: inventory and preview](https://github.com/Vynzaro/HP86F3-Hackintosh/issues/1) | Read-only host/media inventory, preferences and operation preview | No for design/fixtures; yes for HP integration |
| 2 | Package manager | [PM-01: design and bootstrap](https://github.com/Vynzaro/HP86F3-Hackintosh/issues/2) | Architecture decision and MacPorts adapter contract | No for design; real macOS targets required for runtime claims |
| 3 | Terminal/system tools | [Reproducible profiles](https://github.com/Vynzaro/HP86F3-Hackintosh/issues/3) | Small core/optional profiles with preview and recovery requirements | No for planning; yes for Sequoia acceptance on the HP |
| 4 | Installation verifier | [Baseline schema and fixtures](https://github.com/Vynzaro/HP86F3-Hackintosh/issues/4) | Manifest contract and negative/positive synthetic cases | No for preparation; real candidate required before beta |
| Deferred integration | Multi-EFI | [Shared/profile architecture](https://github.com/Vynzaro/HP86F3-Hackintosh/issues/5) | Feasibility and rejection conditions, design only | Yes for each claimed OS/boot configuration |

Priorities describe the suggested development order, not deadlines or physical alpha numbers. Design work may overlap where dependencies allow it.

## Immediate work: installer inspection stage

The first implementation target is INS-01 in [INSTALLER.md](INSTALLER.md), using the proposed conventional entry point `scripts/install_sequoia.py`. Review bootstrap/dependencies and licensing before implementation distribution. This planning change does not create that executable.

The first stage must identify the host, discover media through explicit Linux/macOS adapters, distinguish media profiles and produce a readable preview. It must handle missing tools, unknown sizes, unsupported layouts, ambiguous devices and the system disk being reported as external. Friendly labels and remembered disk numbers are insufficient to select a target.

Start with sanitized synthetic inventories. A later maintainer-run inspection on an available development computer may validate its host adapter, but cannot validate the absent HP or installed macOS. Keep fixture results and real-host observations separate.

Formatting, automatic mounts, downloads, EFI installation, boot-entry edits and package installation are not part of INS-01. Staging and writes have separate milestones and require appropriate recovery checks. The online-Recovery profile requires at least **5 GB usable**, with **8 GB or larger recommended**; full-installer media requires **32 GB or larger** plus an actual payload-fit check.

## Track boundaries and dependencies

### Package manager

[PACKAGE_MANAGER.md](PACKAGE_MANAGER.md) remains the authoritative specification. The first design uses an adapter over MacPorts; it does not promise a new dependency solver, package catalog or independent binary infrastructure. x86_64 covers both Intel and AMD vendors; arm64 is a different architecture and needs its own native execution evidence. Neither an architecture string nor a successful download proves application compatibility.

Choose language/runtime, bootstrap and implementation licensing explicitly. Keep the future prototype isolated under `package-manager/` in Sequoia. Do not silently compile missing archives, migrate other managers or adopt their files. This track has its own development lifecycle and is not an automatic beta gate for Sequoia.

### Terminal and system tools

[SYSTEM_TOOLS.md](SYSTEM_TOOLS.md) defines the candidate utilities. Package profiles and reversible shell configuration are separate from the package-manager implementation. Inspect existing installations first; preserve system utilities, existing managers and the effective Zsh configuration location. Actual package availability and upstream instructions must be rechecked when implementation begins.

Native Siri is a separate investigation in [SIRI.md](SIRI.md); it is not implemented or verified by adding terminal utilities.

### Installation verifier

[INSTALLATION_VERIFICATION.md](INSTALLATION_VERIFICATION.md) governs the reserved `scripts/verify_installation.sh`. Schema/fixture preparation may proceed now; the actual verifier must be implemented and validated during first-beta candidate preparation. No always-successful placeholder is acceptable.

Automatic findings must preserve FAIL/UNKNOWN/NOT_TESTED states and evidence limits. A mounted valid EFI is not proof it was used to boot. The verifier cannot approve a release: reports retain `beta_approved: false`, and [BETA_ACCEPTANCE.md](BETA_ACCEPTANCE.md) remains mandatory.

### Multi-EFI

Begin with a common-input/profile design, not a universal ready-to-boot bundle. Review the exact upstream OpenCore version's conditional capabilities before assigning settings to OS profiles; not every ACPI/UEFI/global setting can vary per selected OS.

Prefer separately generated, independently validated candidates before considering a unified output. Require explicit component compatibility, conflict checks, preserved private identity, a matching validator, backup/rescue and independent regression evidence for every advertised OS. Reject a unified design when shared/global settings conflict.

Tahoe implementation and physical testing retain the agreed gate: an accepted Sequoia beta or completion of Sequoia. This design issue does not open the Tahoe implementation track or claim existing Sequoia drivers support it.

## GitHub workflow

1. Use one scoped issue with deliverables and acceptance criteria per development objective. Link related specifications instead of copying machine logs into issue bodies.
2. Branch from current `Sequoia` for implementation; conventional examples are `feature/installer-inventory`, `feature/package-manager-cli` and `docs/extra-projects`. Examples are not claims that those branches exist.
3. Make focused commits and open a pull request targeting `Sequoia`. Reference the issue with `Refs #N` while work is partial; use a closing reference only when its complete acceptance criteria are met.
4. Record checks actually performed, fixture provenance and unresolved platform/hardware validation. A CI or syntax PASS is not HP compatibility evidence.
5. Request human review for design/release decisions. Keep project release approval separate from merging development work.
6. Keep `main` documentation-only. Propagate reviewed documentation separately; do not merge a Sequoia implementation tree into main. Preserve exact branch names `main`, `Sequoia` and `Tahoe`.

Issues are the live work queue; this index links the tracks and their dependencies. Use existing GitHub issue numbers rather than inventing physical-test IDs for development. No GitHub Project board, scheduled deadline, release tag or milestone object is implied by this document.

## Development acceptance and evidence

| Evidence | What it can establish | What it cannot establish |
| --- | --- | --- |
| Static review/syntax checks | Structure and the particular checked rules | Successful execution or hardware behavior |
| Synthetic fixtures | Parsing/decision behavior for the covered inputs | Real device identity, permissions or platform support |
| Actual Linux execution | Observed behavior on the recorded Linux host | Darwin execution or HP compatibility |
| Actual macOS execution | Observed behavior on that exact OS/build/architecture | Another architecture, another machine or long-term stability |
| Physical HP campaign | The explicitly observed objectives on that candidate | Universal support or automatic release acceptance |

Use the naming rules in [NAMING.md](NAMING.md). Record development revisions, commands, host or fixture context and limitations in pull requests. Use [TESTING.md](TESTING.md) and the physical-test template only for real hardware experiments; preparation does not allocate alpha.15.

## Supervision and distribution

This coordination document and issue drafting were AI-assisted under the maintainer's direct instruction. No live access to the HP or Aspire is implied. Human decisions, real host runs and release acceptance must be recorded separately.

Apply [AI_DISCLOSURE.md](../AI_DISCLOSURE.md), [LEGAL.md](../LEGAL.md) and [SECURITY.md](../SECURITY.md). No new license is selected here. Keep private EFI/config/state, identifying diagnostics, credentials, Apple payloads, firmware and unreviewed third-party binaries out of public changes.
