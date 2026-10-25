# Test roadmap and versioning

Planning snapshot: 2026-10-25, America/Santiago. **Current evidenced version: `26.1.1-alpha.14` — UNSTABLE ALPHA.** This plan adds no executed test, release or automatic schedule.

## Published baseline

The existing public [version history](VERSION_HISTORY.md) records executed alpha.14 and its evidence limits. That remains the current baseline; sustained stability is a separate pending campaign. This forward-looking plan adds no historical diagnostic data or new hardware result. Do not repeat the completed order change merely to allocate the next test.

## Preconditions before another mutation

Identify the active EFI and actual target media, validate the configuration with the matching OpenCore validator, and verify a private backup and working rescue path. Preserve the existing operating systems. If failure reports exist, correlate them with the configurations and human-observed outcomes privately. Reuse applicable baseline evidence and collect a new baseline if the installed state changes.

These are preparation and traceability requirements, not a newly completed alpha. Follow [TESTING.md](TESTING.md) and record physical experiments with [TEST_RECORD.md](../templates/TEST_RECORD.md).

## Proposed physical-test sequence

**Every row below is PLANNED / NOT_TESTED.** The version column is a provisional planning slot, not an allocated version or release promise. A failed or inconclusive physical experiment still consumes an actual alpha number; additional attempts can shift every later slot. Alpha.15 remains the next proposed slot unless the maintainer changes the immediate objective.

| Provisional version | Objective | Evidence needed to close the tested scope |
| --- | --- | --- |
| `26.1.1-alpha.15` | Bluetooth and its internal USB connection | Device/path/driver identification, then real pairing and profile operation; restart/wake reconnection when those dependencies can be tested |
| `26.1.1-alpha.16` | Physical USB map | External/internal port inventory, supported USB 2/3 speeds, hot-plug and peripheral recovery |
| `26.1.1-alpha.17` | Audio input/output and jack | Speaker playback, a listened-to recording of at least 60 seconds, jack switching if present, and post-wake checks |
| `26.1.1-alpha.18` | Native “Hey Siri” feasibility and controlled candidate | [SIRI.md](SIRI.md) stages SIRI-01–SIRI-05; first establish microphone and ordinary Siri operation, then distinguish capability checks from missing hardware functionality; no bypass is assumed |
| `26.1.1-alpha.19` | Camera | Real capture in two applications, permission behavior and reconnection/wake where applicable |
| `26.1.1-alpha.20` | Desktop Wi-Fi | At least 60 minutes of use, 10 reconnects, available 2.4/5 GHz networks and post-wake recovery |
| `26.1.1-alpha.21` | Ethernet | Physical cable link, DHCP/routing, sustained traffic and reconnection |
| `26.1.1-alpha.22` | Graphics and ordinary applications | 30 minutes of 1080p playback plus 30 minutes of GUI/graphics activity; record application versions and actual launch/use results |
| `26.1.1-alpha.23` | CPU, thermals and fan behavior | Recorded idle and sustained-load observations, responsiveness and comparison with valid hardware limits |
| `26.1.1-alpha.24` | Sleep, shutdown and wake | Five sleep/wake cycles and recovery of display, input, sound and networking; no unexplained panic/data loss |
| `26.1.1-alpha.25` | Boot, Fedora and recovery campaign | Five cold boots, five restarts, Fedora round trips, independent rescue boot, and demonstrated EFI restoration; validate autonomous boot if claimed |
| `26.1.1-alpha.26` | Storage and data restoration | Backed-up scratch-file copy/hash tests, supported health observations, and actual restoration of selected files |
| `26.1.1-alpha.27` | Apple services and security posture | Separate iCloud, App Store and Music/TV outcomes; document SIP/AMFI/FileVault state and limitations without automatically changing protections |
| `26.1.1-alpha.28` | Controlled update and rollback | Exact dependency/build comparison, proven recovery beforehand, and regression results after a selected update; defer if no justified candidate exists |
| `26.1.1-alpha.29+` | Integrated candidate and final regression | Implemented/tested verifier, all required gates addressed on the exact candidate, and at least 48 hours of recorded varied use |

The full sleep/restart campaign must revisit dependent Bluetooth, USB, audio, camera, Wi-Fi and Siri results. An early subsystem result with an untested dependency remains partial. Baseline backup and rescue checks happen before modifications, not only in the later full recovery campaign.

Siri retains the maintainer's **minor-patch scope based on alpha.14**. “Minor patch” describes the intended change size; it does not imply implementation or exempt a new physical experiment from chronological test numbering. SIRI-01–SIRI-05 are research-stage identifiers, not new alpha versions. If Siri requires further experiments, record them honestly and revise the later provisional slots.

## Release progression

| Milestone | Required transition | Current status |
| --- | --- | --- |
| `26.1.1-alpha.14` | Existing evidenced baseline | Executed; unstable |
| `26.1.1-alpha.N`, N ≥ 15 | Actual subsequent physical experiment with evidence, including failures/inconclusive results | Planned |
| `26.1.1-beta.1` | G0–G7 accepted, verifier implemented and tested, exact candidate recorded, human release approval | Blocked; all gates currently open |
| `26.1.1-beta.N`, N ≥ 2 | Evidence-backed beta fixes or scope expansion with relevant regression checks and renewed approval | Future, only if needed |
| `26.1.1-rc.1` | Proposed release-candidate stage: agreed scope frozen, no unresolved release-blocking defects, complete evidence for that candidate | Future; no tag or release exists |
| `26.1.1` | Human-approved stable release for an explicitly documented scope, with tested recovery and limitations | Future; not a compatibility guarantee |
| Tahoe alpha track | Begin only after Sequoia's first accepted beta or completion, as already agreed | Not developed; no Tahoe test number allocated |

The prefix `26.1.1` is the project's year/version/subversion scheme, not an Apple OS version. Documentation commits change the documentation history only. No dates are promised for these evidence-dependent milestones.

Beta and later releases must obey [BETA_ACCEPTANCE.md](BETA_ACCEPTANCE.md). P0/P1 defects cannot be waived into beta. Any P2 scope exclusion, including native Siri if unresolved, needs evidence, an explicit consequence, human acceptance and an accurate release description; it must never be reported as working. This plan does not pre-approve an exclusion.

## Related development tracks

| Track | Planned work | Relationship to physical versions |
| --- | --- | --- |
| Native Siri minor patch | SIRI-01–SIRI-05 in [SIRI.md](SIRI.md) | Initial provisional slot alpha.18 after microphone validation; no implementation yet |
| Terminal/system-tool minor patch | [SYSTEM_TOOLS.md](SYSTEM_TOOLS.md) package and shell validation | Separate controlled physical test when executed; may shift the numbered sequence |
| Guided installer | INS-01–INS-05 in [INSTALLER.md](INSTALLER.md) | Separate development milestones; mandatory acceptance if shipped/advertised in a release |
| Installation verifier | [INSTALLATION_VERIFICATION.md](INSTALLATION_VERIFICATION.md) | Mandatory before beta.1; develop and test during candidate preparation |
| Package manager | Separate milestones in [PACKAGE_MANAGER.md](PACKAGE_MANAGER.md) | Independent lifecycle; not an implemented alpha.14 patch or automatic first-beta gate |

## Updating this plan

After a real experiment, allocate its chronological alpha number, preserve its actual result and update [VERSION_HISTORY.md](VERSION_HISTORY.md), [KNOWN_ISSUES.md](KNOWN_ISSUES.md) and the relevant evidence record. Keep pending stages marked NOT_TESTED and adjust only future planning slots. Do not rewrite a failed attempt into a success or turn retrospective evidence review into a new hardware test.
