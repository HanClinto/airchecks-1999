# Handoff 02 — Transcription toolchain setup

## Status
Not started

## Context
We transcribe raw aircheck audio with Whisper/faster-whisper. No whisper
package is installed; we have NOT run transcription yet. The 5090 is occupied
by Inkling 2 (~27GB of 32GB VRAM, ~5GB free; 24-core Ultra 9 CPU, 62GB RAM
with 48GB available).

## Hard constraints
- Do NOT touch the Mac Mini speechcheck service (10.0.1.83:8097) for this.
  It is purpose-built for Korean pronunciation checking (language="ko", Korean
  phoneme scoring, 30s max audio) and backs Lingo; not a general endpoint.
- The Mac Mini's Homebrew openai-whisper / faster-whisper base.en exist but
  require SSH keys from this box that are not configured here.
- 5090: 5GB VRAM free. Whisper small/base fits; large-v3-turbo (~3GB) is
  marginal alongside Inkling 2. CPU fallback is workable.

## Inputs
- `config/endpoints.example.yaml` (committed) — shows the expected config shape.
- `config/endpoints.local.yaml` (gitignored) — actual private endpoints.

## Tasks
1. Create a small venv (e.g. `.venv/`, gitignored) with faster-whisper.
   Consider `openai-whisper` for fidelity at large models vs faster-whisper
   for speed/CPU use. Default: faster-whisper (small or medium model).
2. Verify the venv runs on the box: transcribe a small public audio fixture and
   confirm output is sane.
3. Record the chosen model, backend, and VRAM/CPU posture in this handoff.
4. Wire transcription to the gitignored config shape; never commit private
   endpoints or the local env.
5. Decide: GPU-with-Inkling-2 (small/base, marginal) vs CPU (larger model,
   slower) vs pause Inkling 2 for the heavy pass.

## Outputs
- `.venv/` (gitignored) or documented system-level fallback.
- This handoff updated with the decision + date.
- Optionally a smoke-test transcript labeled as such.

## Done when
- One 1999-scoped audio sample transcribes end-to-end.
- The chosen backend + model are recorded in this handoff.

## Risks / notes
- If CPU-only, large-v3-turbo will be slow but fine for triage.
- Keep the local config gitignored; never commit endpoints.local.yaml.
