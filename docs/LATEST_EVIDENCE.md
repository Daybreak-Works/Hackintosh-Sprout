# Latest terminal and declared project record

Snapshot: 2026-10-24, America/Santiago. Latest evidenced test: **`26.1.1-alpha.14` — UNSTABLE ALPHA**. This is a reconstruction from recovered artifacts, not a new terminal session on the HP.

## What is latest, and by which measure?

| Evidence type | Latest relevant recovered record | What it supports |
| --- | --- | --- |
| Photographed installed-macOS terminal | S05/S06, associated with alpha.14 in the 2026-10-24 roadmap | Reported Metal 3 / 2 GB VRAM / 1920×1080 and loaded graphics/audio dependencies |
| Project status declared in recovered report | S03, dated 2026-10-24 | alpha.14 desktop/wallpaper result and outstanding hardware/service work |
| Standalone OpenCore text log, latest by filename timestamp | S08, `opencore-2026-10-23-211242.txt` | Ends early in console setup; it does not reach the kernel handoff |
| Latest recovered standalone text log that reaches `EXITBS:START` | S07, `opencore-2026-10-23-201648.txt` | Recorded boot handoff at `2026-10-23T20:18:05`; no proved panic |

Source photos have no capture timestamp verified here; their association with alpha.14 comes from the dated project record, not a guessed conversion of a filename. Firmware/log timezone is unknown. “Latest recovered” does not mean “latest file that exists on the user's physical computer.” No standalone alpha.14 terminal export or current complete EFI was recovered.

## Latest terminal photo: display capabilities

S05 visibly reports the following selected fields. This is a **partial manual transcription** of readable text, not original stdout, a complete screenshot or a fresh execution. Line indentation is normalized. Omitted fields include the display serial; no private field is replaced with a fabricated value.

```text
Chipset Model: AMD Radeon RX Picasso Graphics
VRAM (Total): 2 GB
Vendor: AMD (0x1002)
Device ID: 0x15d8
Metal Support: Metal 3
Resolution: 1920 x 1080 (1080p FHD - Full High Definition)
Main Display: Yes
Online: Yes
Connection Type: Internal
```

The photograph shows display-report-style output, but its command invocation is outside the visible region. Do not claim the command itself is visible. The GPU marketing string is the OS report; the physical inventory identifies Raven2. Neither string alone establishes a different chip or sustained acceleration performance.

## Latest terminal photo: loaded kexts

S06 visibly shows `kmutil showloaded` filtered for the relevant components. A line says `No variant specified, falling back to release`. The following **normalized field extraction** preserves only the readable bundle/version pairs; indices, addresses, dependency lists and UUIDs are omitted, and this is not a byte-for-byte terminal dump:

```text
as.vit9696.Lilu (1.7.2)
org.ChefKiss.NootedRed (0.8.10)
as.vit9696.AppleALC (1.9.8)
```

The fallback message belongs to that command's output; it does not establish that the USB bootloader changed from OpenCore DEBUG to RELEASE. Loading proves presence, not hardware functionality or universal correctness of kext order. The same image and S03 support that the wallpaper was functioning after the experiment.

A compact combined transcription is available in [alpha-14-terminal-transcription.txt](evidence/alpha-14-terminal-transcription.txt). Original photographs are not published because they contain unique/private information. See [SOURCES.md](SOURCES.md) for fingerprints.

## Latest original boot-log endpoints

S08, chronologically latest by its recorded filename, ends:

```text
05:428 00:077 OCC: Setup ASCII Output - Success
```

S07, the latest recovered file to reach the later handoff, ends:

```text
77:017 00:064 AAPL: #[EB|LOG:EXITBS:START] 2026-10-23T20:18:05
```

Both originals contain fixed-size NUL padding. Public excerpts omit padding and select only non-sensitive ending lines; the original bytes remain unchanged privately. See [S08 excerpt](evidence/opencore-2026-10-23-211242-excerpt.txt) and [S07 excerpt](evidence/opencore-2026-10-23-201648-excerpt.txt). These records precede the alpha.14 desktop evidence. They must not be presented as logs of that successful run or used to overwrite the later observed status.

## Human declarations preserved in reports

The following are English paraphrases of recorded statements, not invented direct quotations or terminal output:

- S02: the user reached Setup Assistant and the desktop, reported good speaker output, then reported slow graphics and a white wallpaper during alpha.13.
- S02: microphone performance was uncertain, without a structured recording test. A new Apple Account creation attempt hit an account-creation limit; a local user account already existed.
- S03: after re-enabling/reordering NootedRed for alpha.14, desktop/wallpaper worked and 2 GB VRAM / Metal 3 were announced. S05/S06 provide selected direct visual support.
- S03: Bluetooth was not operational, Apple Account/App Store had unresolved errors, and internal autonomous boot had not been validated. Wi-Fi success remained primarily Recovery evidence.
- S03: no completed sustained stability, sleep, storage recovery or whole-system regression campaign was recorded.

## Attribution conflicts and missing evidence

S01 stopped at alpha.13-candidate and is outdated for the latest state. S02 initially lacked the alpha.13 final apply transcript; S03 later records the disabled-NootedRed sequence. This resolves the later narrative without reconstructing a missing original output. S04's source proves what the script is designed to change, not by itself that it was run successfully.

Still needed: live config/EFI hashes, the original private alpha.13/alpha.14 state and backups, current OS build output, successful-run boot logs, sustained functional tests and independently demonstrated restoration. Before another mutation, audit those on the real media. The recoverable historical record is substantial but not an exact machine backup.
