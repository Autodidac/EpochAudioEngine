# EpochAudioEngine

MPL-2.0 permits commercial use, including proprietary larger works subject to its covered-file obligations. See [Commercial use and giving back](#commercial-use-and-giving-back) for licensing, origin links and voluntary credit requests.

Version 0.1.0. Standalone C++23 audio scheduling and deterministic PCM mixing.

Canonical C++23 modules `audio.types`, `audio.manager`, `audio.mixer`,
`audio.device` and `audio.playback_runtime`. The library preserves bounded
command scheduling, deterministic PCM mixing and the existing abstract-device
playback lifecycle. Engine owns SDL integration, decoding/import and project glue.

Configure this directory with CMake 3.28+ and a C++23 module-capable compiler.
Build and run CTest in Debug and Release. Consumers link `Epoch::AudioEngine`.
The MSVC project is independently buildable and uses repository output layout
when present. CPU contracts prove the library boundary, not audible playback
or GUI presentation. Source licensing is preserved in LICENSE.

Build the library and offline demonstration:

```sh
cmake -S . -B out -DBUILD_TESTING=ON -DEPOCH_AUDIO_BUILD_EXAMPLES=ON
cmake --build out --config Release
ctest --test-dir out -C Release --output-on-failure
```

Run `out/Release/epoch_audio_demo example.wav` on a multi-configuration build,
or `out/epoch_audio_demo example.wav` on a single-configuration build. It uses
the real manager and mixer to write one second of stereo 440 Hz PCM audio.
Open the WAV in an ordinary audio player. Existing files are never overwritten.
This is offline rendering; it does not open a physical audio device.
The same executable accepts `--self-test` for a file-free synthesis check.

No other Epoch library is required. SDL device integration and Engine project
admission remain separate consumers. The optional EpochGui_Demo audio example
shows how a GUI application can use this library.


The source-only CI runs Debug/Release CPU contracts and verifies an actual
192044-byte stereo PCM16 48kHz WAV, including refusal to overwrite an existing
file. It uploads only test/source receipts, never WAVs or binaries. Reproduce
the file check with `python tests/audio.wav_contract.py <demo-executable> <local-proof-directory>`.

## Commercial use and giving back

A larger combined work may use its own license, including a proprietary commercial license, provided the covered files remain under MPL-2.0 and its applicable obligations are met.

Commercial use and standalone commercial redistribution are allowed by MPL-2.0;
you do not have to combine EpochAudioEngine with another product. When distributing
covered source modifications, make the covered modified files available under
MPL-2.0 and retain its required notices. Follow LICENSE for the precise source
availability and executable distribution obligations. Private edits do not
require publication, and MPL does not require an upstream pull request.

Please give visible, accurate credit in your application's About screen or its
README, linking to [the canonical EpochAudioEngine repository](https://github.com/Autodidac/EpochAudioEngine)
and [EpochEngine](https://github.com/Autodidac/EpochEngine), which this work
supports. Please offer generally useful changes as upstream pull requests with
clear author credit and provenance, following CONTRIBUTING.md. These are
community requests, not additional copyright-license conditions.
Accepted pull-request contributions retain author credit in GitHub history and in project acknowledgements where applicable.


Keep derivative product branding distinct and do not imply ownership of another
author's work or official endorsement. Factual origin, contributor credit and API
compatibility references are welcome; see TRADEMARKS.md.

## License

First-party source uses **MPL-2.0**; LICENSE contains the unmodified full text.
Private modification is allowed; distribution obligations apply to covered
files under that license. Commercial use is allowed. Required notices and
third-party licenses remain in force. Historical grants are not revoked.
See NOTICE for origin, TRADEMARKS.md for separate branding rules, and
CONTRIBUTING.md / CONTRIBUTOR_LICENSE.md for explicit contribution acceptance.
