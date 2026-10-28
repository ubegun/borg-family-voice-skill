# borg-family-voice-skill

Borg agents family — humans communication skill: a local voice channel
between humans and their agents. Ear and mouth are local, the text in
between is the channel.

A skill for agent rigs: the operator speaks whenever they like, recognition
writes text to a local inbox, the agent reads it on any turn it chooses.
The microphone opens on the operator's command and never otherwise.

- **mailbox** — the default policy: asynchronous, non-blocking, durable
  plain-file inbox with a byte-offset read mark.
- **duplex** — a documented live-conversation policy (queued mouth, echo
  gate, barge-in), to be implemented before it ships.
- **scribe** — local-first transcription with an explicit read boundary.

Status: **architecture-first, pre-release**. This repository is private while
the public release is prepared. It currently documents the architecture and
evidence; it is not yet an installable skill. Public visibility follows the
sanitize, license, diagram, and implementation-readiness checks.

## Architecture

See [`canonical-voice-skill.md`](canonical-voice-skill.md) for the evidence-
weighted architecture, policy boundaries, privacy model, tuning baseline, and
conformance requirements.

See [`voices.md`](voices.md) for the offline mouth-engine survey, per-model
license constraints, and language coverage. Engine and model licenses are
independent of this repository's Apache-2.0 documentation license.

Licensed under the Apache License, Version 2.0.
