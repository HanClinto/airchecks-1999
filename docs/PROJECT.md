# Airchecks 1999 — annotated catalog

## Goal

Build high-quality annotations of raw aircheck samples on archive.org,
starting with the ~367-368 items in the `airchecks` collection dated/tagged
with the year 1999, and extensible to any arbitrary aircheck sample in the
collection (all years).

Aircheck = a recording of a radio station airing (not studio master). These are
rare, unlicensed-by-intent bootleg artifacts — collectors and archivists use
them to verify exactly what a station played, when, and often who was live on
the air. They are valuable for:

- rare/specialized content: exclusive songs (e.g. Will Smith's "Wild Wild West"
  released May 1999 to early partner stations with call-letter overlays to
  prevent other stations pirate-recording and rebroadcasting as their own)
- personalities, contests, commercials, events
- provenance: what a station played on a date, with DJ/presenter attribution

## Deliverables

1. `annotations/` — one YAML/JSON file per sample, structured for collectors.
2. `data/` — machine-readable index of all candidates (all airchecks, with
   filtering to 1999).
3. `docs/` — this file plus schema, methodology, and operating notes.
4. Crossposting: reviewed annotations go up as comments on each archive.org
   sample (requires human review + archive.org login — see "Review gate").

## The 1999 scope

Archive.org query (`collection:airchecks` + year) and result counts as of
2026-11-25:

| Query                                                     | Count |
|-----------------------------------------------------------|-------|
| `collection:airchecks AND year:1999`                      | 246   |
| `collection:airchecks AND year:1999 AND mediatype:audio`  | 244   |
| `collection:airchecks AND year:1999 AND mediatype:video`  | 0     |
| `collection:airchecks AND text:"1999"`                   | 374   |
| `collection:airchecks AND text:"1999" AND mediatype:audio`| 346   |
| `collection:airchecks AND title:1999`                    | 149   |

The user's expected figure (~367-368) corresponds to the text/title search
broader than the `year:` filter. We treat the scope as: **any aircheck sample
whose title/identifier/description/subject mentions 1999 (the broad ~367-368
set), prioritized with a year:1999-exact set**. We will keep both in the index
with a `scope_bucket` field so the broad set stays queryable.

## Candidate corpus (1999-exact, `year:1999 AND mediatype:audio`)

244 items, all audio, all dated 1999. Distribution by month:
Jan 39, Feb 13, Mar 15, Apr 18, May 20, Jun 13, Jul 16, Aug 29, Sep 14,
Oct 26, Nov 17, Dec 24.

Representative entries found (full 244-item list in
`data/airchecks-1999-candidates.json`):

- WSTB (Akron) Innocent Age with Chuck Benjamin, 5-2-99, Buddy Holly
  (unscoped) — description rich: "Radio, aircheck, WSTB, Akron, Chuck
  Benjamin, Innocent Age, 5-2-99, Buddy Holly, Unscoped"
- eaWLTL1199 = ear-ear, "ear" prefix of WLTL (?) — title carries no real metadata
- WBBO 98.5 FM (NYC) 3/19/99 — description contains a song-by-song snippet list
  (Savage Garden, Blackstreet, Jewel, Sheryl Crow, Rob Base & DJ E-Z Rock,
  Britney Spears, NSYNC, Jock Jam '99, Chumbawamba, Will Smith "Miami",
  The Goo Goo Dolls, Madonna, Brandy & Monica, Sugar Ray)
- New Order "True Faith" (Rare Dance Mix) FM Radio May 10, 1999 — from former
  WBMX FM Boston "Remix 98-5" show
- Q98.5 Rockford IL WXXQ FM August 1999 — PM Drive host Mark Charvat
- Radio Australia New Years Eve 1999/2000
- BBC 5975-31 December 1999

Notable: **Will Smith "Wild Wild West" does NOT appear in the 1999-exact audio
set.** Searching `text:"wild wild west"` returns one hit (a 1979 KNOE TV
Channel Eight Report, audio, unrelated). This is consistent with the user's
expectation of *future* candidates, not present ones — a new/targeted search
and more candidate triage should look for this specific item. Flagging it here
so the implementer knows the target artifact may not exist yet.

## Annotation schema (per sample)

Each annotation is a single YAML file in `annotations/<identifier>.yaml`:

```yaml
identifier: <archive.org item id>
title: <original archive.org title>
source_url: https://archive.org/details/<identifier>
collection: airchecks
scope_bucket: 1999_exact | 1999_broad | other
date: <ISO 8601 or null>
station:
  callsign: <string or null>
  frequency_mhz: <number or null>
  location: <string or null>
  format: <string or null>   # CHR, AC, oldies, etc.
  host_or_presenter: <string or null>
  program_name: <string or null>
content:
  type: <one of: song, contest, commercial, event, discussion, montage, other>
  songs:                       # ordered list of detected tracks
    - title: <string|null>
      artist: <string|null>
      start_s: <int>
      end_s: <int>
  segments:                    # DJ talk, intros, contest jingles, etc.
    - type: <string>
      time_s: <int>
      note: <string>
provenance:
  creator: <archive.org creator field or null>
  uploader: <archive.org uploader or null>
  uploaded_at: <publicdate/addeddate or null>
  original_source: <e.g. "fmairchecks.com" if mentioned>
  license_notes: <string>
quality:
  transcription_confidence: <high|medium|low|none>
  duration_s: <int|null>
  detected_songs_count: <int>
  review_status: unreviewed | reviewed | approved | rejected
  reviewer: <string|null>
  review_date: <string|null>
  notes: <string>
```

## Methodology for the annotation routine

1. **Index** — pull `data/airchecks-1999-candidates.json` (done). Build a
   SQLite or DuckDB-backed index that joins metadata fields with annotation
   state. New entries added to the same schema as we go.

2. **Triage gate (human, per sample)** — decide if the sample warrants full
   annotation. Reason to skip: no audio stream, already annotated, reviewer
   wants it kept as-is. This is the actual "routine" to build.

3. **Transcribe** — download raw mp3/ogg from archive.org, run speech-to-text
   (Whisper or faster-whisper; ffmpeg for loudness normalization + trim).
   Detect call signs, presenter names, song verbal mentions.

4. **Match against known music** — given the (high-confidence) textual list of
   songs in the description (WBBO example) plus Whisper output, cross-check
   against a track/artist database. Candidate approach: use archive.org
   metadata as seed; otherwise rely on description text + web search.

5. **Annotate** — write the YAML per the schema. Track review_status. Only
   `approved` annotations are eligible for crossposting.

6. **Crosspost** — post annotation as a comment on the archive.org item (see
   "Crosspost gate" below). Do not post anything without explicit
   human-approved annotation.

## Crosspost gate (important)

- archive.org has no public write API for comments from third-party tools.
  Comments can only be posted via archive.org's own UI, or via an authenticated
  account. **No automation against archive.org comment endpoints without
  explicit user authorization each session.**
- Default workflow: emit the annotation as markdown, then the user reviews and
  posts it themselves in the browser, or approves a manual posting per batch.

## Tools & feasibility

- ffmpeg: present (`/usr/bin/ffmpeg`).
- Audio: no `whisper`, `faster_whisper`, `librosa`, `torch` installed by
  default. We will set up a small venv (or use the 5090 toward Whisper — see
  `~/dev/*` notes) and use faster-whisper for GPU/CPU transcription.
- archive.org download: simple HTTPS download of raw mp3/ogg via
  `https://archive.org/download/<identifier>/<filename>`; metadata via
  `https://archive.org/metadata/<identifier>` (JSON). Development: use `curl`
  or `wget`.
- Music matching: no immediate approach is built. Acceptable first pass is
  using description text + Whisper output + web search to identify tracks.
- Storage: annotations are text-first (YAML), indexed via git. SQLite index
  optional.

## What's missing from the raw corpus (be honest about)

- **No Will Smith "Wild Wild West" hit in 1999 audio.** Likely either
  (a) not on archive.org yet or (b) not a 1999-year audio item. Recommend a
  second targeted search as part of the first implementation iteration.
- Descriptions are often bare ("WLTL radio") — unambiguous track lists are
  rare. The WBBO sample is an outlier in description richness; typical samples
  have none. Star transcription + music matching is required, not optional.
- "Unscoped" in several titles means "not scored (i.e. not edited/synced
  against official masters)" — these are genuinely raw, which is exactly
  what makes them collectible.
- 1999-exact vs broad 1999 mismatch: the user's 367-368 figure is not a
  uniquely-defined number. We document the difference between the three
  plausible readings above and track both in `scope_bucket`.

## Open questions

1. Is the primary scope `year:1999` (244 exact) or the broader text:1999 set
   (~367-368)? → asking the user (see below).
2. Do we want the annotation routine to be run by us (git-driven, local) or
   posted out? → already scoped: review gate means we emit markdown and the
   user posts manually.
3. Do we want the GitHub repo public or private? → asking the user.
4. Whisper backend (faster-whisper local on 5090 vs API)? → default faster-whisper,
   set up when we reach transcription.

## Risks / honest notes

- Transcribing 100s of unscoped music + radio chatter will be expensive on
  GPU/CPU time. Budgeting: 244 audio samples, ~0.5-1 hr each if fully
  transcribed and annotated → ~4-8 days of focused work. Triage gate and
  parallel batching reduce this.
- Archive.org rate-limits. Be polite: 1 request / 2+ seconds for raw downloads.
- Airchecks collection is huge (78,850 audio items). The 1999 vertical is
  manageable (244), but the "any other year" extension is **not** — never
  attempt a full-collection transcription pass.
