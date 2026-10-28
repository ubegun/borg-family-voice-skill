# Open local voices for the mouth of the `voice` skill

Candidate voices and engines for the mouth adapter (canonical §8).
Scope: engines that run fully offline on an Apple Silicon-class laptop,
with emphasis on Russian, Ukrainian, English, German, and Turkish.
Licenses are stated
for code and model weights separately wherever they differ — a voice
model and its engine can carry different terms. Facts verified against
primary sources (GitHub, PyPI, Hugging Face model cards) in October 2026.

No language is the center of this design. The surveyed set is what this
family speaks today; the mouth itself is language-symmetric — a voice
activates per language when its license-checked model file is present,
and any other language joins the same way, one file at a time.

## Piper — the default engine

Neural TTS (VITS in ONNX form), CPU-first, far faster than real time on
Apple Silicon. The original MIT-licensed repository is frozen at 1.2.0
and archived (August 2025); development continues as
**`OHF-Voice/piper1-gpl`** under **GPLv3** (the espeak-ng phonemizer is
embedded in the runtime). Current release v1.8.0 (September 2026) ships
native **macOS arm64 and x86_64 wheels** (`pip install piper-tts`) with
a streaming pipeline — the working route on macOS, verified first-hand.
The 2023 binary tarballs are not: the macOS asset ships debug symbol
bundles (`*.dSYM`) instead of the runtime libraries, and an x86_64
binary under an `aarch64` name. A "Piper 2" exists only as an
English-only prototype with an Apache-2.0 goal — unreleased.

Voices live on Hugging Face (`rhasspy/piper-voices`), one `.onnx` +
`.onnx.json` pair per voice; **each voice declares its own license in
its MODEL_CARD** — review before shipping. Download integrity is
checkable against the Hugging Face LFS hash; do that on first use.
The catalog spans several dozen languages; the sections below cover
the ones this document verifies, not the whole of it.

Russian — exactly four voices, `medium` quality, ~63 MB each, unchanged
since the 2023 set:

| Voice | License | Note |
|---|---|---|
| `ru_RU-dmitri-medium` | **CC0** | male; safe to ship |
| `ru_RU-denis-medium` | **CC0** | male; safe to ship |
| `ru_RU-irina-medium` | **"Unknown"** per model card | female; dataset traces to RHVoice — treat as unlicensed |
| `ru_RU-ruslan-medium` | **CC BY-NC-SA 4.0** | non-commercial — avoid in published artifacts |

Ukrainian — three new **high** voices (May 2026, Apache 2.0) are the
best offline Ukrainian option today: `uk_UA-tetiana-high`,
`uk_UA-mykyta-high`, `uk_UA-oleksa-high`. Legacy: 
`uk_UA-ukrainian_tts-medium` (CC0, three speakers) and
`uk_UA-lada-x_low` (16 kHz, Apache 2.0 dataset).

English — the largest catalog. Solid picks: `en_US-lessac-medium`,
`en_US-amy-medium`, `en_US-ryan-high`, `en_US-libritts-high`,
`en_GB-cori-medium/high`, `en_GB-alan-medium`.

German — `de_DE-thorsten` is the pick (dataset CC0), the rare voice
with a `high` tier alongside medium and low; `de_DE-mls` (medium,
dataset CC BY 4.0, 236 speakers) is the multi-speaker alternative.
Low-tier legacy voices — ramona, karlsson, kerstin, pavoque, eva_k —
derive from M-AILABS, whose dataset terms are non-commercial.

Turkish — exactly one Piper voice: `tr_TR-dfki-medium`, dataset
CC BY-NC-SA 4.0 (non-commercial). A permissive Turkish voice is a
known gap in this survey; on macOS the platform fallback is the system
voice Yelda.

Quality note: the medium tier is 22 kHz; the Russian voices are
English-warmstarted finetunes — usable, but clearly below Silero for
Russian.

## Silero TTS — best open Russian quality, license fork

Small and the fastest thing here (effectively instant on Apple
Silicon); Russian prosody with automatic stress and homographs.
Speakers: `aidar`, `baya`, `kseniya`, `xenia`, `eugene` (v5_ru line);
English via `v3_en` (118 speakers); Ukrainian via `v4_ua`.

The license is a fork in the road:

- wrapper code: MIT;
- most model weights: **CC BY-NC 4.0** — non-commercial;
- the exception: **`v5_cis_base` / `v5_cis_base_nostress` are MIT**,
  covering ~20 CIS languages including Russian and Ukrainian — at the
  cost of manual stress marking (no automatic stress or homograph
  disambiguation).

A permissively-licensed project therefore takes `v5_cis_base` (MIT) or
negotiates with the vendor; personal use can take the best-quality
`v5_ru` under NC terms.

## RHVoice

Long-maintained accessibility synthesizer; engine core **LGPL-2.1+**,
voice data licensed individually (community "Lab" voices are mostly
CC BY-NC-ND). Russian: Aleksandr, Anna, Elena (+ Lab voices); Ukrainian:
Volodymyr, Natalia, Anatol, Marianna; English: BDL, SLT, CLB, Alan, Ksp.
On Apple platforms an official app (macOS 13+) registers the voices
system-wide; the C++ core compiles for embedding. Dated but intelligible
sound, tiny footprint.

## eSpeak NG

GPLv3, ~127 languages, ru and uk improved in release 1.52.0 (December
2024). Robotic — the universal last-resort voice, never a preferred one.
Also the phonemizer inside Piper 1 (the reason that engine is GPLv3).

## Modern neural engines (2024–2026)

| Engine | Code / weights license | ru / uk / en | 16 GB Apple Silicon | Note |
|---|---|---|---|---|
| Kokoro-82M | Apache 2.0 / **Apache 2.0** | no / no / yes | excellent (INT8 ONNX) | best quality-per-MB English |
| Chatterbox (Resemble) | MIT / MIT | yes / no / yes | multilingual via MPS | outputs carry a neural watermark |
| Orpheus | Apache 2.0 / Apache 2.0 | no / no / yes | no (GPU-class) | natural English, emotion tags |
| Sesame CSM-1B | Apache 2.0 | en only | impractical | conversational model, not a product voice |
| Fish Speech / OpenAudio | Apache / **NC** | yes / no | no | open weights are non-commercial |
| F5-TTS | MIT / **CC BY-NC** | via NC community ckpts | CPU slow | NC applies even after fine-tuning |
| GPT-SoVITS | MIT / MIT | community fine-tunes | plausible on CPU/MPS | few-shot cloning suite |
| Bark | MIT / MIT | weak / no / yes | no | unmaintained since Aug 2024 |
| XTTS-v2 | **CPML — NC only** | yes / no | ~real time | Coqui defunct; no commercial path |

## Ukrainian- and Russian-specific projects

- **robinhad/ukrainian-tts** — MIT (since v5), CPU-fine VITS; voices
  lada, tetiana, mykyta, dmytro, oleksa.
- **egorsmkv/tts_uk** — MIT, RAD-TTS++ port, 44.1 kHz, multi-speaker.
- **HolosTTS** — MIT, created July 2026, openly work-in-progress; ONNX
  INT8 CPU build; the most promising modern Ukrainian-native model.
- **Vosk TTS** — **Apache 2.0, Russian-only** multi-speaker VITS
  (~783 MB) — a rare fully-permissive Russian option; basic quality.
- **facebook/mms-tts-{ukr,rus}** — 36 M-param VITS, but CC BY-NC 4.0.

## New in 2025–2026

- **May 2026** — three high-quality Ukrainian Piper voices, Apache 2.0
  (the event of the period for this niche).
- **Sep 2026** — piper1-gpl v1.8.0 (streaming, libpiper, native Apple
  Silicon wheels). No new Russian voices since 2023.
- **Nov 2025** — Silero CIS release: MIT-licensed `v5_cis_base` covering
  ru + uk (manual stress).
- **Jun 2026** — ZONOS2 (weights Apache 2.0, ru Tier 2 / uk Tier 3):
  first open MoE TTS, 8 B — not a laptop proposition.
- **Aug 2026** — FireRedTTS3 (Apache 2.0): **24 languages explicitly
  including Russian and Ukrainian**, zero-shot cloning and speech
  editing; ~11.4 GB of weights; a community port runs it on Apple
  Silicon at ~3× real time. Its README flags an upstream restriction of
  cloning to academic research — resolve before commercial use.

## Choosing

- **Pragmatic default**: Piper engine (accept GPLv3 for the runtime) +
  permissively-licensed voices — ru: `dmitri`/`denis` (CC0); uk:
  `tetiana-high`/`mykyta-high`/`oleksa-high` (Apache 2.0) or
  `ukrainian_tts-medium` (CC0); en: `lessac`/`amy`/`ryan`/`cori`; de:
  `thorsten` (CC0, with a high tier). Turkish has no permissive Piper
  voice — `dfki` is NC-only, so tr rides the platform voice or a
  separate hunt. Avoid `ruslan` (NC) and treat `irina` as unlicensed.
- **Quality-first Russian**: Silero `v5_ru` for personal/NC use;
  `v5_cis_base` (MIT) for a permissive project, with manual stress.
- **Fully-permissive stack** (no GPL, no NC): robinhad/ukrainian-tts +
  egorsmkv/tts_uk (MIT) + Vosk TTS (Apache 2.0, ru) + RHVoice engine
  (LGPL) + Kokoro (Apache 2.0, en) — at the cost of stitching several
  engines together.
- **LLM-grade**: only FireRedTTS3 verifiably covers ru+uk on 16 GB
  Apple Silicon, at seconds-per-sentence cost — a studio voice, not a
  channel voice.
- **Integration seam**: the mouth resolves language → model as a file
  convention — `voices/<lang>.onnx` present means the language speaks.
  Nothing central to maintain; a new language is one license-checked
  file drop.
- The platform voice (OS built-in speech) remains the zero-dependency
  fallback; everything above is an upgrade over it for offline, licensed
  speech in whatever languages the voices directory covers.