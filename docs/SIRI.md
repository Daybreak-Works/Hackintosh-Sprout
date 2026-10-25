# Native Siri voice activation test plan

Planning date: 2026-10-25, America/Santiago. Published baseline: **26.1.1-alpha.14 — UNSTABLE ALPHA**. Tracking stages: **SIRI-01–SIRI-05**. Status: **PLANNED / NOT_TESTED**. No native wake-word patch, preference change, framework modification or boot-argument solution is implemented or validated by this document.

## Objective and scope

Investigate whether the installed Sequoia system can activate its native Siri assistant through its native “Hey Siri” / “Oye Siri” detector on the HP 86F3. Use the activation phrase actually supported by the selected Siri language. Dictation commands, Voice Control, keyboard shortcuts, external wake-word engines and remote assistants do not satisfy this test's native activation objective.

The maintainer requested this as a minor-patch investigation based on alpha.14. Its initial provisional slot is alpha.18 after microphone validation in [ROADMAP.md](ROADMAP.md). Planning does not allocate a new alpha; an actual physical experiment receives its chronological number under [NAMING.md](NAMING.md). Do not modify the established Lilu/NootedRed/AppleALC order to pursue this unrelated feature.

## Research question

The proposed investigation concerns native voice-trigger capability checks and their hardware dependencies. Treat `CoreSpeech`, `VoiceTrigger`, `corespeechd` and the `VoiceTriggerUserEnabled` preference as items to inspect, not as a proven bypass or evidence of current functionality. A reference in older headers must be checked against the installed build before it informs a candidate. This plan publishes no private conversation transcript, system inventory or diagnostic output.

Two independently sourced boundaries guide the investigation:

- Native “Hey Siri” is not exclusive to M-series Apple Silicon Macs: Apple's 2018 Intel MacBook Pro announcement describes the T2 bringing this feature to those machines. Apple's MacBook Air announcement also describes an always-on T2 processor supporting the feature. [1][2]
- OpenCore documents `BridgeOSHardwareModel` as model information propagated through EfiBoot and used by SoftwareUpdateCoreSupport. That documentation does not describe a T2 emulator or a Siri implementation; setting that value is not evidence that either exists. [3]

The hypothesis to investigate is whether an actual compatibility check can be satisfied or narrowly modified while retaining the native detector, or whether the installed path depends on missing hardware/firmware functionality. **Removing a check is not proof that the function behind it can run.** These alternatives remain unresolved on this HP.

## Test stages

Each stage starts NOT_TESTED. These are stage IDs, not release numbers. Preserve direct command results, visible behavior and interpretations separately using [TEST_RECORD.md](../templates/TEST_RECORD.md).

| Stage | Work | Completion evidence |
| --- | --- | --- |
| SIRI-01 | Establish input and ordinary Siri operation | Identify the selected input/language, listen to a ≥60 s microphone recording, check permissions, and establish that manually opened Siri understands and responds; this prerequisite is not native activation success |
| SIRI-02 | Read-only native detector diagnosis | Record relevant preferences, process/service availability and narrowly filtered CoreSpeech/VoiceTrigger logs around an attempted native setup/activation; record command failure or missing fields as unknown |
| SIRI-03 | Review actual capability path | Match relevant components to the exact installed OS/build and architecture; distinguish microphone/settings failure, capability rejection and unavailable hardware support; older headers alone are insufficient |
| SIRI-04 | Prepare and test a justified candidate, only if one is found | Identify exact changes, matching baseline hashes, validation, backup and restoration method before a separately reviewed physical attempt; if no implementable candidate is found, retain an inconclusive result instead of writing speculative settings |
| SIRI-05 | Validate native activation and regressions | Demonstrate the native wake phrase and response repeatedly without a substitute listener, then recheck restart/wake, audio, resource use and recovery on that candidate |

For SIRI-02, read-only inspection may include `defaults read com.apple.Siri VoiceTriggerUserEnabled`, audio endpoints and targeted logs for `corespeechd` / `VoiceTrigger`. These are proposed checks, not supplied results. Preference presence, a TRUE value, a loaded process or a visible settings toggle alone cannot establish native activation. Reuse applicable OS/build observations and collect the missing Siri-specific evidence privately.

## Proposed functional acceptance

These are project test targets, not Apple's certification criteria. Record the actual counts and conditions, including failures:

1. With ordinary Siri already working and the approved native configuration active, attempt the configured wake phrase 10 times in a quiet room and 10 times in a recorded normal-use noise condition. Record successful activations and responses separately; the proposed pass target is 10/10 in each condition.
2. Use the built-in microphone path under test. No Dictation, Voice Control, external listener, keyboard shortcut or manual click may initiate those measured wake attempts. Manual invocation is allowed only for the separate SIRI-01 prerequisite.
3. Record at least five minutes of ordinary speech without the trigger phrase and note unintended activation; the proposed target is none in that observation window. This is not a universal false-positive-rate claim.
4. Repeat native activation after a restart and after a validated sleep/wake cycle; if sleep itself is not yet validated, leave that portion NOT_TESTED and keep the overall result partial.
5. Compare idle CPU/resource behavior with the unchanged baseline over a stated interval, recheck recording/playback, and report crashes, new boot failures or regressions. Do not invent a hardware-independent CPU threshold.
6. If a change was applied, demonstrate restoration of the exact affected configuration/files through the documented recovery path. Report restored behavior separately from a successful file copy.

Use PASS only for the tested scope with supporting evidence. A shown setting or successful manual Siri interaction is not a native wake-word PASS. Use FAIL for an attempted objective that fails, INCONCLUSIVE when the mechanism cannot be established, and NOT_TESTED when no physical attempt occurred. Record untested language, lock-screen, distance or ambient-noise conditions as limitations rather than claiming universal behavior.

## Candidate and publication boundaries

Start with read-only diagnosis. This plan contains no writes to Siri preferences, EFI, NVRAM or system frameworks and authorizes no automatic changes to SIP, AMFI, FileVault or firmware. Any future system-file candidate must specify its exact build dependencies, signing/protection implications, validated recovery method and expected scope before application. Follow [TESTING.md](TESTING.md).

Keep voice recordings, transcripts, account information, full diagnostic output and private machine identities private. Publish only reviewed, non-sensitive observations. No Apple framework, patched proprietary binary, firmware or voice model is included. Follow [LEGAL.md](../LEGAL.md), [SECURITY.md](../SECURITY.md) and [AI_DISCLOSURE.md](../AI_DISCLOSURE.md); this research asserts no new redistribution rights or legal exception.

## Release relationship

Native activation remains unverified until a functional result is recorded. The microphone issue SEQ-005 in the existing public issue register is a prerequisite with its own closure evidence. Installing terminal tools or completing a graphics test does not establish either result.

If native activation remains unavailable, the feature must be documented honestly. Any proposed limited-scope beta exclusion follows the existing P2 evidence and explicit human acceptance process in [BETA_ACCEPTANCE.md](BETA_ACCEPTANCE.md); no exclusion is approved here. Do not advertise native “Hey Siri” until demonstrated.

## Sources

Reviewed on 2026-10-25. These primary sources establish platform context and the documented OpenCore variable; neither supplies a validated Sequoia/AMD wake-word bypass.

1. [Apple: 2018 MacBook Pro update, Intel processors and T2 / Hey Siri](https://www.apple.com/jo/newsroom/2018/07/apple-updates-macbook-pro-with-faster-performance-and-new-features-for-pros/).
2. [Apple: 2018 MacBook Air, T2 always-on processor and Hey Siri](https://www.apple.com/ma/newsroom/2018/10/all-new-macbook-air-takes-flight/).
3. [OpenCore reference source, BridgeOSHardwareModel](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.tex).
