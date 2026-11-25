# Airchecks 1999 — goals and index taxonomy

## What the catalog is for

An extensible, structured catalog of aircheck samples from the archive.org
`airchecks` collection. An "aircheck" is a recording of a radio station airing
— not a studio master. These are rare, unlicensed-by-intent bootleg artifacts.
Collectors, archivists, historians, and fans of personalities / contests /
commercials / events use them to verify exactly what a station played, when,
and often who was live on the air.

The catalog is text-first (YAML annotations), git-tracked, and extensible to
any year or item — 1999 is the anchor, not the boundary.

## The content taxonomy (what we want to index)

Every sample gets one `content.type` in the annotation. The types are ordered
by collector priority — the first three are the flagships.

### 1. Exclusive / partner-station releases  ← flagship
- Description: A song played on one station before another (e.g. Will Smith's
  "Wild Wild West", May 1999, on exclusive partner stations with call-letter
  overlays to prevent other stations from recording and rebroadcasting as
  their own). These are the rarest provenance artifacts: evidence of a
  specific station's early-release hold.
- Evidence: description text mention of an exclusive / early release; call
  letters or overlays mentioned; agreement with press or release coverage;
  date precedes commercial release.
- Status: NOT found yet (see "Flagship pursuit" below) — this is a specific
  search, not a guess.

### 2. Radio edits and remixes
- Description: DJ/host-curated edits of songs — rare EDM remixes, extended
  mixes, "remix 98-5" shows, "True Faith" dance-mix style. These are the most
  distinctive 1999-specific content type.
- Evidence: description mentions of remix/edit/rare/dance-mix; station shows
  that feature one song per broadcast.
- Example: `true-faith-rare-dance-mix-fm-radio-may-10-1999` (New Order "True
  Faith" EDM remix, "Mix Music Variety" show, WBMX FM Boston).

### 3. Commercials and promos
- Description: Promoted spots, sponsor drives, "Promo" or "Spot" segments.
- Evidence: title/description mentions commercial/promo/spot; radio station
  metadata suggests ad play.
- Example: `wruw-bill-anderson-1960-r-b-12-19-99-unscoped` (classified as
  commercial by heuristic).

### 4. Radio host spots (presenter-anchored)
- Description: A show anchored by a known DJ / presenter / host. High value
  for collectors of radio personalities.
- Evidence: host/DJ name in title or description.
- Examples: `81.3-mhz-j-wave-1999-hip-hop-journey-da-cypher-with-dj-hasebe-sugar-soul`
  (J-Wave, Dj Hasebe & Sugar Soul), `q-98.5-rockford-il-wxxq-fm-aircheck-...`
  (Mark Charvat, PM Drive), `kut-american-pop-...-host-louis-harrison-...`
  (Louis Harrison — recurring), `wubt-103.5-mhz-the-beat-...` (Jammin' Only).

### 5. Oldies and classic-edits
- Description: 60s/70s/80s classic edits played in 1999 — "The Fleetwoods",
  "oldies", "1960 R&B". Heavy in the corpus (~half of 1999-exact).
- Evidence: oldie/classic/early-60s/50s mentions in title/description.
- Example: `innocent-age-chuck-benjamin-wstb-9-26-99-unscoped` (early 1960s,
  The Fleetwoods, Chuck Benjamin, Innocent Age).

### 6. Personalities and interviews
- Description: One-on-one DJ/host spotlights, interviews, special shows.
- Evidence: named host/guest pair in title or description.
- Examples: `wbbo-mar-19-1999` (WBBO 98.5 FM song list), `wstb-innocent-age-...`
  (Chuck Benjamin), `OA-1999-05` (Opie and Anthony), O&A,
  ` kut-american-pop-louis-harrison-...`.

### 7. Contests, sweepstakes, giveaways
- Description: Promotional contest broadcasts, call-in contests, giveaways.
- Evidence: contest/sweepstake/giveaway/promotion keyword.
- Example: none found in 1999-exact corpus — treat as a fresh search.

### 8. Events and live broadcasts
- Description: Birthday spots (e.g. WDHA birthday songs for a specific
  person), live events, station anniversaries.
- Evidence: birthday/event/live keyword; named person + date.
- Example: WDHA-105.5 birthday songs (2023, outside 1999), `knoe-tv-8-...`
  (1979).

### 9. Pirate / unlicensed broadcasts
- Description: Recordings of unlicensed or pirate stations. Rare and novel
  provenance.
- Evidence: title/description mention of pirate/BTR/unlicensed/underground.
- Example: `btr-milwaukee-pirate-92.9-102399-rock-punk` (BTR Milwaukee pirate).

### 10. International / foreign stations
- Description: Stations outside the US (Japanese, French, Australian).
- Evidence: station city/country in title/description.
- Examples: `81.3-mhz-j-wave-...` (Tokyo, JAPAN),
  `101.9-mhz-fun-radio-1997-star-system-special-techno-house-mix-avec-max`
  (Paris, FRANCE).

### 11. Radio-edit montages / compilations
- Description: Compilation shows, "set" broadcasts with multiple songs.
- Evidence: multiple songs in one broadcast, no single host.
- Example: `true-faith-...` (one song per show but editorial in shape).

### 12. Commercials / promos (broad) — see type 3
### 13. Other (unclassified)
- Description: Anything that doesn't fit. Kept, not dropped.

## The flagship pursuit: Will Smith "Wild Wild West" (May 1999)

**Goal**: find one or more 1999 aircheck samples that feature Will Smith's
"Wild Wild West" (released May 1999 on exclusive partner stations with
call-letter overlays).

**Status as of 2026-11-25**: NOT FOUND.

Evidence gathered (all negative):
- `collection:airchecks AND text:"wild wild west"` → 1 hit (KNOE TV 8,
  May 2, 1979 — 1979, wrong year).
- `collection:airchecks AND title:"wild wild"` → 0 hits.
- `collection:airchecks AND subject:"wild wild west"` → 0 hits.
- `collection:airchecks AND text:"will smith"` → 3 hits, none 1999-era
  Wild Wild West (WBBO 98.5 FM 3/19/99 — Will Smith "Miami", not Wild
  Wild West; 1997 Z-Planet Z100 — unrelated; ORT Mixtape — unrelated).
- `collection:airchecks AND text:"wild wild"` → 8 hits, none 1999-era
  or Wild Wild West (WBBO 98.5 FM 3/19/99, KNOE TV 8 1979, A-log on the
  Airwaves 2011/2016, Skoipunka shows — unrelated).
- **Hand-check (per user)**: close to 20 samples checked by hand, none
  contain a Wild Wild West play.

**What we know**: "Wild Wild West" was indeed a Billboard hit in 1999.
The airchecks collection may simply not have the artifact, or it may be
archived under a different collection (e.g. `RadioRecordings`,
`will-smith`, or a music-specific collection).

**Remaining plan** (handoff 05):
- Search a wider archive.org set (all collections) for Wild Wild West.
- Check Will Smith-specific collections.
- If still nothing found, record as "not present in archive.org" in the
  handoff; revisit with user confirmation.

**Why this matters**: it is the flagship provenance artifact of the 1999
exclusive-release story (billboard hit + early partner-station release with
call-letter overlays). Crucially, if we can find ONE aircheck of it, the
catalog gains the example the user asked for; if we cannot, the catalog
documents why it is absent.

## What each entry in the catalog must support

Per annotation (see `docs/PROJECT.md` for schema):
1. Station: callsign, frequency, location, format, host/presenter, program name.
2. Content: type (one of the taxonomy above), songs (title, artist, year,
   confidence, source URL), segments (DJ talk, contest intros, etc.).
3. Provenance: creator, uploader, original source (fmairchecks.com, mixcloud,
   etc.), license notes.
4. Quality: transcription confidence, duration, review status, notes.

## Priority order for the 1999 vertical

| Priority | Taxonomy type | Why |
|----------|---------------|-----|
| P1 | Exclusive / partner-station releases | Flagship story; no examples yet |
| P2 | Radio edits and remixes | Signature 1999 content; distinctive |
| P3 | Radio host spots | Anchor catalog around named personalities |
| P4 | Oldies and classic-edits | Corpus-heavy (~half of 1999) |
| P5 | Commercials / promos | Rare, collectible |
| P6 | Personalities / interviews | Rarity; named hosts |
| P7 | Contests / sweepstakes | Rare (none found) |
| P8 | Events / live broadcasts | Rare (none found) |
| P9 | Pirate / unlicensed broadcasts | Rare, novel provenance |
| P10 | International | Minority class; few items |

## Non-goals (explicit)

- Do NOT do a full-collection transcription pass — the archive.org
  `airchecks` collection is ~78,850 audio items; only 1999 (244) is in
  scope.
- Do NOT auto-post annotations as archive.org comments — review gate.
- Do NOT record unverified songs — null + "unknown" is fine.
- Do NOT transcribe bare-metadata samples just to fill a count.
- Do NOT touch the Mac Mini speechcheck service for this project.

## Extensibility

Any year or item can be labeled with the same content taxonomy by:
1. Adding an item to `data/<year>-candidates.json` with a `scope_bucket` field.
2. Running the same annotation routine per handoff 06.
3. Annotating with the same schema + content type.
