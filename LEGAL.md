# Legal notice, scope and limitation of liability

Last reviewed for this documentation snapshot: 2026-10-24. This notice describes repository scope and risk allocation; it is not legal advice, a legal opinion, an Apple authorization or a guarantee that an exclusion is enforceable in every jurisdiction. Obtain qualified local advice before relying on legal conclusions for distribution or commercial activity.

## Independent experimental project

This is an independent, non-official record of compatibility experiments on an HP computer. It is not affiliated with, sponsored by, endorsed by or supported by Apple, HP, AMD, OpenAI or the upstream driver/bootloader maintainers. Product names and trademarks identify systems and components; their ownership remains with the respective rights holders. No trademark license or certification is implied.

The project is intended for technical research and learning. Educational, personal, non-commercial or experimental intent does **not** itself create permission to use or redistribute software, override a contract, excuse infringement or establish a legal exception.

## Apple software restrictions

The [macOS Sequoia Software License Agreement](https://www.apple.com/legal/sla/docs/macOSSequoia.pdf), especially sections 2J–2N, restricts installation/use on non-Apple-branded computers and redistribution of Apple software, and addresses firmware, copying and reverse engineering. The HP in this project is not Apple-branded. Documented technical success does not establish licensed use.

The applicable agreement, any separately licensed components and applicable law control; this repository grants no Apple rights. A lawful download source does not by itself authorize installation on this HP. Any legal exception requires a specific assessment; none is asserted here. Read the agreement supplied with the software and the current [Apple license index](https://www.apple.com/legal/sla/) rather than relying only on this summary.

## Materials excluded from the repository

| Excluded material | Reason / boundary |
| --- | --- |
| Full or partial macOS installers, `InstallAssistant.pkg`, Apple installer apps and payloads | Proprietary content; no redistribution authorization is supplied by this project |
| Recovery/BaseSystem images, Apple DMG/ISO/IPSW images, preinstalled VM/system/APFS images and disk clones | These can embed Apple software, user data or both; not distributed here |
| Proprietary Apple frameworks, extracted kexts such as IOSkywalkFamily/IO80211FamilyLegacy, patched Apple binaries and cached OS packages | A historical reference to a component does not grant copying, modification or distribution rights |
| Apple/HP or other vendor firmware, ROM dumps, and unreviewed OEM ACPI dumps | Vendor ownership, possible private identifiers and unclear redistribution terms; original project-authored minimal source requires separate provenance review |
| Activation material, account credentials, tokens, certificates/private keys and private machine identities | Security/privacy risk; no service-access rights or bypass is provided |
| Complete personal EFI bundles and private `config.plist`/NVRAM/state/backups | May combine unique identifiers, private data and third-party material with distinct licenses |
| Unreviewed third-party binaries, kext bundles or source without applicable notices/rights assessment | Public availability is not a universal redistribution license |
| Unredacted full logs, screenshots and videos containing personal information | Protect identities, accounts and private system/network details; publish reviewed excerpts only |

These are project distribution exclusions; they do not assert that every listed item is always unlawful to possess or distribute under every possible license. Openly licensed components must be assessed under their actual version's terms. The repository may describe an excluded component without hosting it, mirroring it or endorsing unauthorized use.

## Allowed scope of repository contributions

Contributions should be original technical documentation, appropriately licensed project-authored source, minimal reviewed configuration examples, sanitized test evidence and links to authoritative upstream material. Before adding third-party content, verify the precise revision's license, attribution, source/distribution obligations and permission to modify or redistribute. Preserve all required notices. Do not use this notice to relicense upstream work.

No installers, cracks, activation bypasses, unauthorized credentials or methods to evade account limits are supplied. Do not present repeated identity changes as a remedy for service restrictions. The project does not promise iCloud, App Store, DRM, updates or other Apple services will work or remain available.

## No warranty

To the maximum extent permitted by applicable law, the project's materials are provided **as is and as available**, without express or implied warranties, including merchantability, fitness for a particular purpose, accuracy, completeness, non-infringement, compatibility, uninterrupted operation or security. Experimental status, documentation, a passing test or a future verifier does not create a warranty.

No obligation to provide support, updates, repairs, recovery, availability or continued compatibility is undertaken by this notice. Upstream authors and service providers have their own terms. Their work and support must not be represented as guaranteed by this project.

## Limitation of liability and user responsibility

To the maximum extent permitted by applicable law, the maintainer and contributors disclaim liability arising from use of or reliance on project materials, including device malfunction, boot failure, firmware/EFI/NVRAM changes, partition damage, data loss/corruption, downtime, security exposure, service/account restrictions, financial loss and consequential or incidental damages, regardless of the legal theory asserted.

This is an intended limitation, not a promise of complete immunity or a statement that reading this repository forms an enforceable contract. Nothing here excludes liability or mandatory rights that applicable law does not allow to be excluded, including any applicable non-waivable consumer protections or liability for conduct that cannot legally be disclaimed. Jurisdiction and facts can change the result.

Users remain responsible for assessing their rights to use software, understanding instructions, choosing correct devices, maintaining independent verified backups and accepting the operational risks of experiments. Do not use an unstable installation for critical work or irreplaceable data. An AI-assisted legal notice does not replace qualified legal review.

## Repository license status

This notice is **not a software or documentation license**. No new blanket license is granted by this documentation update. An earlier recovered prototype mentioned a license, but that does not automatically establish the licensing scope of the current repository, current contributions or third-party code. Before redistributing project-authored implementation, the maintainer must explicitly confirm an appropriate license and add its text and scope. Existing rights granted independently by a rights holder are unaffected.

## Rights and privacy concerns

Report a non-sensitive concern through the repository's available contact/issue mechanism with the affected path, claimed right and a concise description. Do not publish personal information or credentials as evidence. Sensitive reports should use a private channel verified with the maintainer; no unverified contact address is supplied here. The maintainer should assess substantiated concerns and correct or remove material where appropriate; no guaranteed response time is promised.
