# free_energy_demos

A collection of self-contained demonstrations of free energy
calculation methods, built around real molecular systems. Each demo is a
Jupyter notebook that walks through a full pipeline end to end, with the
theory explained alongside the code, so it can be read as a tutorial or run
as a working example.

## Demos

### RBFE demo (`rbfe_demo/`)

A relative binding free energy (RBFE) calculation on the
[OpenFE TYK2 benchmark set](https://github.com/OpenFreeEnergy/openfe-benchmarks),
using pmx hybrid topologies, GROMACS, OpenFF, and alchemlyb. The notebook
covers the full workflow:

1. **Network planning** - score ligand similarity with LOMAP and build a star
   network of alchemical transformations.
2. **Hybrid topology** - parameterize ligands and protein with OpenFF, then
   build dual-topology hybrid molecules with pmx.
3. **Simulation** - minimize, equilibrate, and run production sampling, with
   two interchangeable approaches (fixed-λ windows and expanded ensemble) and
   templates for running on a cluster.
4. **Analysis** - estimate ΔΔG with TI and MBAR via alchemlyb, with
   overlap-matrix and dH/dλ diagnostics.

*(More demos to come.)*

## Getting started

Each demo has its own setup instructions in its notebook (see Stage 0 of the
RBFE notebook). In brief, for the RBFE demo:

```bash
mamba create -n rbfe-demo -c conda-forge python=3.10 \
    openff-toolkit rdkit lomap2 networkx py3dmol "setuptools<82" \
    alchemlyb pandas numpy matplotlib ipykernel
mamba activate rbfe-demo
mamba install -c conda-forge gromacs    # <--- if needed
```

pmx should be installed from source:

```bash
git clone https://github.com/deGrootLab/pmx.git
cd pmx && git checkout develop
pip install --no-build-isolation .
```

An `environment.yml` is provided as a starting point (pmx still installed
separately). See the notebook's Stage 0 for full details.

## Requirements

- Python 3.10
- GROMACS
- pmx, OpenFF Toolkit, RDKit, LOMAP, alchemlyb

## Running

Open the notebook and run the stages in order. Simulations can be run directly
from the notebook (fine for a small test) or submitted to a cluster; the
notebook includes annotated Slurm templates for both the fixed-λ and
expanded-ensemble approaches.

Pre-computed example output is available for the analysis stage, in case your
own runs are still in progress: see the pointer in the notebook.
