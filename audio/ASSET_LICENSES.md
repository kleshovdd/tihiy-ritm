# Audio asset licenses and provenance

## User-provided ambience

The seven production tracks in `ambience/` were supplied by the application owner as MP3 files in `звуки окружения/`. Their embedded metadata identifies the artist/source as `Zvukogram.com`; the displayed Russian titles are read from the same metadata. Before release, the owner should retain the applicable purchase or distribution license for these files.

- Source files: user-provided MP3.
- Delivery processing: normalized to −24 LUFS and encoded as AAC/M4A and Opus/Ogg.
- Embedded credit: Zvukogram.com.
- Attribution: not required.
- Ambience target: −24 LUFS, encoded peak checked below −1 dBFS.

## Breathing masters and procedural auxiliary cues

The production inhale/exhale files `breath-*-master` are delivery encodes of `breathing-audio-prototypes/variant-b`. Revision 6 is project-owned original softened pitchless silk-flow synthesis created by `scripts/build-breathing-audio-prototypes.py`; it contains no samples from the five user reference recordings. The references informed only the desired softness and spectral balance. The synthesis has a smooth resonance-free spectrum, no musical pitch, no sample grains, and no LFO, tremolo, chorus, detune or close-frequency beating.

The auxiliary `cue-air-*` hold/transition files are original procedural assets generated locally by `scripts/generate-procedural-audio.ts`. They contain no third-party samples, speech, melodies or watermarks.

- Master target: seamless 8-second texture at 48 kHz; runtime gain and low-pass envelopes adapt it to each breathing phase without pitch-shifting.
- Auxiliary cue target: short one-shot onset signal, approximately 0.58–0.78 seconds, low-passed and checked below −6 dBFS.
- Verification: `pnpm audio:verify` checks existence, duration, peak and ambience loudness consistency. Human listening QA on supported phones remains required before public release.

The runtime uses one `soft-breathing-texture` cue theme. Older experimental `cue-glass-*`, `cue-natural-*` and unused `cue-air-*` files may remain in the workspace for comparison, but they are not referenced by the production manifest or UI.

## Placeholder voice

`voice/ru-RU/speechkit/` contains the owner's pregenerated Russian SpeechKit voice delivery. The normalized MP3 sources are kept in `assets/voice/ru-RU/speechkit/`; M4A and Ogg delivery copies are produced by `pnpm audio:import`.

No external CC, stock, streaming, YouTube, Spotify, BBC Sound Effects or unknown-license material is used by the application.
