
<!---
SPDX-FileCopyrightText: © 2018-2026 Alexandros Theodotou <alex@zrythm.org>
SPDX-License-Identifier: FSFAP
-->

# Zrythm GET PRO FOR FREE!

*a highly automated and intuitive digital audio workstation*

![screenshot](https://www.zrythm.org/static/images/screenshots/screenshot-20260729.png)

Zrythm is a digital audio workstation tailored for both professionals and beginners, offering an intuitive interface and robust functionality.

Key features include:

- Streamlined editing workflows
- Flexible tools for creative expression
- Limitless automation capabilities
- Powerful mixing features
- Chord assistance for musical composition
- Support for various plugin and file formats

Zrythm is [free software](https://www.gnu.org/philosophy/free-sw.html) written in C++23 using Qt/QML and JUCE.

## Features

- Clip looping and cloning
- Adaptive snapping
- Editing tools: pencil, eraser, cut, ramp and audition
- Multiple lanes per track
- Piano roll (MIDI editor) with velocity editor
- Chord pad, chord editor and chord suggestions
- Audio editor with adjustable gain/fades
- Musical mode with offline time-stretching
- Audio/MIDI recording with takes
- Wide variety of track types for every purpose
- Support for VST3, CLAP, LV2, LADSPA and AudioUnit plugins
- Type 0 and 1 MIDI file support
- WAV audio file import
- Built-in plugin browser
- Undoable user actions with undo history
- Hardware-accelerated UI
- SIMD-optimized DSP
- Cross-platform, cross-audio/MIDI backend and cross-architecture
- Available in multiple languages including Chinese, Japanese, Russian, Portuguese, French and German

<details>
<summary>Not yet ported from v1 (click to expand)</summary>

- Clip linking
- Bounce anything to audio or MIDI
- Piano roll chord integration and drum mode
- Audio editor part editing (including in external app)
- Event viewers (list editors) with editable object parameters
- Per-context object functions
- Punch in/out recording and record on MIDI input
- Device-bindable parameters for external control
- Signal manipulation with signal groups, aux sends and direct anywhere-to-anywhere connections
- In-context listening by dimming other tracks
- Automate anything using automation events or CV signal from modulator plugins and macro knobs
- Detachable views for multi-monitor setups
- Searchable preferences
- VST2, DSSI, SFZ/SF2 SoundFont support and other audio file formats
- Built-in file browser
- Optional plugin sandboxing (bridging)
- Stem export
- Automatic project backups
- Serializable undo history

</details>

For a full list of features, see the
[Features page](https://www.zrythm.org/en/features.html)
on our website.

## Download / Run a prebuilt build

A portable Linux **AppImage** for this `v2.0.0-alpha.3` snapshot is included in
this repository under `package-Debug/`.

**To run it (Linux, x86_64):**

```bash
chmod +x package-Debug/Zrythm-2.0.0-alpha.3-Linux.AppImage
./package-Debug/Zrythm-2.0.0-alpha.3-Linux.AppImage
```

If FUSE is unavailable, run in extracted form:

```bash
./package-Debug/Zrythm-2.0.0-alpha.3-Linux.AppImage --appimage-extract-and-run
```

The included AppImage is a **Debug build** produced from this source snapshot on
a x86_64 GNU/Linux system. It is self-contained and does not require a separate
Qt installation at runtime.

> **Note:** This is an alpha snapshot build created for testing and evaluation
> purposes. For official releases and prebuilt installers for all platforms, see
> <https://www.zrythm.org/en/download.html>.

## Building from source

Zrythm is written in C++23 with Qt6/QML and JUCE. The project uses:

- **CMake** as the build system
- **Conan** for most dependencies (Qt, fmt, spdlog, Boost, JUCE-related deps, etc.)
- **CPM** for a few remaining dependencies (CLAP, VST3 SDK, etc.)
- **Ninja** as the build tool

Full build instructions, including dependency setup, configuration, packaging
and CI notes, are in:

- [docs/github/GITHUB_INSTALL_INSTRUCTIONS.md](docs/github/GITHUB_INSTALL_INSTRUCTIONS.md)
  — quick-start for building, installing and packaging from this repository
- [docs/github/CI_BUILD_PACKAGE.md](docs/github/CI_BUILD_PACKAGE.md)
  — CI packaging pipeline overview
- [doc/dev/](doc/dev/) — developer documentation
- [AGENTS.md](AGENTS.md) — contributor / AI-agent build & test reference

In brief (Linux, with Conan available):

```bash
# 1. Install system deps (X11/Wayland dev libs, freetype, fontconfig, alsa, etc.)
#    and CMake + Ninja. See GITHUB_INSTALL_INSTRUCTIONS.md for details.

# 2. Configure dependencies with Conan
conan install . -pr:h gcc_debug -pr:b gcc_release --build=missing --lockfile=conan.lock

# 3. Configure the project
cmake -G Ninja -S . -B conanbuild/Debug \
  -DCMAKE_TOOLCHAIN_FILE=conanbuild/Debug/generators/conan_toolchain.cmake \
  -DCMAKE_BUILD_TYPE=Debug

# 4. Build
cmake --build conanbuild/Debug --parallel

# 5. (Optional) Package a Linux AppImage
./pack_appimage.sh

# 5b. (Optional) Run tests
ctest --test-dir conanbuild/Debug --output-on-failure
```

### Running from the build tree

```bash
source conanbuild/Debug/conanbuild.sh
./conanbuild/Debug/products/bin/zrythm
```

> **Important:** do not source `conanbuild.sh` / `conanrun.sh` in the same shell
> where you run `conan install` or other package-building commands.

### Packaging

`pack_appimage.sh` wraps the CPack AppImage packaging step used by CI:

```bash
./pack_appimage.sh
# Output: package-Debug/Zrythm-2.0.0-alpha.3-Linux.AppImage
```

Environment variables: `BUILD_TYPE`, `BUILD_DIR`, `PACKAGE_OUTPUT_DIR`.

See `docs/github/CI_BUILD_PACKAGE.md` for the CI packaging pipeline overview.

## Status

This repository contains a **snapshot** of the Zrythm source tree at
`v2.0.0-alpha.3`, together with a portable Linux AppImage built from that
snapshot for testing.

- **Upstream project:** <https://gitlab.zrythm.org/zrythm/zrythm>
- **This GitHub copy:** built, packaged and documented here for convenience

## License

Zrythm is free software. See [COPYING](COPYING) for copying conditions and
[TRADEMARKS.md](TRADEMARKS.md) for the trademark policy. License texts for
bundled third-party components are in [LICENSES/](LICENSES/).

Zrythm is licensed under the GNU Affero General Public License v3.0 or later
(AGPL-3.0-or-later), with a limitation on trademark use. Some bundled
dependencies use other open-source licenses; see [REUSE.toml](REUSE.toml) and
[LICENSES/](LICENSES/) for attribution and license texts.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Community

- Forum: <https://forum.zrythm.org>
- Matrix: `#zrythmdaw:matrix.org`
- IRC: `#zrythm` on Libera.Chat
- Discord: <https://discord.gg/ScHUMcNtPb>

## Support

If you would like to support this project, please consider donating at
<https://www.zrythm.org/en/download.html> or through the links on the website.

## Repository

- **Canonical upstream:** <https://gitlab.zrythm.org/zrythm/zrythm>
- **This mirror/snapshot:** <https://github.com/ahamedrashid-me/zrythm-2.0.0-alpha.3>
