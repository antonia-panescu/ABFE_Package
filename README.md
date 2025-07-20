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
    base_path           = "/ABS/PATH/TO/WORK/FOLDER",                 # e.g. "/home/user/projects/a2a_run"
    charmm_folder       = "/ABS/PATH/TO/CHARMM_GMX",                  # …/system_setup/charmm/charmm_gmx
    protein_folder      = "/ABS/PATH/TO/PARAMETERISED_PROTEIN",       # …/protein_prep/protein_param
    sdf_folder          = "/ABS/PATH/TO/LIGAND_SDFS",                 # folder full of *.sdf
    crystal_water_gro   = "/ABS/PATH/TO/crystal_waters.gro",          # the file you merge in
    mdp_templates_path  = "/ABS/PATH/TO/MDP_TEMPLATES",               # dir that contains your .mdp files
    jobscript_template_path = "/ABS/PATH/TO/JOBSCRIPT_TEMPLATES",     # dir with SLURM/Archer scripts

    # the three below are optional (defaults shown):
    solvate_water_count = 10286,
    crystal_water_count = 136,
    num_nodes           = 2
)

# prepare every ligand in the SDF folder
setup.setup_all()

# or, for a single ligand, single run:
# setup.setup_simulation("cmp_123")

# all ligands, 5 repeats
# setup.setup_all(repeats=5)

# single ligand, custom repeats (three replicas for only cmp_42
# for replica in range(1, 4):
#    setup.setup_simulation("cmp_42", replicate=replica)
```
