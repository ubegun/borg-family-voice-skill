# Open local voices for the mouth of the `voice` skill

Candidate voices and engines for the mouth adapter (canonical §8). All
options below run offline on the machine that speaks; no audio or text
leaves it. Licenses matter as much as sound: a voice model and its
engine can carry different terms.

Status marks:

- **[verified]** checked first-hand;
- **[to verify]** license or support claim not yet re-checked;
- **[digest pending]** a wider survey is still running; the entry may grow.

## Piper — the pragmatic default

Neural TTS in ONNX form, fast on CPU, no GPU needed. Voices are hosted
in the `rhasspy/piper-voices` repository on Hugging Face; each voice is
a pair of `.onnx` + `.onnx.json`. **[verified]**

- Russian: `ru_RU-irina-medium` (female), `ru_RU-dmitri-medium` (male),
  `ru_RU-denys-medium` (male). **[verified]**
- Ukrainian: `uk_UA-ukrainian_tts-medium`, `uk_UA-lada-medium`. **[to verify]**
- English: `en_US-lessac-high`, `en_US-ryan-high`, `en_GB-alan-low`,
  `en_GB-northern_english_male-medium`. **[to verify]**
- Release binaries exist for Linux, macOS, Windows. The macOS binary is
  x86_64 and runs under Rosetta 2 on Apple Silicon; synthesis of a short
  line is near-instant. **[verified]** A native arm64 route also exists
  via the Python package. **[to verify]**
- Model file integrity is checkable against the Hugging Face LFS hash —
  recommended before first use. **[verified]**
- Engine code: MIT. Voice model licenses vary per voice and derive from
  their training datasets — read the voice card before shipping one.
  **[to verify per voice]**

## Silero TTS

Compact and fast, Russian/English/Ukrainian voices (female/male pairs),
widely used in Russian-language assistants. Code repository: MIT;
**the model weights have historically carried a non-commercial clause —
verify current terms before adopting. [to verify]**

## RHVoice

Classic formant/concatenative synthesizer, long maintained for Russian
and Ukrainian: multiple Russian voices, Ukrainian voices among them.
GPL. Quality is dated but intelligible; worth listing as the
lightweight fallback. macOS support: **[to verify]**

## eSpeak NG

GPLv3, covers ru/en/uk among dozens of languages. Robotic timbre — a
last-resort voice that is always available, never a preferred one.

## Coqui XTTS-v2

Multilingual neural TTS with voice cloning; supports Russian. License
CPML (non-commercial) — **a hard flag for any published artifact**; also
heavy for a 16 GB laptop. **[to verify]**

## Bark (Suno)

Expressive but slow on CPU; code MIT, **model weights license to
verify — historically non-commercial. [to verify]**

## Recent neural engines (2024–2026)

Kokoro, Chatterbox, Orpheus, Sesame CSM, Fish Speech, F5-TTS, GPT-SoVITS
— the survey is still compiling licenses and Russian/Ukrainian support
per engine. Most are English-first; several carry NC licenses or sizes
beyond a laptop. **[digest pending]**

## Recommendation

Piper is the default open mouth for ru+en(+uk) offline speech: small,
fast on CPU, per-language voices, verifiable downloads. A platform voice
(the OS built-in `say` route) stays as the zero-dependency fallback.
Everything else on this list is an alternative or an upgrade, not the
baseline.