# Contributing

Use English for repository files and common, predictable filenames. Discussion with the maintainer may be in Spanish. Keep `main` documentation-only; implementation belongs in `Sequoia` or `Tahoe` according to its actual target. Do not merge all of an OS branch into `main` merely to update documentation.

## Evidence-based changes

Before changing a claimed result, read the version record and linked evidence. Distinguish direct log, photo transcription, user report, report summary, hypothesis and plan. Preserve negative results and explicitly dated corrections. Never invent an error string, execution transcript, test pass, missing configuration or machine identity.

Use [TEST_RECORD.md](templates/TEST_RECORD.md) for physical experiments and [NAMING.md](docs/NAMING.md) for new filenames. Include the exact baseline, hypothesis, changed keys/files, validation, observed output, human result and rollback. Update the version history and known issues together. A new documentation commit does not create an alpha; a branch does not create a tested release.

## Review before publication

- Confirm scope and source provenance, then sanitize identifiers and personal data.
- Check relative document links, filenames, version/status consistency and evidence quotations.
- Test code according to its effects. A future installer/verifier needs failure cases and real-machine validation; a prose correction does not need a fake hardware test.
- Review upstream rights and notices; exclude the materials listed in [LEGAL.md](LEGAL.md).
- Disclose material AI assistance under [AI_DISCLOSURE.md](AI_DISCLOSURE.md). Human direction and validation remain necessary.
- Do not claim beta until [BETA_ACCEPTANCE.md](docs/BETA_ACCEPTANCE.md), including the implemented verifier, is satisfied on the exact candidate.

No repository-wide contribution license is selected by this update. Identify authorship and rights for proposed implementation; the maintainer must settle licensing scope before redistribution. Contributions must not rely on an AI disclaimer to avoid source, safety or rights review.
