# SOFiA application examples R 11-1220 #

The SOFiA package comes with some application examples to demonstrate how the software works and to provide you with a basic draft for writing your own scripts. The application examples are simple matlab scripts that should run out of the box. Only make sure that all necessary SOFiA routines/files are accessible to these scripts. Some of the examples run on real measured array data. You need our [array datasets](ARRAY_DATA.md) to execute them.

### Overview ###

| **Number** | **Content** | **Simulation or real array data** |
|:-----------|:------------|:----------------------------------|
| [AE1](AE1.md) | Generating an ideal plane wave using [W/G/C](WGC.md) and visualizing the result using [makeMTX](MAKE_MTX.md) and [visual3D](VISUAL_3D.md). | Simulation                        |
| [AE2](AE2.md) | Generating a discretely sampled plane wave using [S/W/G](SWG.md) on a Lebedev-Grid  | Simulation                        |
| [AE3](AE3.md) | Observing a "real plane wave"  | Real array data                   |
| [AE4](AE4.md) | Observing 4 "real plane waves" coming from different directions having different levels  | Real array data                   |
| [AE5](AE5.md) | Observing 4 "real plane waves" coming from different directions at different arrival times  | Real array data                   |
| [AE6](AE6.md) | Reconstruction of an ideal impulse response  | Simulation                        |
| [AE7](AE7.md) | Reconstruction of an aliased impulse response  | Simulation                        |
| [AE8](AE8.md) | Rendering directional RIR from a Classroom  | Real array data                   |