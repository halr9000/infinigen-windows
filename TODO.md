# TODO

## Goals

- [ ] Make this thing work on Windows w/o WSL
  - (optional) make it x-plat for fun
- [ ] Fully-automated, two steps only: clone & install

## How?

- requirement: pwsh (not Windows PowerShell)
- requirement: cuda
- requirement: OpenGL
- requirement: conda (probably)
- let python and conda do their things

## Tasks

### Reesarch

- [ ] figure out what install.sh does
- [ ] look at those git submodules
- [ ] review llvm requirements
- [ ] review py requirements
- [ ] review blender-python requirements
- [ ] review terrain requiremtns
- [ ] review NURBS requirements
- [ ] make sure it'll work with blender/windows

### Code

- [ ]  write an install script in powershell

## Questions to Answer

- can I use an external blender?
- can any of this compiling be avoided?
- how hard is it to publish a bpy plugin?

## Research Notes

### install.sh

- checks for wget, which we don't care about in powershell. Will use IWR or BITS (that might require windows powershell tho, don't recall)

### blender

They download and install blender, dunno why.

### submodules

submodule "worldgen/infinigen_gpl"
submodule "process_mesh/dependencies/eigen"
submodule "process_mesh/dependencies/argparse"
submodule "process_mesh/dependencies/cnpy"
submodule "process_mesh/dependencies/indicators"
submodule "process_mesh/dependencies/tinycolormap"
submodule "process_mesh/dependencies/glm"
submodule "process_mesh/dependencies/fast_obj"
submodule "process_mesh/dependencies/json"
submodule "process_mesh/dependencies/stb"
submodule "process_mesh/dependencies/glfw"

### llvm

Hrm this looks heavy https://llvm.org/docs/GettingStartedVS.html

### python/conda deps

(why did they require use of conda but not use a conda env.yaml?)

Notables top of my head:

scikit-learn
numpy
opencv-python

fake-bpy-module-latest (why isn't this in reqs?)

### python include files

Seems to be related to Blender as they copy them there. Must be required for compiling using bpy.

### Blender deps

Starts by running ensurepip in bpy. Doesn't it include pip?

environment -> CFLAGS

### worldgen itself

Looks like they monkeypatch worldgen into the newly installed blender...guess they wanted to make this self-contained and not distribute as a blender module in that ecosystem, which is weird to me.

### build worldgen/terrain

Looks for cuda/nvcc and will pass that result to install_terrain.sh

Build process runs inside of blender-python

### build NURBS

Also runs using blender-python.

Seems to optionally compile OpenGL in as well?
