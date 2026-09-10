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

## Implementation update — 2026-09-08

The active cue renderer is now `apps/web/src/audio/procedural-cue.ts`, profile `air-wave-v1` (seed 73129, 48 kHz). It synthesizes original filtered noise with a phase-sized envelope; no source recording, tone, grain loop, or third-party sample is used. `scripts/export-procedural-cues.ts` reproduces the WAV masters and AAC/Opus delivery. Runtime generates exact-duration buffers with the same implementation; exported 8-second inhale/exhale files are preview/reference delivery, not looped runtime sources. Hold markers are 320/400 ms followed by silence. Rest has no cue.

Missing ambience delivery was rebuilt from the same seven owner-supplied MP3 files using `scripts/restore-runtime-audio.py`, with a −24 LUFS / −8 dBTP normalization target and short boundary fades. This processing does not establish commercial distribution rights. The older attribution-not-required statement above remains unverified until the owner's actual licence is retained; no new licence has been inferred from embedded metadata.

The missing safety-stop-if-unwell delivery was encoded from the existing SpeechKit MP3 master. No new speech synthesis was performed. The future `ru-female-calm-v1` voice directory is indexed separately; its rights depend on the eventual recording/provider agreement.

## Marina production voice — 2026-09-09

- Provider: ElevenLabs, user-selected library voice `ymDCYd8puC7gYjxIamPt` (Marina — Soft, Clear and Warm).
- Generated under the owner's Starter account. Distribution remains subject to the owner's ElevenLabs subscription/terms; no voice samples from Open or other applications were used.
- Original text: project-owned `content/guidance.ru-RU.json`, 152 phrases. Model/settings and generation records: `audio/production/manifest.json` (development documentation, not deployed).
- Delivery: `voice/ru-RU/ru-female-calm-v1/*.m4a`; AAC mono 96 kbps. Original API MP3 preserved outside public assets. Constant gain only; post-encode true peaks checked.
- The application uses local files. ElevenLabs credentials are never distributed with the application.

## Guided catalogue (September 2026)

Active files are exclusively under `audio/guided/`: 93 original Russian utterances generated through the user's authorized ElevenLabs account and three selected library voice IDs, four breath Foley assets derived from two project-commissioned ElevenLabs Sound Generation sources, and one project-authored harmonic ambience loop. No Open recording is used in these files. Voice-library/provider terms apply to the generated voice recordings.

Exact texts, models, settings, hashes, raw sources and processing provenance are retained in `audio/guided/production-manifest.json`, `voice-profiles.json`, `sound-manifest.json`, and `breath-source/manifest.json` at repository root. Calibration and source files are kept outside the deployed public audio directory. Listening acceptance and physical-device QA are documented separately in `docs/guided-implementation/IMPLEMENTATION_RU.md`.
