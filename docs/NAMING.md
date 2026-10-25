# Naming and version conventions

Use common English names with stable meaning. New names must be predictable across platforms and must not encode unproven success. Preserve original evidence privately; renaming a public derivative must not destroy its source mapping.

## File and directory names

| Type | Convention | Example |
| --- | --- | --- |
| Standard repository document | Common uppercase Markdown name | `README.md`, `CHANGELOG.md`, `LEGAL.md` |
| Topic document | Uppercase words separated by underscores | `docs/VERSION_HISTORY.md` |
| Directory | Lowercase, hyphen-separated if needed | `docs/evidence/`, `tests/fixtures/` |
| Executable project script | Lowercase snake_case and accurate extension | `scripts/verify_installation.sh` |
| Physical test report | `alpha-NN-topic.md` within `docs/tests/` | `docs/tests/alpha-14-graphics.md` |
| Candidate report before execution | `candidate-topic.md` | `docs/tests/candidate-bluetooth.md` |
| Evidence / log | Lowercase hyphenated topic and source date/time | `opencore-2026-10-23-201648-excerpt.txt` |
| Per-run generated report directory | Version plus ISO-style timestamp with explicit zone convention | `reports/26.1.1-beta.1/20261024T203000-0300/` (example only) |
| Verifier outputs inside one private run | Stable conventional filenames | `installation-verification.json`, `installation-verification.md` |
| Template | Uppercase descriptive Markdown name | `templates/TEST_RECORD.md` |

Examples of future paths do not mean those files or tests already exist. Do not create versioned test files for unexecuted hardware runs. New filenames use ASCII, no spaces, accents, parentheses, `(1)`, `final-final`, `new`, `fixed` or unexplained suffixes. Keep logical versions in report metadata and Git; use separate variant labels for genuine A/B comparisons.

Preserve required upstream runtime names such as `config.plist`, `OpenCore.efi` and kext bundle names when used privately or under a reviewed future distribution. Renaming them to match project aesthetics can break loading; this convention does not override the platform's filename requirements.

## Versions, results and dates

- Project version: `26.1.1-alpha.14`. `26.1.1` is the maintainer's year/version/subversion series, independent of macOS's version/build.
- Allocate an alpha number only after a physical experiment. A failed or inconclusive executed test still counts; preparation alone does not.
- Preserve historical 8A/8B identifiers in prose; use a `variant` field for future A/B records. Do not rewrite them as independent successful alphas.
- Documentation-only changes use commit history and CHANGELOG, not new alpha/beta labels.
- Use ISO 8601 dates and timestamps with offset/timezone when known. User-facing project dates use America/Santiago. Do not convert old firmware timestamps if their timezone was not recorded.
- Result values: `PASS` for the explicitly tested objective, `PARTIAL`, `FAIL`, `INCONCLUSIVE`, `NOT_TESTED`. Whole-project stability is a separate status.
- Issue IDs: `SEQ-001`, etc. Evidence IDs: `S01`, etc. Neither implies a test passed.

## Historical name mapping

The following source names are retained **only as provenance labels**. New public documents use the standardized names in this table. Source files are not silently rewritten, renamed in place or republished as validated tools.

| Historical source label | Current standard document / future role |
| --- | --- |
| `catalogo_versiones_inestables_hp86f3_2026-10-23.md` | `docs/VERSION_HISTORY.md` (updated English synthesis) |
| `HP86F3_26.1.1-alpha.13_reporte_arranque.md` | alpha.13 section in `docs/VERSION_HISTORY.md` |
| `HP86F3_Sequoia_Roadmap_Alpha_a_Beta_2026-10-24.md` | `docs/BETA_ACCEPTANCE.md` and `docs/TESTING.md` |
| `prueba13_gpu_ab_segura_hp86f3.py` | Historical GPU comparison source; any future port should be reviewed as `scripts/test_gpu.py` |
| `prueba14_nootedred_orden_h86f3.py` | Historical order experiment source; any future port should be reviewed as `scripts/test_kext_order.py` |
| `156554.jpg`, `156555.jpg` | Selected text observations in `docs/evidence/alpha-14-terminal-transcription.txt` |
| Numbered downloads such as `(1)` and `(2)` | Track original filename + SHA-256 privately; deduplicate by bytes, not suffix |

The proposed script names above reserve an understandable naming pattern; **no script migration or functional equivalence is claimed by this documentation update**. A future refactor must preserve/review CLI behavior, state paths, backup rules and safety checks, then test it before replacing a historical tool.
