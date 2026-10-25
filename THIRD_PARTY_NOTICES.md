# Third-party references and redistribution review

This documentation update does not bundle upstream code or binaries. Mentioned software remains the work of its respective authors. Recorded component versions appear in [HARDWARE.md](docs/HARDWARE.md); references below do not imply the current upstream release matches the historical installation.

| Component / project | Upstream reference | Project use / status |
| --- | --- | --- |
| OpenCorePkg / ocvalidate | [acidanthera/OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) | Bootloader and matching configuration validator referenced historically |
| Lilu | [acidanthera/Lilu](https://github.com/acidanthera/Lilu) | Plugin framework observed loaded |
| VirtualSMC | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) | Historical dependency |
| AppleALC | [acidanthera/AppleALC](https://github.com/acidanthera/AppleALC) | Historical audio experiments / loaded driver |
| NootedRed | [ChefKissInc/NootedRed](https://github.com/ChefKissInc/NootedRed) | Experimental AMD graphics dependency |
| AMD kernel patches | [AMD-OSX/AMD_Vanilla](https://github.com/AMD-OSX/AMD_Vanilla) | Historical AMD patch source reference; active revision unverified |
| SSDTTime | [corpnewt/SSDTTime](https://github.com/corpnewt/SSDTTime) | Historical board-specific ACPI preparation reference |
| Bluetooth firmware project | [thegwchr/RealtekBluetoothFirmware](https://github.com/thegwchr/RealtekBluetoothFirmware) | Investigation reference only; no working installation established |
| BlueToolFixup / BrcmPatchRAM | [acidanthera/BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM) | Investigation reference only; not a proven Realtek solution here |
| RTL88WiFi, AMDSata, RealtekRTL8111 and supporting components | Exact acquired source/revision must be re-established | Names in reports are not sufficient provenance or redistribution permission |
| macOS and proprietary Apple Wi-Fi components | [Apple software licenses](https://www.apple.com/legal/sla/) | Not bundled; restrictions discussed in [LEGAL.md](LEGAL.md) |

No license identifier is assigned from memory to an unverified historical binary. In particular, do not assume that a current upstream license is identical to the terms of the recorded old version or that all “kexts” share one license.

Before adding a dependency, record its upstream URL, immutable revision/tag, original filename, SHA-256, license text/source, copyright notices, modification status and redistribution requirements. Resolve missing provenance before publication. Prefer reference links over mirroring binaries. A source being visible on GitHub does not by itself make every use or redistribution permissible.

Original project-written ACPI/source must be distinguished from OEM tables and third-party generated snippets. Keep applicable attribution and review the minimum necessary publication. Do not copy macOS UI assets, proprietary code or installers into this repository or the separate future Linux project.
