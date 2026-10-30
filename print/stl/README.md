# STL files

One file per part, in print orientation, in millimetres, named `<side>_<part>.stl`:
`torso.stl`, `l_hip_upper.stl`, `r_hip_upper.stl`, `l_thigh.stl`, ...
Parts identical on both sides drop the side prefix and get `qty: 2` in
[`../../bom/printed_parts.csv`](../../bom/printed_parts.csv).

These are print files, not the simulation meshes. The meshes in
[`../../robot_description/meshes/`](../../robot_description/meshes/) are in URDF link frames and may merge
several printed parts into one link.

Before a release, re-export these from the latest CAD and check them against the parts on the robot.
