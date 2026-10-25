# Hardware and recorded software

Snapshot: 2026-10-24. Sources: S01–S03 and S09 in [SOURCES.md](SOURCES.md). Values are historical observations, not a current inventory collected during this documentation update.

## Physical target

| Component | Recorded hardware | Validation boundary |
| --- | --- | --- |
| Computer | HP All-in-One 22-dd0xxx | One individual machine tested |
| Motherboard / BIOS | HP 86F3 / F.50 | Another BIOS or board revision requires a new baseline |
| CPU | AMD Athlon Silver 3050U, 2 physical cores / 2 threads | Desktop boots; sustained CPU and power tests pending |
| GPU | AMD Raven2, PCI `1002:15D8` | macOS photo labels it AMD Radeon RX Picasso Graphics; do not infer a hardware replacement from that string |
| RAM | Approximately 15 GiB usable/system-reported | Reservation and reported totals vary; not a DIMM specification |
| NVMe | WD PC SN530, 256 GB | Contains Fedora and approximately 80 GiB Sequoia APFS allocation |
| SATA | Seagate HDD, 1 TB; AMD FCH controller `1022:7901` | Visible after AMDSata; no ext4 support or sustained-write claim |
| Display | Built-in HP panel, 1920×1080 observed | Brightness and wake behavior pending |
| Audio | Realtek ALC236 | Speakers reported working; microphone and jack pending |
| Wi-Fi | Realtek RTL8821CE, `10ec:c821` | Experimental stack worked in Recovery; desktop endurance pending |
| Bluetooth | Realtek USB `0bda:b00a` | Enumerated; working pairing not established |
| Ethernet | Realtek RTL8111/8168 family | No physical cable test available in recovered evidence |
| Camera | Chicony `04f2:b6c4` | Inventory detection only; macOS capture pending |
| USB | AMD XHCI; Genesys `05e3:0608` seen in topology | Keyboard/mouse connected directly; Genesys hub may be internal |

Do not distribute a universal EFI for other HP 86F3 machines. CPU variants, ACPI, BIOS, panel, network modules and port wiring must be compared before any compatibility claim. A similar marketing model name is insufficient.

## Software versions

| Component | Recorded version | Source / confidence |
| --- | --- | --- |
| macOS Sequoia | 15.8.1 | Saved reports; exact installed build needs a new `sw_vers` capture |
| Fedora Workstation | 44 | Preserved operating system in the project records |
| OpenCore | 1.0.8 DEBUG | Inventories and boot logs |
| Lilu | 1.7.2 | Latest photographed loaded-kext output, S06 |
| NootedRed | 0.8.10 | Latest photographed loaded-kext output, S06 |
| AppleALC | 1.9.8 | Latest photographed loaded-kext output, S06 |
| VirtualSMC | 1.3.8 | Historical inventory; not freshly audited |
| AMDSata | 0.9.2 | Historical inventory; not freshly audited |
| RealtekRTL8111 | 2.4.2 | Historical inventory; link operation not tested |
| RTL88WiFi and supporting Wi-Fi components | Exact installed revisions not recovered | Version/source/license audit required before reuse |
| AMD kernel patches | Exact active revision and count unverified | Historical counts vary; never construct the current config from an assumed count |
| SMBIOS model | iMac20,1 | Model designation only; unique identity fields remain private |

`alcid=55` appears in the tested audio configuration. Historical notes mention another layout property that may be stale or use the wrong HDA path; this is an investigation item, not an instruction to overwrite working audio settings.

The alpha.14 script changes NootedRed enablement/order only. It does not download replacement binaries or repair every subsystem. A script's presence does not prove that its dependencies, private state JSON or backup still exist.

## Evidence still required

Obtain a read-only inventory of the actual USB EFI, config hash, matching `ocvalidate` output, kext versions/hashes, ACPI hashes, kernel-patch revision, OS build and selected boot medium. Keep unique serials, account details, UUIDs and network identifiers out of public reports. Do not reconstruct missing private state JSON merely to make an old script accept a different baseline.
