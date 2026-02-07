# DW Factory Automation (Publish Build)

This package is a full replacement for previous `DW:fac_*` scripts.

## Scripts To Import
- `DW.Factory:auto` from `DWFactory_auto.txt`
- `DW.Factory:controller` from `DWFactory_controller.txt`
- `DW.Factory:base` from `DWFactory_base.txt`
- `DW.Factory:base_plate` from `DWFactory_base_plate.txt`
- `DW.Factory:parts_stack` from `DWFactory_parts_stack.txt`
- `DW.Factory:parts_refine` from `DWFactory_parts_refine.txt`
- `DW.Factory:parts_board` from `DWFactory_parts_board.txt`
- `DW.Factory:parts_circuit` from `DWFactory_parts_circuit.txt`
- `DW.Factory:parts_shape1` from `DWFactory_parts_shape1.txt`
- `DW.Factory:parts_shape2` from `DWFactory_parts_shape2.txt`
- `DW.Factory:parts_block` from `DWFactory_parts_block.txt`
- `DW.Factory:machines_a` from `DWFactory_machines_a.txt`
- `DW.Factory:machines_b` from `DWFactory_machines_b.txt`
- `DW.Factory:producers_core` from `DWFactory_producers_core.txt`
- `DW.Factory:producers_gems` from `DWFactory_producers_gems.txt`
- `DW.Factory:debug` from `DWFactory_debug.txt`
- Optional: `DW.Factory:bootstrap` from `DWFactory_bootstrap.txt`

## One-Key Usage
1. Run `DW.Factory:auto` once.
2. Press `F` to toggle all automation ON/OFF.
3. Keep Factory open while validating behavior.

## What It Covers
- Core chain: `ore`, `dust`, `ingot`, `plate`
- Mid parts: `plate.stack`, `plate.dense`, `cable`, `wire`, `plate.circuit`
- Advanced parts: `circuit`, `chip`, `rod`, `screw`, `pipe`, `ring`
- Blocks: `block`, `block.dense`
- Machines (all tiers):
  - `machine.oven`, `machine.crusher`, `machine.presser`, `machine.refinery`, `machine.assembler`
  - `machine.cutter`, `machine.shaper`, `machine.mixer`, `machine.boiler`, `machine.transportbelt`
- Producers (all tiers where applicable):
  - `producer.shipyard`, `producer.statueofcubos`
  - `producer.gems`, `producer.exoticgems`

## Debug Output
- `dw_fac_human`: concise human-readable status.
  - Green: currently attempting task.
  - Red: blocked/stalled reason.
  - Gray: automation off.
- `dw_fac_debug`: raw advanced diagnostics (state, machine activity flags, counts).
- `dw_fac_heartbeat`: controller liveness counter (increments while running).

## Missing Recipe/Machine Cases
If a path is unavailable (recipe not unlocked, machine not built, missing inputs), the script:
- updates red status text with reason,
- keeps trying other tasks,
- returns to blocked path later.

## Bootstrap Mode
Use `DW.Factory:bootstrap` if assembler progression is stuck early.
It front-loads stacked/dense plates, cable, wire, then repeatedly attempts assembler craft.

## Repo Files
- Front-page guide: `README.md`
- Direct import export blobs: `DW_FACTORY_EXPORT_BLOBS.md`
- Implementation notes: `DW_FACTORY_SCRIPTING_GUIDE.md`
