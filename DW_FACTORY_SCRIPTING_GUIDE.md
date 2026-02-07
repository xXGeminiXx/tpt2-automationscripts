# Perfect Tower 2 Factory AI Scripting Guide (Practical)

## Ground Rules (What Works)
- Keep each script under 50 actions after compile.
- Use multiple workers and a launcher script; do not force everything into one script.
- Use one global run toggle and one generation counter to restart workers safely.
- Use labels for flow; place impulses/conditions before labels.
- Treat factory automation as a scheduler, not a guaranteed crafter.

## Ground Rules (What Does Not Work)
- Scripts do not place machines into the factory grid for you.
- Scripts cannot bypass missing unlocks/recipes.
- A successful `craft()`/`produce()` call attempt does not guarantee immediate item increase.

## Reliable Architecture
1. `auto` script handles key toggle and starts workers.
2. Worker scripts own disjoint item groups.
3. Debug script publishes one human string + one raw string.
4. Optional bootstrap script handles early progression bottlenecks.

## Robustness Patterns
- **Generation guard**: each worker snapshots `dw_fac_gen` on start and exits if it changes.
- **Heartbeat**: maintain `dw_fac_heartbeat` in a lightweight controller loop for liveness checks.
- **Busy checks**: `active("machine")` before `produce()`.
- **Input checks**: cap requested `need` by available source count.
- **Failure hold**: set `dw_fac_err_until = now() + 10000000.` to keep failure text readable (~1 second).
- **Stall detection**: if state/tier/need repeat too long with need > 0, show stalled warning.

## State/Debug Design
- Keep numerical `dw_fac_state` for advanced users and forensic debugging.
- Reserve state ranges early to avoid collisions as package size grows.
  - Suggested: `100-199` bootstrap, `200-499` parts, `500-699` machines, `700-899` producers, `900-999` diagnostics.
- Keep `dw_fac_task` and `dw_fac_fail` as plain-language strings.
- Publish:
  - `dw_fac_human` for normal usage.
  - `dw_fac_debug` for detailed usage.

## Common Failure Modes And Handling
- **Machine busy**: set failure reason, skip to next tier/task.
- **No source inputs**: set failure reason (`Need ore`, `Need cable`, etc.), skip.
- **Recipe/unlock missing**: detected as repeated stall; show red “missing machine/unlock/materials” warning.
- **User left factory UI**: script may keep running but practical validation is easiest with factory open.

## Naming And Packaging Recommendations
- Use a stable package namespace for public release (example: `DW.Factory:*`).
- Keep file names aligned with script role (`auto`, `base`, `parts_*`, `machines_*`, `debug`, `bootstrap`).
- Document keybinds and required script list in one README.

## Extending To Other Systems (Museum/Lab/etc.)
- Reuse the same pattern:
  - launcher,
  - specialized workers,
  - debug/status publisher,
  - bootstrap if progression gates exist.
- Avoid large single scripts; split by responsibility and data flow.
