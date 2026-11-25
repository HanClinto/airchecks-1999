# Handoff 01 — Scope and corpus selection

## Status
Pending (defaulted to year:1999 exact — user has not confirmed)

## Context
The repo indexes aircheck samples from the archive.org `airchecks` collection.
The 1999 scope is ambiguous — two readings are in play and both are indexed.
The canonical target decision needs to be made and documented.

## Known query counts (2026-11-25)
| Query | Count |
|---|---|
| `collection:airchecks AND year:1999` | 246 |
| `AND mediatype:audio` | 244 |
| `AND mediatype:video` | 0 |
| `collection:airchecks AND text:"1999"` | 374 |
| `AND mediatype:audio` (broad) | 346 |
| `AND title:1999` | 149 |

## Inputs
- `data/airchecks-1999-candidates.json` — the 244-item year:1999 audio set.
- `docs/PROJECT.md` — full framing and schema.

## Tasks
1. Confirm primary scope with the user (default: year:1999 exact, 244 items).
2. Decide whether to build the broad text:1999 set (~346 items) as secondary.
3. Emit the canonical scoped corpus as a tracked file (e.g. regenerate
   `data/airchecks-1999-candidates.json` with a `scope_bucket` field per item —
   `1999_exact` vs `1999_broad`).
4. Validate no duplicates, all identifiers resolvable via
   `https://archive.org/metadata/<identifier>`.

## Outputs
- `data/airchecks-1999-candidates.json` (or successor) — canonical,
  scope-tagged, validated.
- Confirmation recorded in this handoff (decision + date).

## Done when
- User decision recorded in this handoff.
- Every canonical item returns valid metadata from archive.org.

## Risks / notes
- The user's expected ~367-368 matches the broad reading, not the exact one.
  Resolve this explicitly rather than silently picking.
- The 244-item set is 100% audio, 0 video — don't waste time on video.
