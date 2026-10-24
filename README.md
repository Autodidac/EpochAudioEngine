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

Quick guide to [MPL-2.0](LICENSE); the full license governs. "Covered files"
means this library's MPL source, your changes to it, and new files containing
its code. Separate files in a larger application can use another license.

### Allowed

- [x] Use the library commercially, including in proprietary applications.
- [x] Sell applications or redistribute the library itself, changed or unchanged.
- [x] Make private/internal changes without publishing them or sending a PR.
- [x] License your separate application files under your own terms while meeting
  MPL obligations for the covered files.

### Required when distributing outside your organization

- [ ] Keep covered source, including your modifications, available under MPL-2.0.
- [ ] When shipping binaries, tell recipients how to obtain that covered source
  reasonably and promptly, charging no more than its distribution cost.
- [ ] Tell recipients the source is MPL-2.0 and include the license or explain
  how to obtain it.
- [ ] Preserve required copyright, patent, license and warranty/liability notices.
- [ ] Keep recipients' MPL source rights intact under any additional terms.

### Not allowed

- [ ] Do not make distributed covered source proprietary-only or withhold the
  covered source required for your binaries.
- [ ] Do not remove substantive required notices or present someone else's work
  as your own.
- [ ] Do not assume MPL grants rights to project names/logos or imply official
  endorsement. Use distinct product branding; see [TRADEMARKS.md](TRADEMARKS.md).

### Recommended, entirely optional

- [ ] Give visible credit and link to [this repository](https://github.com/Autodidac/EpochAudioEngine) and
  [EpochEngine](https://github.com/Autodidac/EpochEngine) in your About screen or README.
- [ ] Share useful fixes, features, tests and documentation through a
  [pull request](https://github.com/Autodidac/EpochAudioEngine/pulls); accepted contributions receive author credit.
- [ ] Follow [CONTRIBUTING.md](CONTRIBUTING.md) when choosing to contribute.

**MPL does not require an upstream pull request. But it would be a lot cooler if
you shared!** Contributions help these libraries support themselves and continued
work on EpochEngine. These recommendations add no copyright-license conditions.

See [Mozilla's MPL FAQ](https://www.mozilla.org/en-US/MPL/2.0/FAQ/) for examples.

## License

First-party source uses **MPL-2.0**; LICENSE contains the unmodified full text.
Private modification is allowed; distribution obligations apply to covered
files under that license. Commercial use is allowed. Required notices and
third-party licenses remain in force. Historical grants are not revoked.
See NOTICE for origin, TRADEMARKS.md for separate branding rules, and
CONTRIBUTING.md / CONTRIBUTOR_LICENSE.md for explicit contribution acceptance.
