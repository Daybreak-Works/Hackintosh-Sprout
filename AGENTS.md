# Repository working instructions

## Project state and language

- Repository text is English; conversation with the maintainer is normally Spanish.
- Read README.md, docs/LATEST_EVIDENCE.md and docs/KNOWN_ISSUES.md before changing status or proposing machine changes.
- The documented baseline is 26.1.1-alpha.14, UNSTABLE ALPHA, until newer evidence is added. No alpha.15 or beta has been executed by writing documentation.
- Preserve exact branch names: main, Sequoia, Tahoe. main accepts documentation only. Implementation belongs in the relevant OS branch.

## Evidence and naming

- Follow docs/NAMING.md and use templates/TEST_RECORD.md for physical tests.
- Keep direct output, photo transcription, human report, interpretation and planned work distinct. Never fabricate missing output, hashes, config/state files or test results.
- Do not relabel a preparatory script, fixture, syntax check or repository commit as a successful hardware test.
- Preserve historical originals privately; publish standardized, sanitized derivatives with provenance.

## Hardware and release work

- Identify and back up the actual current EFI before mutations; preserve Fedora and the rescue USB. Historical scripts may require missing private state and must not have their checks bypassed.
- Keep changes narrow and reversible, with validation and evidence. No unplanned disk erase, firmware write, global NVRAM reset or identity rotation.
- For beta.1 preparation, implement and validate scripts/verify_installation.sh according to docs/INSTALLATION_VERIFICATION.md. Its absence blocks beta promotion.
- Complete G0–G7 in docs/BETA_ACCEPTANCE.md on the exact release candidate and record human acceptance before declaring beta.
- Preserve README's USB distinction: minimum 5 GB usable for the OpenCore/online-Recovery profile, 8 GB or larger recommended/tested historical device; full installer profile 32 GB or larger with actual payload fit.

## Publication

- Follow LEGAL.md, SECURITY.md and AI_DISCLOSURE.md. Do not commit proprietary Apple files, unreviewed third-party binaries, private EFI/config/state, identities or credentials.
- Review source rights; do not infer the current project's license from an old prototype.
- Check links, text excerpts, source fingerprints and version/status consistency. Report exactly what was tested and what remains unknown.
