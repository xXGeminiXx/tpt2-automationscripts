# AGENTS.md - Perfect Tower 2 Automation Repo Guide

This repository is dedicated to The Perfect Tower II automation scripts and docs.
Primary focus right now is Factory automation with publishable, import-ready script blobs.

## 1) Repo Scope
- Game: The Perfect Tower II
- Current completed domain: Factory
- Current partial domain knowledge: Museum patterns, script architecture, UI-safe automation practices
- Not fully automated yet: Modules/Blueprint/Damage systems

## 2) What We Know (Factory)
- Script package naming is standardized as `DW.Factory:*`.
- Master control is `DW.Factory:auto` with one-key toggle (`F`) via `dw_run`.
- Orchestration pattern:
  - Shared globals for state/debug
  - Generation-based restart (`dw_fac_gen`)
  - Heartbeat/liveness (`dw_fac_heartbeat`)
  - Independent worker scripts by domain (base, parts, machines, producers, shop)
- Debug/status channels:
  - `dw_fac_human` = player-facing status text
  - `dw_fac_debug` = advanced diagnostics
- Failure handling pattern:
  - `dw_fac_err`, `dw_fac_fail`, `dw_fac_err_until`
  - Red message persists long enough to read, then scheduler continues

## 3) What We Know (Game Constraints)
- Scripts cannot place machines in the factory grid; player layout must exist.
- Recipes may fail from missing unlocks/materials; this must be treated as normal runtime state.
- UI click automation (shop buying) requires the correct UI open and visible.
- Historical note: older turbo-based script assumptions are not valid for this repo direction.

## 4) Current Factory Coverage
- Base resources and shaping chains
- Parts, machine crafting, producer crafting
- Gem + exotic gem producer goals
- Shop automation components:
  - `DW.Factory:shop` (craft-side attempt loop)
  - `DW.Factory:shop_buy` (Factory Shop UI buyer)
- Bootstrap helper:
  - `DW.Factory:bootstrap` for early assembler progression bottlenecks

## 5) Modules / Blueprint / Damage Status
- We have architecture and automation patterns that transfer well.
- We do NOT yet have a complete modules/blueprint/damage automation implementation in this repo.
- For that domain, collect and store:
  - exact item/system names used by TPT2 AI calls
  - unlock flow and prerequisite chains
  - UI screenshots for tabs and button targets
  - known valid script calls and failure symptoms

## 6) Authoring Rules For This Repo
- Keep source scripts in `DWFactory_*.txt`.
- Keep publish docs updated:
  - `README.md`
  - `DW_FACTORY_EXPORT_BLOBS.md`
- Import blobs must be code-block safe and header-free:
  - include ONLY encoded blob string in code fences
  - do NOT prepend `DW.Factory:name` or `1 0 N` lines in copy blocks
- Prefer additive changes over removal unless explicitly requested.

## 7) Validation Checklist After Script Changes
- Confirm compile success in external editor.
- Verify toggle behavior (`F`) and global state flips.
- Verify at least one successful action path and one blocked path message.
- Ensure red blocked message remains readable before switching tasks.
- Confirm no unintended script stalls (heartbeat/state still moving).

## 8) Git Sync Workflow (Default)
- After any meaningful change:
  - update relevant docs and import blobs
  - `git add` changed files
  - `git commit` with a clear message
- Keep branch ready for push immediately after commit.
- If user asks to push, push without rebasing unrelated history.

## 9) Near-Term Automation Roadmap
- Factory hardening and edge-case tuning
- Museum modernization
- Modules/Blueprint/Damage automation package
- Shared utility patterns for status, retries, and scheduler behavior

