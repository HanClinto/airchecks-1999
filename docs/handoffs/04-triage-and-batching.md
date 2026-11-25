# Handoff 04 — Triage and batching

## Status
Not started

## Context
Transcribing 244 samples at ~30 min each is ~5 days of focused work. The triage
gate prevents waste: decide per-sample whether it's worth full annotation and
how much effort to apply.

## Inputs
- `data/index.db` (from handoff 03) or the candidate JSON directly.
- Transcription (handoff 02) output directories.

## Tasks
1. Per-item triage gate:
   - rich-description samples (WBBO-style song lists) → full transcription +
     match.
   - rich-finding samples (WSTB-style single songs) → light transcription.
   - bare-metadata samples ("ear", "WLTL", unscoped noise) → skip or minimal.
   - Will Smith / Wild Wild West target → dedicated search + tracking (see
     handoff 05).
2. Batch into groups (e.g. 10-20 per batch) by station/month, not alphabetical.
3. Record the triage decision as `review_status` + `notes` in the annotation
   YAML (or, in the index, `triaged-skip` / `queued` / etc.).

## Outputs
- Triage record per sample in the index.
- A triage report (markdown or table) — one row per item: title, station,
  batch assignment, decision.

## Done when
- Every 1999-scoped item has a triage decision recorded.
- Decisions are reversible (re-triage with a scripted overwrite).

## Risks / notes
- Don't burn time on bare-metadata items just to fill a count.
- Don't batch by callsign when callsign is missing — fall back to month.
