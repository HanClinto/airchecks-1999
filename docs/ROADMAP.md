# Parallel workflows — airchecks-1999

## Workflow map

```
01 Scope & corpus ──▶ 03 Index ──▶ 04 Triage ──▶ 06 Annotation routine
                                       │                  │
                                       │                  ▼
                                       │              08 Music matching
                                       │                  │
                                       └────────────▶ 07 Crosspost (gated)

02 Transcription (parallel to 01/03/04)
05 Wild Wild West search (isolated, parallel)
09 Repo polish (parallel, low priority)
```

## Workflow table

| # | Workflow | Handoff | Depends on | Runs in parallel with | Owner state |
|---|----------|---------|------------|----------------------|-------------|
| 01 | Scope & corpus | `docs/handoffs/01-scope-and-corpus.md` | — | 02, 05, 09 | Pending user decision |
| 02 | Transcription toolchain | `docs/handoffs/02-transcription-toolchain.md` | — | 01, 03, 05, 09 | Not started |
| 03 | Index build | `docs/handoffs/03-index-build.md` | 01 (scope) | 02, 05, 09 | Not started |
| 04 | Triage & batching | `docs/handoffs/04-triage-and-batching.md` | 03 | 02, 05, 09 | Not started |
| 05 | Wild Wild West search | `docs/handoffs/05-wild-wild-west-search.md` | — | 01, 02, 03, 04, 09 | Not started |
| 06 | Annotation routine | `docs/handoffs/06-annotation-routine.md` | 02, 03, 04, 08 | — | Not started |
| 07 | Crosspost gate | `docs/handoffs/07-crosspost-gate.md` | 06 | — | Not started |
| 08 | Music matching | `docs/handoffs/08-music-matching.md` | 02, 06 | 02, 03 | Not started |
| 09 | GitHub repo finalization | `docs/handoffs/09-github-repo-finalization.md` | — | 01, 02, 03, 04, 05, 06, 07, 08 | Partially done |

## Sequencing

- **Parallel batch A** (start now, no dependency): 01 (pending user input), 02, 05, 09.
- **Parallel batch B** (after 01 picks the scope): 03, and 08's preprocessing steps.
- **Batch C** (after batch B + 02): 04, 08, and 06 once the transcription and
  index are ready.
- **Batch D** (after 06): 07 — gated on human review.

## Priorities

1. **01 (scope)** — blocks 03/04/06/07. User input needed.
2. **02 (toolchain)** — blocks 06/08. Feasible to start now.
3. **05 (Wild Wild West)** — independent, cheap, flag for user.
4. **03 (index)** — cheap once scope is picked.
5. **04 (triage)** — human-in-the-loop.
6. **08 (music matching)** — hard, continuous improvement, not gated.
7. **06 (routine)** — main workflow; depends on 02/03/04/08.
8. **07 (crosspost)** — gated on human review.
9. **09 (repo polish)** — low priority, mostly README update.

## Status snapshot (as of 2026-11-25)

- Repo created: https://github.com/HanClinto/airchecks-1999 (public)
- Candidate index: 244 items (year:1999 exact)
- No transcription runs; no annotations; no crosspost queue.

## Exit criteria (first milestone — the 1999 vertical)

- Scope confirmed; index built; one full annotation (YAML verified) for one
  1999-scoped sample; Wild Wild West outcome recorded; README reflects the
  new state.

## Exit criteria (second milestone — 1999 batch)

- All triaged-in samples have annotations.
- At least one approved annotation exists.
- Crosspost queue is emitted and pending human review.
