# STEP files

- `sir_servington_assembly.step`: the full robot assembly.
- One file per unique part, named like the print files: `torso.step`, `l_hip_upper.step`, `l_thigh.step`, ...
  Mirrored left/right parts get one file each; parts that are the same on both sides get one file
  without a side prefix.

Export from the same CAD version as the STLs in [`../../print/stl/`](../../print/stl/).
