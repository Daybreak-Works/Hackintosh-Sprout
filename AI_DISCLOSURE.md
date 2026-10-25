# AI assistance and direct human supervision

## Why AI is used

This is an extremely complex experimental project spanning firmware, UEFI, ACPI, AMD kernel compatibility, graphics, network/audio drivers, installation, recovery and documentation. OpenAI ChatGPT/Codex is used solely as a technical assistance tool to help the human maintainer manage that complexity. It is not a replacement for human control, physical testing, upstream documentation or professional advice where needed.

## Work assisted by AI

AI assistance has included organizing recovered project records; comparing logs, scripts and photographed terminal output; identifying uncertainties; proposing hypotheses and reversible tests; drafting or revising diagnostic/configuration scripts; researching upstream references; preparing English documentation; and making repository changes under the maintainer's instructions. This documentation set was AI-assisted and prepared under the maintainer's explicit request.

Recovered historical scripts include AI-assisted experimental work and have not all been validated against the present machine state. A script being generated, syntax-checked or archived does not establish that it was safely executed, that it changed the intended EFI, or that its hardware hypothesis was correct.

The README banners were also generated and refined with OpenAI's built-in image generation tool under direct human direction. The maintainer reviewed alternatives, selected the Sequoia design, requested successive Tahoe refinements and explicitly approved both final images before publication. Artwork provenance, prompts and file fingerprints are recorded in [assets/README.md](assets/README.md). Visual approval does not certify hardware compatibility, originality or legal clearance.

## Direct supervision

The human maintainer directly supervises the project: defines goals and constraints, provides source material, operates and observes the physical HP, reviews proposed machine-affecting actions, supplies test results and decides release scope. Repository editing may be performed by the assistant within explicitly authorized work. No live hardware access to the HP is implied by a repository commit.

Direct supervision does not mean that every AI-produced sentence or line of code has already received an independent human audit. The final review and release acceptance must be recorded explicitly. AI may help prepare a report; only an actual observation and its evidence support a test result. The assistant must not claim to have heard speaker output, paired a device or completed a reboot that the human performed.

## Limits of AI output

AI can misunderstand hardware, produce incorrect commands, misread photographs, overlook licensing conditions, confuse historical and active states or suggest changes that cause boot failure or data loss. Confidence of wording is not evidence. A photo transcription can omit or misread text; a report summary cannot replace an unavailable original log. No claim is made that all AI-generated material is original, legally cleared or free of defects.

The assistant has not recovered the complete literal earlier conversation or the full active EFI/private state. Known gaps must remain visible. Generated examples, fixture output and planned tests must be labelled and never inserted as real terminal evidence.

## Required review method

1. Identify the actual baseline and preserve a verified backup/recovery path before any hardware-affecting proposal.
2. Separate observed symptoms, user declarations, hypotheses, proposed actions and measured outcomes.
3. Review paths, devices, configuration changes, component versions and upstream sources. Use dry-run/read-only inspection where practical.
4. Test narrowly, collect results and check regressions. Code syntax and `ocvalidate` checks do not replace physical validation.
5. Review privacy and redistribution before publishing logs, configuration or binaries. Do not send credentials or private identity fields to public issues or unnecessary services.
6. Require explicit human release acceptance. AI cannot certify Apple support, legal compliance, installation safety or universal compatibility.

## Attribution and accountability

Credit upstream authors for their work and preserve applicable notices. AI use does not transfer upstream rights to the project or remove the maintainer's review responsibilities. Keep a provenance trail for substantive changes through commits, test IDs and evidence references. Do not invent model versions, a percentage of AI authorship or an audit that was not performed.

See [LEGAL.md](LEGAL.md), [TESTING.md](docs/TESTING.md) and [SOURCES.md](docs/SOURCES.md) for the legal, validation and provenance boundaries.
