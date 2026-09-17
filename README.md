
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
https://drive.google.com/file/d/14rux94Y4-gpcYLvNUygZ2aziVwq8JJI0/view?usp=drive_link

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

Here's my comprehensive assessment of the plugin management system and other key features in this Zrythm codebase:

Plugin System Architecture Assessment
1. Plugin Managers — Properly Implemented
There are two distinct but complementary managers:

A. PluginManager (in src/gui/backend/) — GUI/QML-facing manager

Lives under namespace zrythm::gui::old_dsp::plugins
Responsible for scanning and keeping track of available plugins
Wraps JUCE's AudioPluginFormatManager and KnownPluginList
Exposes PluginDescriptorList for QML binding
Handles serialization/deserialization of known plugins to XML
Adds internal (Faust) plugins to the known list at startup
Prunes deleted plugin files during scan
References: src/gui/backend/plugin_manager.h, plugin_manager.cpp
B. PluginScanManager (in src/plugins/) — Headless scanner

Runs scanning in a separate worker thread via Qt's QThread + Worker pattern
Iterates through all registered plugin formats (CLAP, VST3, LV2, VST, AU, LADSPA, DSSI, SF2, SFZ, JSFX, Internal)
Uses out-of-process scanning for crash isolation (OutOfProcessPluginScanner)
Tracks currently-scanning plugin with mutex-protected state
Emits scanningFinished and currentlyScanningPluginChanged signals
Can be stopped gracefully via requestStop()
2. Supported Plugin Protocols — Comprehensive
The Plugin::ProtocolType enum covers 11 protocols:


Internal, LV2, DSSI, LADSPA, VST, VST3, AudioUnit, SFZ, SF2, CLAP, JSFX
Actual format implementations built into the binary:

CLAP: Custom CLAPPluginFormat + ClapPlugin host (implements ClapHostBase with full clap_host callbacks)
VST3: Custom Vst3PluginFormat (uses VST3 SDK directly for discovery) + Vst3Plugin host (implements IComponent/IAudioProcessor/IEditController)
VST2/LV2/AU/LADSPA/DSSI: Handled via JUCE's built-in AudioPluginFormat implementations (added via juce::addDefaultFormatsToManager())
Internal (Faust): FaustPlugin hosting bundled Faust DSPs compiled into Zrythm, with both FX (single dsp) and Instrument (PolyVoiceManager) modes
3. Plugin Host Implementations — Robust
Each plugin type has its own QObject-derived host class deriving from Plugin (which derives from ProcessorBase):

Plugin Type	Host Class	Key Features
CLAP	ClapPlugin	Full ClapHostBase implementation (audio ports, params, timer, log, latency, thread check, posix fd, thread pool, GUI). Uses clap::helpers::Host template with maximal checking
VST3	Vst3Plugin	Native VST3 hosting via SDK's IComponent. Handles bus arrangements, presets, MIDI CC mapping, parameter creation, program changes
JUCE-hosted (VST2/LV2/AU/etc)	JucePlugin	Wraps juce::AudioPluginInstance. Async initialization, parameter mapping, MIDI buffer management
Internal (Faust)	FaustPlugin	Bundled Faust DSPs. FX mode with direct compute, Instrument mode with PolyVoiceManager. Rebuildable param mapping
4. Plugin Factory & Object Model — Modern C++
PluginFactory uses the Builder pattern to construct plugin instances
Dispatches to appropriate builder based on ProtocolType (CLAP→ClapPlugin, VST3→Vst3Plugin, Internal→FaustPlugin, else→JucePlugin)
Uses utils::create_object<PluginT>() for typed object creation with registry
PluginUuidReference (typed UUID reference) for safe cross-references
Fully serializable via to_json/from_json with base64-encoded plugin state
5. PluginGroup — Flexible Container System
PluginGroup derives from QAbstractListModel for QML integration
Supports Serial (chain) and Parallel (sum) processing modes
Recursive nesting (groups can contain groups)
Type-safe: DeviceGroupType enum (Audio, MIDI, Instrument, CV)
Built-in fader for level control with mute/solo
Used in channels for MIDI FX, Instrument, and Audio FX processing
6. Plugin Host Window System — Cross-Platform
Two implementations:

QtPluginHostWindow: For X11/xcb, Win32, Cocoa — uses Qt Widgets top-level window with offscreen QML header
X11PluginHostWindow: For GNU/Linux Wayland sessions — raw X11 window with XEmbed support
Key features:

PluginViewResizeCoordinator handles resize coordination between host and plugin (CLAP adjust_size/set_size, VST3 checkSizeConstraint/onSize)
Header strip with preset popup (rendered offscreen via QML)
Scale factor tracking (contentScaleFactor) for HiDPI
Close requests hide rather than destroy (plugin owns editor window)
7. Plugin Discovery & Scanning — Safe
Out-of-process scanning via OutOfProcessPluginScanner (spawns subprocess to isolate crashes)
SubprocessCoordinator handles IPC with condition variable synchronization
Blacklisting of crashed plugins via JUCE's dead man's pedal mechanism
Known plugins serialized to XML for persistence
Skip-environment-variable support (ZRYTHM_SKIP_PLUGIN_SCAN)
8. Other Key Features Verification
DSP Graph System:

ProcessorBase → Plugin hierarchy with proper process_impl, prepare_plugin_for_processing, release_resources_impl overrides
[[clang::nonblocking]] annotation on real-time audio processing paths
Parameter sync with ParamSync and change_tracker() for efficient updates
** Faust Plugin System:**

Architecture file (faust_base.h) provides minimal dsp, UI, Meta, Soundfile base classes
Faust-generated code compiles standalone (no Faust headers needed at runtime)
FaustPluginInfo registry with create_ and class_init_ function pointers
PolyVoiceManager for polyphonic instruments with release-tail detection
Build System:

VST3 SDK via CPM (v3.8.0_build_66), CLAP via CPM (v1.2.7), clap-helpers (v0.3)
JUCE from custom fork (zrythm/JUCE, branch zrythm_fixes) with VST3 parameter-cache resync fix
LV2 hosting enabled (ZRYTHM_WITH_JUCE_LV2_HOSTING=ON on Unix)
Separate zrythm_vst3_hosting_lib static library for VST3 hosting glue code
Tests:

Extensive unit tests under tests/unit/plugins/: clap_plugin_test, faust_plugin_test, juce_plugin_test, vst3_plugin_test, plugin_factory_test, plugin_group_test, plugin_scan_manager_test, plugin_descriptor_test, etc.
Integration tests: plugin_integration_test, test_plugins_scan_test
CLAP test fixtures: test_gain_clap, test_configurable_clap, test_bad_ports_clap
VST3 test plugins: test_gain_vst3, test_synth_vst3, test_latency_vst3, test_midi_cc_vst3, test_param_groups_vst3, test_programs_vst3, test_restart_vst3, test_gui_vst3
9. Potential Concerns / Notes
find_plugin_from_uri / find_from_descriptor / pick_instrument are TODO stubs — These PluginManager methods are #if 0'd out and return nullptr. The real lookup happens through the PluginDescriptorList QML model. This could be an issue if code paths depend on them.

VST3 hosting is disabled in some build configurations — The compile commands show JUCE_PLUGINHOST_VST3=0 but the code has a full custom VST3 implementation via the VST3 SDK. This is expected since VST3 is hosted directly rather than through JUCE's VST3 plugin format.

No VST2 hosting in the custom code path — VST2 relies entirely on JUCE's built-in format. This is standard practice.

The "old_dsp" namespace for PluginManager suggests this is the older DSP GUI layer. The newer plugins namespace has the headless PluginScanManager. Both coexist.

Conclusion
The plugin management system is well-implemented and comprehensive, covering:

Multiple plugin format discovery (CLAP, VST3, LV2, VST2, AU, LADSPA, DSSI, SF2, SFZ, JSFX)
Out-of-process crash-safe scanning
Threaded scanning with progress reporting
Custom plugin hosts for CLAP and VST3 with full spec compliance
JUCE-based hosting for legacy formats
Bundled Faust plugin system with both FX and instrument support
Flexible PluginGroup container architecture
Cross-platform plugin window hosting (Qt/X11)
Full serialization and QML integration
Extensive test coverage
The architecture follows modern C++23 patterns with proper use of std::unique_ptr, std::span, concepts, ranges, pimpl, and [[clang::nonblocking]] for real-time safety.

## Repository

- **Canonical upstream:** <https://gitlab.zrythm.org/zrythm/zrythm>
- **This mirror/snapshot:** <https://github.com/ahamedrashid-me/zrythm-2.0.0-alpha.3>
