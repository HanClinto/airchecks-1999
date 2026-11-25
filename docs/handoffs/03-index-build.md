# Handoff 03 — Index build

## Status
Not started

## Context
A machine-readable index joins the (canonical) candidate set with annotation
state so we don't re-scan archive.org. Git holds the annotations; the index is
a local, rebuildable cache.

## Inputs
- `data/airchecks-1999-candidates.json` — candidate set.
- `docs/PROJECT.md` — schema (annotation YAML).

## Tasks
1. Choose the index: SQLite (zero deps, matches existing tooling) or DuckDB.
   Default: SQLite, file at `data/index.db` (gitignored or lightly committed).
2. Schema: one row per item — identifier, scope_bucket, title, date,
   description, creator, local status (untriaged | triaged-skip | queued |
   transcribing | annotated | approved | rejected), review_status,
   annotation_path.
3. `tools/build_index.py` — reads the candidates JSON, creates/migrates the
   SQLite schema, upserts rows, refreshes metadata (cheap idempotent pass).
4. Record the schema in this handoff (table + column list).

## Outputs
- `tools/build_index.py` (committed).
- `data/index.db` (gitignored or minimal).

## Done when
- `sqlite3 data/index.db 'select count(*) from items;'` returns the scoped
  count (~244 for year:1999, ~346 for broad).
- Rebuilding is idempotent (safe to re-run).

## Risks / notes
- Index is a cache, not canonical data — canonical state lives in
  `annotations/` and `data/airchecks-1999-candidates.json`.
- Refresh must be polites-rate-limited (~1 req per 2s).
