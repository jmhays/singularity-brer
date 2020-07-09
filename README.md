# BRER: Singularity

This repository contains the Singularity recipe used to build containers for BRER simulations. 
A pre-built image is hosted on Sylabs Singularity [library](https://cloud.sylabs.io/library/kassonlab/default/brer). 

The main project for running these simulations is hosted at https://github.com/kassonlab/run_brer.

## Getting the container
Pull directly from singularity library (recommended):
```angular2html
singularity pull --name singularity-brer.sif library://kassonlab/default/brer
```
or build it yourself:
```angular2html
sudo singularity build singularity-brer.sif deffile
```
where `deffile` is one of the recipe files in this repository.

## Once you've got the container

### Running 
The GROMACS build in this container is GPU-compatible (built with CUDA). In order to take advantage of this, use 
the Singularity `exec` command with the `--nv` option:
```angular2html
singularity exec --nv singularity-brer.sif python3 my_run_script.py
```
`--nv` will bind the host nvidia drivers to the container, so be sure that your drivers are compatible with the CUDA version in the container (default CUDA 10.1).

An example run script is provided on the [main project website](https://github.com/kassonlab/run_brer))

Note: There is no Python 2 installed in the container (`/usr/bin/python` is actually Python3). Any Python scripts you write that you wish to run in the container 
must be compatible with Python 3.X
#### Miscellaneous
**Warning**: Use `singularity exec ...`, not `singularity run ...`.
