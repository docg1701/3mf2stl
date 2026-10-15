# 3mf2stl

Geometry from a 3MF file into a binary STL. Python standard library only.

```bash
./3mf2stl input.3mf                      # writes input.stl beside it
./3mf2stl path/*.3mf                     # one .stl per .3mf, same names
```

Every input is written next to its 3MF as `<same name>.stl`; there is no output argument. A file that fails is reported on stderr and the rest keep converting; the exit status is 1 if any failed.

Reads `<mesh>`, `<component>` (3MF Production Extension, `p:path`), `<item>` and `<component>` transforms, and the `unit` attribute (output in millimetres). `Metadata/` is never opened, so printer, filament, process and per-object extruder settings cannot reach the output.

Not handled: `beamlattice`, materials/colours, mesh repair.

Verified against OrcaSlicer 2.4.2 CLI export (`--export-stl`) on MakerWorld files:

| file | layout | triangles | total surface area |
|---|---|---|---|
| 3 objects | Production Extension, 3 parts | 14370 | 33644.2878 vs 33644.2877 |
| 12 objects | single-part | 54422 | — |
