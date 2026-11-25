# Handoff 06 — Annotation routine

## Status
Not started

## Context
Per-item annotation: download audio, transcribe, match songs/stations/
presenters, write the YAML schema. This is the main routine.

## Inputs
- Handoff 02 (transcription), handoff 03 (index), handoff 04 (triage).
- `docs/PROJECT.md` — annotation schema.

## Tasks
1. `tools/download.py` — download raw audio (mp3/ogg) from
   `https://archive.org/download/<identifier>/<filename>`, politeness delay
   (1 req / 2s), cache to `data/raw/<identifier>/` (gitignored).
2. `tools/transcribe.py` — run transcription on a download, output segments
   with timestamps. Use the handoff-02 backend.
3. `tools/annotate.py` — combine metadata + transcript + triage state, write:
   - `annotations/<identifier>.yaml` per schema.
   - Update the index row's `annotation_path` + `review_status`.
4. Validation:
   - YAML parses.
   - Songs (if any) are plausibly in the 1999 position (artist+title match
     against description text first, web search as fallback).
   - Callsigns in Whisper/description align with station field.

## Outputs
- `annotations/<identifier>.yaml` per approved item.
- Updated index.

## Done when
- One annotated YAML passes validation for each triaged-in sample.
- Re-running annotate.py is idempotent (skips approved, overwrites unreviewed).

## Risks / notes
- Transcribe only triaged samples.
- Don't invent fields — use null and note "unknown" where the evidence is
  not strong.
- Airchecks cover mostly music; song/artist matching is the hardest part —
  be honest about match confidence in the annotation.
