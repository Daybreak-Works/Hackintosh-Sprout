<p align="center">
  <img src="assets/images/sequoia-banner.png" alt="Sequoia — HP86F3-Hackintosh: macOS compatibility research" width="100%">
</p>

# HP86F3-Hackintosh
Experimental macOS Sequoia and Tahoe compatibility research for the HP 22-dd0xxx All-in-One (HP 86F3), documenting OpenCore configuration, AMD hardware support, diagnostics, testing, and release development.

## Project status

**Sequoia is the current experimental platform: `26.1.1-alpha.14`, UNSTABLE ALPHA.** No beta or stable release has been declared. This documentation-only branch uses the same Sequoia banner as the active research branch.

**Tahoe development has not started.** It will begin only after Sequoia reaches its first accepted beta or the Sequoia project is completed.

Start with the [Sequoia documentation](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/Sequoia), [version history](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/docs/VERSION_HISTORY.md), [latest evidence](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/docs/LATEST_EVIDENCE.md) and [beta acceptance criteria](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/docs/BETA_ACCEPTANCE.md).

## Separate package-manager development track

A [multi-architecture package manager](docs/PACKAGE_MANAGER.md) is now planned as a separate subproject: prioritize AMD/Intel x86_64 on Sequoia, then validate native Apple Silicon arm64 support. The proposed first prototype is a project-owned CLI over MacPorts, with an independent backend reserved for later evaluation.

This track is **PLANNED, not implemented or tested**. It has its own milestones and eventual versioning, does not change the Hackintosh alpha status and does not block the first Sequoia beta. `main` hosts its specification only.

## Branch structure

| Branch | Purpose |
| --- | --- |
| [`main`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/main) | Documentation only: project overview, hardware information, test history, compatibility status, and roadmap. |
| [`Sequoia`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/Sequoia) | macOS Sequoia development, configuration, scripts, and version-specific documentation. |
| [`Tahoe`](https://github.com/Vynzaro/HP86F3-Hackintosh/tree/Tahoe) | Future Tahoe research; development has not started and depends on Sequoia reaching an accepted beta or completion. |

`main` remains the default branch and contains documentation only. Implementation changes belong in the appropriate macOS branch; only documentation changes should be brought back into `main`.

Creating a branch or publishing a banner does not indicate a tested or stable release. Read the project's [legal notice](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/LEGAL.md) and [AI disclosure](https://github.com/Vynzaro/HP86F3-Hackintosh/blob/Sequoia/AI_DISCLOSURE.md).

The banner artwork and generation process are documented in [assets/README.md](assets/README.md).
