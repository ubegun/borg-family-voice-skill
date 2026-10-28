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

Status: assembling. The canonical document lands here first; content is
published only after a sanitize review.

## Architecture

See [`canonical-voice-skill.md`](canonical-voice-skill.md) for the evidence-
weighted architecture, policy boundaries, privacy model, tuning baseline, and
conformance requirements.

Licensed under the Apache License, Version 2.0.
