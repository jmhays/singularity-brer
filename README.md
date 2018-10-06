# BRER: Singularity

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/1761)

This repository contains the Singularity recipe used to build containers for BRER simulations. 
A pre-built image is hosted on Singularity Hub. 

The main project for running these simulations is hosted [here](https://github.com/jmhays/run_brer).

## Getting the container
Pull directly from singularity hub (recommended):
```angular2html
singularity pull --name singularity-brer.img shub://jmhays/singularity-brer
```
or build it yourself:
```angular2html
sudo singularity build singularity-brer.simg shub://jmhays/singularity-brer
```

## Once you've got the container

### Running 
A couple of things to note before running:
- There is no Python 2 installed in the container. Any Python scripts you write that you wish to run in the container 
must be compatible with Python 3.X
- The Python executable is `python3`, _**NOT**_ `python`. So trying to run `python` will get you nowhere. I need to
figure out how to get the alias working properly.

The GROMACS build in this container is GPU-compatible (built with CUDA 8.0). In order to take advantage of this, use 
the Singularity `exec` command with the `--nv` option:
```angular2html
singularity exec --nv singularity-brer.simg python3 my_run_script.py
```
`--nv` will bind the host nvidia drivers to the container, so be sure that your drivers are compatible with CUDA 8.0.

An example run script is provided on the [main project website](https://github.com/jmhays/run_brer))
#### Miscellaneous
**Warning**: executing `singularity run shub://jmhays/singularity-brer` won't do anything.