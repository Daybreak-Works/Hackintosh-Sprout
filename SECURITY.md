# Security and privacy

The project is experimental and does not claim a supported or hardened configuration. Firmware, bootloader, kernel patches, third-party drivers and changes to OS protections can affect security. Document the actual state and each necessary exception; never describe an unmeasured state as secure.

## Do not publish

Keep serial numbers, MLB, SystemUUID, ROM, Apple Account details, tokens, passwords, private keys, network addresses/SSIDs, disk/display/USB serials, personal volume names and private paths out of commits and reports. Full EFI, NVRAM dumps, private manifests, backups and raw screenshots can contain these values even when a single visible field appears harmless.

Preserve private originals for troubleshooting. Create a separate sanitized excerpt and record what was removed. Review filenames, metadata and attachments too. Standard vendor/device IDs and public component versions can be useful; unique device/person/account identifiers require removal. Do not publish a hash of a secret as a substitute for redaction.

## Reporting problems

Use a public issue only for a sanitized technical report: tested version/build, issue ID, symptom, minimal evidence and reproduction steps. Do not attach a complete private EFI to prove an issue. For sensitive exposure, use a private channel verified with the maintainer. Do not assume GitHub private vulnerability reporting is enabled or publish secrets while trying to find a channel.

If a secret has been exposed, removing the latest file does not remove it from Git history. Revoke/rotate affected credentials where possible and assess history cleanup with the maintainer; preserve the minimum evidence needed without duplicating the secret. Do not force-push or delete unrelated history without an agreed recovery plan.

## Working protections

Keep the known-working rescue USB and verified backups. Inspect commands and device targets before running them. Do not automatically change SIP/FileVault, NVRAM, firmware, partitions or Fedora boot entries. Account-service restrictions are not a reason to bypass authentication or rotate machine identities. The [future verifier](docs/INSTALLATION_VERIFICATION.md) must be inspection-only apart from explicitly requested report output.

There is no guaranteed security-support period, response time or vulnerability-free release. See [LEGAL.md](LEGAL.md) for the project's scope and limitations.
