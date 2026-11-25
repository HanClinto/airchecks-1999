# Handoff 05 — Wild Wild West targeted search

## Status
Not started

## Context
The flagship user target: Will Smith's "Wild Wild West" (May 1999), released to
early partner stations with call-letter overlays. Earlier search found NO
matching audio item in the year:1999 set. This needs a targeted search + a
decision on where to track it (new item, or known-absence).

## Inputs
- `docs/PROJECT.md` — the known finding (no match in 1999 audio).
- `data/airchecks-1999-candidates.json` — all 244 items, scanned for the title
  already; no match.

## Tasks
1. Broaden the search — query archive.org advancedsearch for:
   - `collection:airchecks AND text:"wild wild west"` (one hit: 1979 KNOE
     TV Channel Eight Report — audio, unrelated).
   - `collection:airchecks AND (title:"wild wild" OR ident:"wild*")`.
   - `collection:airchecks AND (text:"smith" AND text:"1999")` — find any
     May 1999 Smith item.
   - General search: `wild wild west` site:archive.org.
2. Decide:
   - Is there a 1999 sample not in the `collection:airchecks` set? (e.g. under
     `collection:RadioRecordings` or `collection:will-smith`).
   - Or is the artifact not on archive.org at all?
3. Record outcome here — findings + recommendation:
   - New candidate corpus entry (if found).
   - Or a "no_match" state for the target.

## Outputs
- This handoff updated with findings + decision.
- If found: new candidate file (`data/wild-wild-west-candidates.json`) and a
  row in the index.

## Done when
- The targeted search is run and the outcome is recorded.
- The decision on whether to keep this as a target is documented.

## Risks / notes
- Do not invent a match; the current finding is "not present in 1999 audio".
- This is a search task, not an annotation task.
