# Evidence provenance and source fingerprints

Snapshot: 2026-10-24. Sources below were recovered from the project's earlier work. Original bytes and private records remain outside this public repository. This index supports traceability; it does not make private material publicly downloadable or establish an exact machine backup.

## Evidence labels and precedence

- `DIRECT-LOG`: selected content from an original text log, with transformations/omissions stated.
- `PHOTO-TRANSCRIPTION`: human-readable fields transcribed from an original photograph; not original stdout.
- `USER-REPORTED`: the operator's observation preserved in a project report; not independently repeated by the assistant.
- `REPORT-SUMMARY`: a recovered written analysis; may combine evidence and interpretation.
- `HYPOTHESIS` and `PLANNED`: explanations or future actions, not results.

Prefer contemporaneous direct evidence for exactly what it shows. Use dated later reports to establish later state, while preserving earlier uncertainties. Source code proves intended behavior, not execution. Never resolve contradictory reports by silently fabricating missing output.

## Original source index

All SHA-256 values below cover the complete original bytes, including original line endings or log padding. They are content fingerprints, not current config hashes or signatures by an independent auditor.

| ID | Original source label | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| S01 | `catalogo_versiones_inestables_hp86f3_2026-10-23.md` | 19244 | `ebe98217472c5c6c3c0c2005f99a700e358d2e5a8622a142f4dbb0ae8c759d9c` |
| S02 | `HP86F3_26.1.1-alpha.13_reporte_arranque.md` | 6080 | `69869b00c992e759821988adb62c6c5b4193f64dc74251517203bfbed280431d` |
| S03 | `HP86F3_Sequoia_Roadmap_Alpha_a_Beta_2026-10-24.md` | 16095 | `2441b5ccf8f62d153e9a87b2c1371e0ba170a4755cad6f830060313ec29ca5ca` |
| S04 | `prueba14_nootedred_orden_h86f3.py` | 11478 | `25b2989a02ef010a0523e46bfb97d24011c749321648cf67a56b26992a7cdf3d` |
| S05 | `156554.jpg` | 298762 | `4cdca675dcd8a0fb0cc5e353ac70cc77f94a4d27e1ab1aee877ac832188b920e` |
| S06 | `156555.jpg` | 300108 | `b572dedf21b487856e4fa03d046bb72c30511979dbf81c50e97dcb442bbf75e5` |
| S07 | `opencore-2026-10-23-201648.txt` | 262144 | `a95b7c89b30d14fa608618922883c5f89eb9241998eea463351450926468caa2` |
| S08 | `opencore-2026-10-23-211242.txt` | 262144 | `f62c2b4e67b1d35cf5379650f9025b87b5fcdcfb1f0eaf1d48082d75dc61a3c0` |
| S09 | `26.1.1-alpha.7-inventario-v2-20261022-230609.md` | 19594 | `f4b38eacc344ac42524e41634d67bde81db587d148b7d0fc2b81fe5c12599aab` |
| S10 | `informe-acpi-hp86f3.md` | 2139 | `f149b4b7af454215187e358df44414591cc07d9ca8d129459f026f7eca8618df` |
| S11 | `informe-dsdt-hp86f3.md` | 2905 | `e61d25ac73d7a270287630f4a7df36748ca6cba35af0130b75e06359b31da7c0` |
| S12 | `informe-final-ssdt-hp86f3.md` | 4513 | `92214bf6243d26989eac44665e640e4de9845faccb9223499360a3cbf43a0738` |
| S13 | `HP86F3_CONTINUITY_2026-10-24.md` | 16185 | `d671098ef2f3f136f9c5e27074d6a3244573d35c1b62cc0b9cfc807bf2223955` |
| S14 | `prueba13_gpu_ab_segura_hp86f3.py` | 10423 | `a72f0b048c5f503ef7cdf957b0ac2c9287a4652a5b6b75ec1b2a2cbccab2921b` |

## Source scope

- **S01:** Historical catalogue, 2026-10-23. Ends at alpha.13-candidate; early attribution explicitly incomplete.
- **S02:** Contemporaneous alpha.13 boot report, 2026-10-24. Includes user declarations and the missing final apply-transcript caveat.
- **S03:** Latest recovered roadmap/status, 2026-10-24. Records alpha.14 success, remaining issues and beta gates.
- **S04:** Recovered alpha.14 script source. Shows enablement/order changes and baseline/backup checks; source alone is not execution proof.
- **S05:** Photographed terminal display capabilities and visible desktop wallpaper, associated with alpha.14 by S03. Original has a display serial; not republished.
- **S06:** Photographed loaded-kext output, associated with alpha.14 by S03. Original has private identity/display data; not republished.
- **S07:** Latest recovered standalone OpenCore log reaching EXITBS:START; original includes NUL padding. Exact variant attribution unavailable.
- **S08:** Latest recovered standalone OpenCore log by filename; ends early at console setup. Original includes NUL padding.
- **S09:** Historical hardware/software inventory. Does not substitute for the active alpha.14 EFI.
- **S10:** Recovered ACPI analysis report; supports preparatory work, not precise early-alpha execution attribution.
- **S11:** Recovered DSDT analysis report.
- **S12:** Recovered SSDT analysis report.
- **S13:** Recovery/continuation synthesis, 2026-10-24; secondary record describing recovery coverage and missing active files. Not a new hardware test.
- **S14:** Historical safer GPU A/B script source; not evidence that every proposed mode was executed.

## Public derivatives

| File | Derivation / omissions | SHA-256 of published bytes |
| --- | --- | --- |
| [alpha-14-terminal-transcription.txt](evidence/alpha-14-terminal-transcription.txt) | Selected photo fields; identifiers and unneeded rows omitted; normalized text. | `0d40f983fdfe6611ecc1e29058e9b3fa40592890033aff2e768fa82d24755167` |
| [opencore-2026-10-23-201648-excerpt.txt](evidence/opencore-2026-10-23-201648-excerpt.txt) | Final non-empty log line only; original NUL padding and earlier lines omitted; LF text with provenance header. | `23e58a786e195610b597842cb50624e31422afa86f25e75ae1c538c9917075a2` |
| [opencore-2026-10-23-211242-excerpt.txt](evidence/opencore-2026-10-23-211242-excerpt.txt) | Final non-empty log line only; original NUL padding and earlier lines omitted; LF text with provenance header. | `86b7ce1804a7a09211776d963aab31f1c3f335f52b05dd4b9008a5cfe017e6d5` |

Original screenshots are excluded because they expose unique/private information. Original reports are summarized in English, not republished wholesale with private paths. The file labels above retain historical spellings solely for traceability; new repository files follow [NAMING.md](NAMING.md).

## External primary references

- [Apple macOS Sequoia Software License Agreement](https://www.apple.com/legal/sla/docs/macOSSequoia.pdf), especially 2J–2N: legal limitations summarized in [LEGAL.md](../LEGAL.md). Checked 2026-10-24; the agreement supplied with the software and applicable law control.
- [Apple software license index](https://www.apple.com/legal/sla/): current official license entry point.
- [Apple: Create a bootable installer for macOS](https://support.apple.com/en-us/101578): full-installer USB capacity, distinct from this project's OpenCore/online-Recovery medium. Checked 2026-10-24; official Mac instructions do not validate an HP installation.
- Upstream component attribution and unresolved historical provenance are listed in [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md). References are not proof that a particular driver works on this machine.

## Recovery limits

The prior recovery located 161 original artifact records (including duplicate downloads): reports, scripts, logs, ACPI material, pictures, videos and historical repository scaffolding. This public update is a selected, sanitized documentation synthesis, not publication of that private recovery archive.

No complete active alpha.14 EFI/config/kext tree, private alpha.13/alpha.14 state JSON, actual HDD backup, APFS image or full literal earlier chat transcript was recovered. No independent new hardware run occurred during documentation. A missing source cannot be reconstructed merely by assigning a standardized filename or writing a plausible terminal transcript.
