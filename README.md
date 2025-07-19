# ABFE_Package
Code for setting up and running replica ABFE simulations

## HPC-specific dependencies

In addition to the Python environment (`abfe_environment.yml`), this workflow requires the following modules to be loaded on the HPC environment before running:

```bash
module load gromacs/2020.3-AVX2-GPU
module load plumed/2.8.1_cuda_mpi
```

## Usage

This package provides a `SimulationSetup` class for preparing vanilla systems.

Example:
```python
from abfe.setup import SimulationSetup

setup = SimulationSetup(
    base_path="/path/to/base",
    charmm_folder="/path/to/charmm",
    protein_folder="/path/to/protein",
    sdf_folder="/path/to/sdfs",
    crystal_water_gro="/path/to/crystal_water.gro",
    mdp_templates_path="/path/to/mdp_templates",
    jobscript_template_path="/path/to/jobscript_templates"
)

setup.setup_all()
```
