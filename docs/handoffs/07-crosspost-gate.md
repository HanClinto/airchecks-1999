# Handoff 07 — Crosspost gate

## Status
Not started (gated on review)

## Context
Approved annotations are crossposted as comments on their archive.org sample.
Archive.org has no public comment-write API for third parties.

## Hard constraints
- NEVER post comments via automation without explicit user authorization
  each session.
- Posting happens in the browser, by the user. Tooling may emit the
  markdown/comment text, nothing else.

## Inputs
- Approved annotations in `annotations/<identifier>.yaml` (review_status=approved).

## Tasks
1. `tools/crosspost_prepare.py` — for each approved annotation, emit:
   - The GitHub-tracked source (`annotations/<identifier>.yaml` + a
     copy-paste-ready markdown comment).
   - A list (`docs/crosspost-queue/<batch>.md`) of annotations queued for
     posting, with the exact comment text to paste.
2. Human review per-batch: reviewer eyeballs each annotation, confirms
   correctness (right station/song/artist/date).
3. Human posts in archive.org UI, one comment per sample.
4. After posting, mark the annotation `posted` in the index (tool reads
   a local `docs/crosspost-queue/<batch>.jsonl` of pasted comments).

## Outputs
- `docs/crosspost-queue/<batch>.md` — markdown comments ready to paste.
- `annotations/<identifier>.yaml` — gaining `quality.review_status=posted`
  after successful manual post.

## Done when
- Per-batch review has happened.
- Each queued comment is either posted manually or recorded as not-posted
  in the queue.

## Risks / notes
- Archive.org may rate-limit or require login in the browser — do not try
  to bypass via curl.
- Comment text should be short, factual, and link back to the repo (not
  include private endpoints).
