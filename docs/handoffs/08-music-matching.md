# Handoff 08 — Music matching

## Status
Not started

## Context
Matching transcribed segments and description-text songs against a track/artist
database is the hardest part. No tool is built; this needs a small,
defensible approach.

## Inputs
- Transcript output (handoff 02) and annotation YAML schema (PROJECT.md).
- Description text (e.g. WBBO song list) — high-confidence track names.

## Tasks
1. Use description-text songs first (strongest evidence).
2. For Whisper-detected mentions, cross-check against:
   - a 1999 song reference (web search, or archive.org metadata),
   - a per-artist search (e.g. Will Smith, Mariah Carey, Madonna).
3. For unknown songs, leave title/artist null and note the confidence.
4. Validate match confidence: title+artist+year triple, with a source URL.

## Outputs
- Song list in the annotation with `title`, `artist`, `year`, `confidence`,
  `source_url` per song.

## Done when
- Every song-bearing annotation has a confidence + source URL, or is marked
  unknown.

## Risks / notes
- Do not fabricate song titles. Null + "unknown" is fine and expected.
- 1999-specific knowledge is heavy; rely on external sources over model memory.
