# AGENTS.md

`3mf2stl`: 3MF to binary STL, one file, geometry only.

## Rules

- Python 3 standard library only. No dependencies, no venv, no pip, no build step, no vendored code.
- One file, `3mf2stl`. CLI stays `3mf2stl <input.3mf> <output.stl>`.
- Never open `Metadata/`: printer, filament, process and per-object extruder live there.
- Fail loud: raise `PackageError` with the offending value. No fallbacks, no partial output.
- Geometry only: no repair, no validation, no materials, no extra flags.

## Files

- `3mf2stl` — converter. `README.md` — usage. Test models are gitignored (`*.3mf`, `*.stl`).

## Checking a change

Both layouts must convert:

1. single-part vanilla 3MF — meshes inside `3D/3dmodel.model`;
2. Production Extension — root part holds only `<component p:path="...">`, meshes live in `3D/Objects/*.model`, each with its own object id space.

Compare triangle count and total surface area against a slicer export of the same file. Area is rotation and translation invariant, so it catches a broken transform. STL format: 80-byte header, `uint32` count, 50 bytes per triangle (12 floats + attribute).

## Style

Functions ≤ 20 lines, explicit names, comments only where the reason is non-obvious (matrix layout, id remapping). Commits: short imperative.
