# Terminal and system tools

Research date: 2026-10-25, America/Santiago. Baseline: **26.1.1-alpha.14 — UNSTABLE ALPHA**. State: **proposed minor patch; NOT_TESTED on the HP**.

The maintainer requested general-purpose tools comparable to the Fedora environment. This document defines a staged installation candidate for Sequoia. It does not establish a new physical test, assign another alpha number or certify application compatibility. Commands below are instructions for the physical macOS installation, not output from that machine.

## Recovered context and limits

Recovered conversation context references Git, Python, curl, jq, unzip and rsync in the HP's Fedora preparation workflow, alongside Linux hardware and boot tools such as pciutils, usbutils, dmidecode, alsa-utils, efibootmgr and acpica-tools. This is a secondary conversation record, not a complete package inventory or proof that every referenced package was installed.

The Zsh plugins, fzf, ripgrep, btop, tmux, ncdu, iTerm2 and LocalSend below are **new candidates**, not reconstructed facts about the previous HP installation. Tools discussed for another Fedora computer must not be silently attributed to this HP.

Historical Linux preparation scripts depend on Linux commands, device paths and sometimes missing private state. Do not execute them unchanged on macOS. These additions do not require editing OpenCore, SMBIOS, kext order or NVRAM.

### Native Siri investigation

The maintainer also requested native “Hey Siri” activation through system files or boot configuration, and scoped that work as a minor patch to the current alpha. No verified implementation has been found or tested on this HP. Changing a Siri preference is not evidence that native wake-word detection works. Dictation, custom voice commands and external wake-word applications do not satisfy the requested objective.

Next evidence remains the actual OS build, reported model, audio input endpoints, Siri preferences and relevant CoreSpeech logs. No such new terminal output has been received. Keep this investigation separate from the utility installation result and from the existing microphone issue, SEQ-005. No Siri preference writes or system-file patches are included here.

## Package manager choice

For this Sequoia x86_64 candidate, prefer **MacPorts**. Homebrew's current support policy classifies Intel macOS as Tier 3, has stopped new Intel bottle builds and points users of Sequoia and earlier toward MacPorts. Existing Homebrew installations may still work; inspect the existing environment before adding or migrating a manager. This recommendation is based on upstream policy reviewed on the research date, not on a successful installation test. [1]

This AMD Hackintosh uses the x86_64 software architecture; that does not make it an officially supported Intel Mac. Package availability and successful execution must be tested on the actual system. Prefer binary archives to avoid unexpected compilation workloads on the Athlon 3050U. A missing binary is a reason to stop and review that package, not to silently compile its entire dependency tree.

The separate [package-manager subproject](PACKAGE_MANAGER.md) plans a project-owned multi-architecture interface, initially using a MacPorts adapter. It is not implemented and is not included in this alpha.14 utility patch. The installation candidate below continues to use upstream MacPorts directly.

The current Homebrew macOS installer also rejects non-arm64 hosts. That restriction on new installations is distinct from the limited continued operation of existing Intel installations. See the [upstream installation script](https://github.com/Homebrew/install/blob/HEAD/install.sh), reviewed on 2026-10-25.

## Selected tools

| Group | Package / application | Purpose and scope |
| --- | --- | --- |
| Shell assistance | `zsh-autosuggestions`, `zsh-syntax-highlighting` | History-based suggestions and command highlighting; both need shell configuration. Highlighting is not a command safety guarantee. [4][5] |
| Search | `fzf`, `ripgrep` (`rg`) | Interactive selection and fast text search in project files and logs. [6][7] |
| Structured data | `jq` | Inspect JSON without manually searching long records. [8] |
| Resource monitoring | `btop` | Inspect CPU, memory, processes and I/O; do not assume AMD temperature or GPU sensors are available or accurate. [9] |
| Terminal sessions | `tmux` | Multiple panes and detachable sessions while the host keeps running; not persistence through a reboot. [10] |
| Disk usage | `ncdu` | Inspect directory sizes; use its read-only mode for initial checks. [11] |
| File transfer | `rsync` | Controlled file copying and comparison; not a complete APFS, EFI or system-restoration solution. [12] |
| Scripting, optional | `python313` | Explicit Python 3.13 interpreter with per-project virtual environments; no replacement of Apple's system files. [13] |
| Terminal UI, optional | iTerm2 | Alternative terminal interface; Apple's Terminal remains sufficient for the initial package set. [14] |
| Nearby file sharing, optional | LocalSend | Transfer files between macOS, Fedora and Samsung/Android over the local network. [15] |

Check existing Git, curl, SSH and unzip first. Apple's Command Line Tools provide a development baseline, including Git; duplicate installations are unnecessary unless an actual version requirement arises. GNU utilities can be evaluated separately when a script requires GNU-specific behavior. Do not globally replace macOS's BSD utilities or assume identical command-line options.

## Installation procedure

### 1. Inspect the current macOS environment

Run in Terminal on Sequoia:

```sh
sw_vers
uname -m
xcode-select -p
command -v port
command -v brew
command -v git
command -v python3
/bin/zsh --version
```

An absent command is diagnostic information, not a reason to modify boot settings. Record the actual OS/build and package-manager state. If Homebrew is already in use, inventory it before deciding on migration; avoid mixing libraries from multiple prefixes. Do not remove an existing package manager as part of this candidate.

### 2. Prepare MacPorts

If the Command Line Tools are absent, request them and wait for installation to finish:

```sh
xcode-select --install
```

Use Apple's tools compatible with the installed Sequoia version. Full Xcode is not generally necessary for this initial CLI set, although some ports require it. [2]

Download the **macOS 15 Sequoia package installer** linked from the [official MacPorts guide](https://guide.macports.org/chunked/installing.macports.html). Use its default `/opt/local` prefix. After installation, open a new terminal and run:

```sh
port version
sudo port selfupdate
```

The package installer configures the shell environment. If `port` is absent in a fresh terminal, consult the guide's shell setup section before manually changing PATH. [2]

### 3. Install in small groups

Preview the first group, then install it:

```sh
port -y install jq ripgrep fzf
sudo port -b install jq ripgrep fzf
```

After checking those commands, add shell assistance:

```sh
sudo port -b install zsh-autosuggestions zsh-syntax-highlighting
```

Add these optional groups individually when needed:

```sh
sudo port -b install btop tmux ncdu
sudo port -b install rsync
sudo port -b install python313
```

`-y` previews actions; `-b` requests binary archives and aborts when an archive is unavailable. The preview does not guarantee archive availability. An interrupted installation can leave already completed dependencies installed: record `port installed` and the error before retrying. Do not remove `-b` automatically. [3]

Python, if selected, can be invoked as `/opt/local/bin/python3.13`. Create a virtual environment inside the relevant project with `/opt/local/bin/python3.13 -m venv .venv`; do not use global `sudo pip` or replace `/usr/bin/python3`.

### 4. Activate Zsh additions

Back up the existing Zsh configuration before editing it. If `ZDOTDIR` is configured, use its actual `.zshrc` rather than assuming the file is in the home directory. Review existing plugins to avoid loading the same plugin twice. Retain the current login shell.

Inspect installed paths and any package-specific notes:

```sh
port contents zsh-autosuggestions
port contents zsh-syntax-highlighting
port notes zsh-autosuggestions
port notes zsh-syntax-highlighting
```

For the default MacPorts prefix, add this block to the existing interactive Zsh configuration. Confirm the two paths against the inventory above. Put syntax highlighting **after all other plugins and custom widgets**, at the end of the file. These guards prevent missing files from breaking shell startup; skipped guards do not count as successful activation. [4][5][6]

```zsh
# HP86F3 optional terminal additions.
if [[ -x /opt/local/bin/fzf ]]; then
    source <(/opt/local/bin/fzf --zsh)
fi

if [[ -r /opt/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh ]]; then
    source /opt/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh
fi

# Keep this after other widgets/plugins.
if [[ -r /opt/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ]]; then
    source /opt/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
fi
```

Open a new terminal and keep the original session available until the new shell starts cleanly. New fzf key bindings may replace existing shortcuts, so check Ctrl-R and Ctrl-T. Syntax highlighting must visibly work and suggestions must be tested against existing harmless history entries.

### 5. Optional applications

Obtain iTerm2 or LocalSend only through their official download pages. Select a release compatible with macOS 15 and **Intel/x86_64 or Universal**; an Apple-Silicon-only build will not run on this AMD computer. No application build has been validated on this HP. Install and test one at a time. [14][15]

For LocalSend, use the same trusted local network and allow the local-network permission if macOS requests it. Test an ordinary non-sensitive file and compare its SHA-256 at both endpoints. This can help transfer reports between the Samsung and Sequoia independently of the unresolved Bluetooth driver, provided network connectivity works. Fedora on the same dual-boot HP cannot be running simultaneously with Sequoia; a Fedora transfer requires another running device or a separate transfer step.

## Linux functions and macOS equivalents

These are functional alternatives, not compatible command aliases:

| Fedora task | Sequoia approach |
| --- | --- |
| Package installation with DNF | MacPorts `port`, using macOS packages rather than RPM files |
| PCI/USB/audio inspection | System Information, `system_profiler SPUSBDataType SPAudioDataType`, and targeted `ioreg` inspection |
| Process/resource inspection | Activity Monitor or the candidate `btop` |
| Disk inventory | Disk Utility and read-only `diskutil list`; do not translate Linux `/dev/sdX` device names mechanically |
| Service and log inspection | macOS `launchctl` and unified `log`; Linux systemd units and `journalctl` are not drop-in equivalents |
| Audio settings and routing | Sound settings, Audio MIDI Setup and CoreAudio; ALSA/PipeWire configuration is not portable directly |
| GNOME desktop extensions | Evaluate macOS-native applications per feature; GNOME extensions cannot simply be copied |

Firmware, filesystem, bootloader and driver tools from the Fedora preparation phase remain a separate workflow. The host-OS note in the README still applies.

## Acceptance and rollback

All candidate additions currently have result **NOT_TESTED**. Before marking an individual tool usable:

1. Record `sw_vers`, `uname -m`, `port version`, `port installed requested`, dependency inventory and the exact commands run. Sanitize user paths and any private content before publication.
2. Check versions with `jq --version`, `rg --version`, `fzf --version` and the corresponding optional tools. Test JSON parsing and text search against disposable non-sensitive files.
3. Verify new Terminal startup, suggestions, highlighting and fzf shortcuts. If tmux is selected, test detach and reattach before making it part of a workflow.
4. Compare idle responsiveness before/after, with the same applications open. Check that shell changes introduce no startup error. This is not a whole-system stability test.
5. For rsync, first inspect a `--dry-run` copy between disposable directories; then compare transferred file hashes. Avoid `--delete` in the initial exercise. For ncdu, use `ncdu -r -r` on a chosen directory to disable both deletion and shell spawning. [11]
6. Record the outcome using [TEST_RECORD.md](../templates/TEST_RECORD.md). Package success does not close Siri, Bluetooth, sleep or beta acceptance requirements.

To undo shell changes, remove only the added block or restore the saved configuration after reviewing any intervening edits. Open a fresh terminal to confirm recovery. Individual MacPorts packages can be deactivated with `sudo port deactivate NAME`; replace `NAME` with the actual package and respect dependency errors. Do not force removal or indiscriminately uninstall dependencies. [3]

No EFI/NVRAM rollback is part of this user-space procedure because no EFI/NVRAM change is proposed. The existing rescue-media and hardware-test rules remain in effect for any later boot experiment.

## Sources

Upstream documentation was reviewed on 2026-10-25. Package existence is not proof of available Sequoia x86_64 archives or successful execution on this HP. Third-party software remains governed by its own license; this repository includes instructions, not redistributed installers or binaries. See [LEGAL.md](../LEGAL.md), [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md) and [AI_DISCLOSURE.md](../AI_DISCLOSURE.md).

1. [Homebrew support tiers](https://docs.brew.sh/Support-Tiers).
2. [MacPorts installation guide](https://guide.macports.org/chunked/installing.macports.html) and [Command Line Tools requirements](https://guide.macports.org/chunked/installing.html).
3. [MacPorts port manual](https://man.macports.org/port.1.html).
4. [MacPorts zsh-autosuggestions](https://ports.macports.org/port/zsh-autosuggestions/) and [installation recipe](https://github.com/macports/macports-ports/blob/master/sysutils/zsh-autosuggestions/Portfile).
5. [MacPorts zsh-syntax-highlighting](https://ports.macports.org/port/zsh-syntax-highlighting/) and [upstream setup](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md).
6. [MacPorts fzf](https://ports.macports.org/port/fzf/) and [upstream shell integration](https://github.com/junegunn/fzf#setting-up-shell-integration).
7. [MacPorts ripgrep](https://ports.macports.org/port/ripgrep/).
8. [MacPorts jq](https://ports.macports.org/port/jq/).
9. [MacPorts btop](https://ports.macports.org/port/btop/).
10. [MacPorts tmux](https://ports.macports.org/port/tmux/).
11. [MacPorts ncdu](https://ports.macports.org/port/ncdu/) and [upstream manual](https://dev.yorhel.nl/ncdu/man).
12. [MacPorts rsync](https://ports.macports.org/port/rsync/).
13. [MacPorts Python 3.13](https://ports.macports.org/port/python313/).
14. [iTerm2 downloads](https://iterm2.com/downloads.html).
15. [LocalSend downloads](https://localsend.org/download).
