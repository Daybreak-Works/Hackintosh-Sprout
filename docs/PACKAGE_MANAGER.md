# Multi-architecture package manager

Status: **PLANNED — specification only; no implementation or package installation has been tested.**
Decision recorded: 2026-10-25, America/Santiago.

## Relationship to HP86F3-Hackintosh

The maintainer requested a separate package-manager development track within the project, prioritizing continued access to software on x86_64 and extending to arm64. It has its own scope, milestones, test matrix and eventual versioning. It is not an OpenCore patch, a new Hackintosh alpha or a requirement for the first Sequoia beta.

The project-wide specification is maintained in `main`, with a matching copy in `Sequoia` for integration planning. `main` remains documentation-only. A future Sequoia prototype may live under `package-manager/` in the `Sequoia` branch, separate from boot scripts, EFI material and hardware diagnostics. No implementation directory or additional repository is created by this specification.

Planning may proceed now. Testing on the HP must first establish a recorded, recoverable Sequoia baseline. The existing hardware and beta acceptance work remains the priority. Tahoe development retains its existing prerequisite: an accepted Sequoia beta or completion of the Sequoia project.

## Motivation and terminology

As reviewed on 2026-10-25, Homebrew's macOS installer rejects non-arm64 hosts. Its support policy places Intel macOS in Tier 3, has stopped new Intel bottle builds and schedules removal of Intel execution in or after September 2027. Existing x86_64 installations may still work. These are different constraints: installation policy, binary availability and existing-runtime support. [1][2]

The objective is sustainable package management across architectures, with explicit compatibility information. It must not be justified by a claim that Homebrew never supported Intel or that every package already runs on this AMD HP.

Here, **multi-architecture** means x86_64 and arm64 support. Intel and AMD are processor vendors, not two different software architectures in this target. Multi-core compilation is a separate resource-management feature; it does not provide cross-architecture compatibility.

## Target matrix

| Target | Priority and scope | Evidence status |
| --- | --- | --- |
| macOS Sequoia 15, AMD x86_64, HP 86F3 | First integration target; validate individual packages on the actual Athlon 3050U | NOT_TESTED |
| macOS Sequoia 15, Intel x86_64 Mac | Same architecture, separate hardware and runtime validation | NOT_TESTED; test host required |
| macOS Sequoia 15, Apple Silicon arm64 | Second implementation milestone, using native arm64 packages | NOT_TESTED; test host or suitable macOS runner required |
| Other macOS releases, including Tahoe | Add explicit OS/build/architecture combinations only after testing | Deferred |
| Linux x86_64 / arm64 | Possible later adapter; preserve portability in the design without claiming support | Outside the initial scope |

Select packages using OS version, architecture, ABI, CPU feature requirements and dependency compatibility. Do not equate x86_64 with guaranteed Intel/AMD interchangeability for every application. Do not publish generic x86_64 binaries built with machine-specific instruction assumptions without declaring those requirements.

An arm64-only application does not become runnable on this AMD computer because a package manager downloads it. The manager must reject incompatible artifacts or offer an independently available compatible build. Universal binaries are acceptable only when they contain a suitable slice and satisfy the other requirements. Cross-architecture emulation is outside the initial scope.

## Proposed implementation approach

Start with a project-owned command-line interface and a **MacPorts adapter**. MacPorts exposes architecture and OS constraints in its recipes and supports preview and binary-only operations. Availability still varies by package, architecture and macOS release. [3][4]

This first prototype would be a management interface over MacPorts, not a newly implemented dependency solver or an independent package repository. MacPorts would retain ownership of its installed files and registry. The adapter must not edit that registry directly, adopt Homebrew files or silently migrate an existing installation.

Use an adapter boundary so a future native backend can be evaluated separately. Building a full independent ecosystem also requires recipes, build workers, artifact hosting, signing, updates and maintainers; a new command name alone does not supply those capabilities. The implementation language, executable name and distribution format remain undecided.

The manager itself must have a documented bootstrap path that does not require a working Homebrew installation. Prefer a small distributable native executable per architecture or another explicitly provided runtime; verify its macOS deployment target before choosing a language/toolchain.

## Initial functional requirements

- Search packages, inspect metadata, list installed/requested packages and report available updates.
- Provide read-only environment diagnostics: OS/build, hardware and process architecture, existing managers, prefix, developer tools and available storage.
- Preview dependency changes before installation, upgrade or removal. Keep repository-metadata refresh separate from upgrading installed packages.
- Prefer existing compatible binary packages. If none is available, stop with a clear explanation; source compilation requires an explicit user choice and resource estimate.
- Install, upgrade and remove a small selected package set through the backend while respecting dependencies and file ownership.
- Export a versioned inventory and import it as a reviewed plan. Record exact package versions/revisions, variants, architecture, backend and source/index revision where available. Report unavailable versions instead of silently substituting them.
- Preserve backend exit codes, diagnostic output and partial-completion information. Never label an interrupted multi-package operation as fully rolled back without evidence.

The first candidate set is `jq`, `ripgrep` and `fzf`, matching the existing terminal-tools plan. Their inclusion here is a test proposal, not a claim that compatible archives are currently available or installed.

## Integrity, isolation and recovery requirements

- Invoke validated backend commands with argument arrays rather than constructing executable shell strings from package names.
- Keep diagnostics unprivileged. Request elevated privileges only for operations that actually require them; show the affected prefix and intended changes.
- Use backend verification for its archives. Any future project-owned catalog must authenticate metadata and artifacts, verify hashes, enforce allowed extraction paths and have a documented signing-key lifecycle. A checksum alone does not authenticate its source.
- Record before/after inventories and operation logs. Recovery must respect existing packages and dependent applications; do not promise atomic rollback across arbitrary upstream installation scripts.
- Do not change EFI, NVRAM, SIP, AMFI, SMBIOS, firmware or the macOS system volume as part of package management. Keep manager-owned paths separate from other managers and system files.
- Avoid automatic source builds on the 2-core/2-thread HP. If source builds are later supported, expose conservative concurrency and storage controls.
- Keep personal paths, credentials and machine identifiers out of public reports. Publish only reviewed, sanitized diagnostics.

## Milestones and acceptance

| Milestone | Deliverable and acceptance evidence | State |
| --- | --- | --- |
| PM-01 — Design | Review this scope, choose bootstrap/runtime strategy and confirm the first test hosts | Specification prepared; human design acceptance pending |
| PM-02 — Read-only prototype | CLI search, metadata, inventory, architecture detection and preview; absent-backend and incompatible-target cases handled | PLANNED |
| PM-03 — Sequoia x86_64 prototype | Controlled install/upgrade/remove of the candidate set, dependency handling, missing-archive and interrupted-operation tests | PLANNED |
| PM-04 — Multi-architecture validation | Native arm64 build and execution; independent Intel x86_64 and AMD x86_64 evidence; correct artifact selection and mismatch rejection | PLANNED |
| PM-05 — Independent backend evaluation | Assess maintenance capacity and whether a native catalog/solver adds enough value; approve its trust and recovery design before implementation | DEFERRED; not a promised deliverable |

Record each result as PASS, PARTIAL, FAIL, INCONCLUSIVE or NOT_TESTED with the exact manager revision, backend version, OS build, CPU/architecture, package versions and sanitized output. A mocked test or successful cross-compilation is not proof of execution on another architecture.

Before advertising a multi-architecture release, require real execution evidence for each advertised target, a reproducible installation procedure, dependency/removal tests, a verified recovery procedure and human release acceptance. The package manager will use its own version history; package-manager milestones must not increment the HP's physical alpha numbers.

A graphical interface, large independent package catalog, automatic migration, automatic OS upgrades, Windows support and additional CPU architectures are outside the initial scope. They may be evaluated later without blocking Sequoia stabilization.

## Naming, AI assistance and distribution

Use conventional future names such as `package-manager/README.md`, `CHANGELOG.md`, `src/`, `tests/` and `docs/`. These are proposed paths, not existing implementation files. Follow the repository's naming and evidence rules.

This specification was prepared with OpenAI ChatGPT/Codex assistance under the maintainer's direct instructions. AI may assist with research, design, code and test preparation; the human maintainer supervises decisions and release acceptance. No machine tests are represented by this document.

The existing [AI disclosure](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/AI_DISCLOSURE.md), [legal notice](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/LEGAL.md) and [security policy](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/SECURITY.md) apply. Decide and document an explicit license before distributing project-authored implementation. Retain upstream notices and verify redistribution rights before hosting any package. This track does not include Apple installers, proprietary frameworks/kexts, firmware, credentials or private EFI bundles.

## Primary references

Reviewed on 2026-10-25; upstream policy and package coverage may change.

1. [Homebrew support tiers](https://docs.brew.sh/Support-Tiers).
2. [Homebrew installation script](https://github.com/Homebrew/install/blob/HEAD/install.sh), macOS architecture check. This is a moving upstream reference, not a pinned project dependency.
3. [MacPorts Portfile reference](https://guide.macports.org/chunked/reference.html), `supported_archs`, `platforms` and deployment-target metadata.
4. [MacPorts port manual](https://man.macports.org/port.1.html), dry-run, binary-only and activation/deactivation behavior.
