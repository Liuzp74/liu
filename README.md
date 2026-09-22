# Thermal Conductivity Prediction and Structural Inversion of Quartz Fiber Fabrics

> **Data-driven design of thermal performance for textile composites in aerospace electronic packaging and thermal protection**

## Overview

Owing to their low dielectric constant, excellent thermal stability, and good mechanical properties, quartz fiber fabrics are essential in aerospace electronic packaging and thermal protection. This project establishes a digital framework that integrates **parametric modeling, data-driven prediction, and structural inversion**, covering three fundamental weaves: plain, twill, and satin.

- **Unified parametric encoding**: maps the three weaves into a common mathematical space;
- **High-throughput modeling and simulation**: geometric models generated in TexGen, with a training dataset built via steady-state heat conduction simulations in Abaqus;
- **Neural network surrogate model**: significantly more accurate than conventional mixture rules, and about three orders of magnitude faster than direct finite element analysis (second-scale response);
- **Structural inversion**: couples the surrogate model with a differential evolution algorithm and introduces a weaveability-constrained penalty function, enabling intelligent inversion from target thermal conductivities to fabric structural parameters.

This repository provides the **generated dataset**, the **neural network model code**, and the **fabric structural inversion code for specific engineering scenarios**, supporting reproducibility and further development.

## Repository Structure

```
quartz-fabric-thermal/
├── data/                      # Training dataset (geometry-thermal-conductivity samples for the three weaves)
│   ├── plain/                 # Plain weave samples
│   ├── twill/                 # Twill weave samples
│   └── satin/                 # Satin weave samples
├── model/                     # Neural network surrogate model
│   ├── dataset.py             # Data loading and preprocessing
│   ├── network.py             # Network architecture
│   ├── train.py               # Training script
│   └── predict.py             # Fast thermal-conductivity prediction interface
├── inversion/                 # Structural inversion code
│   ├── surrogate.py           # Surrogate model wrapper
│   ├── de_optimizer.py        # Differential evolution optimizer
│   ├── constraints.py         # Weaveability-constrained penalty function
│   └── run_inversion.py       # Main inversion program (three typical engineering scenarios)
├── requirements.txt
└── README.md
```

> Note: the structure above is an example; please adjust paths and file names according to the actual layout.

## Usage

### 1. Dependencies

- Python 3.9+
- PyTorch (or the framework actually used)
- NumPy / pandas / scikit-learn
- Matplotlib (visualization)
- TexGen and Abaqus (only if regenerating the dataset)

```bash
pip install -r requirements.txt
```

### 2. Quick Start

**(1) Load the dataset**

```python
from model.dataset import FabricDataset

dataset = FabricDataset(root="data", weaves=["plain", "twill", "satin"])
```

**(2) Train / load the surrogate model**

```bash
python model/train.py --data_dir data --epochs 500
```

**(3) Run structural inversion**

```bash
python inversion/run_inversion.py --scenario 1 --target_kx 0.8 --target_ky 0.6
```

The inversion outputs the optimal fabric structural parameters (yarn spacing, number of layers, fiber volume fraction, etc.) together with the predicted thermal conductivities.

### 3. Typical Engineering Scenarios

The inversion code includes representative scenarios. Switch between them via `--scenario`, or customize the target conductivities in the configuration file.

## Useful Resources

| Resource | Link |
|---|---|
| TexGen (textile geometric modeling) | https://www.texgen.co.uk/ |
| Abaqus (FEA, Dassault Systemes) | https://www.3ds.com/products/simulia/abaqus |
| PyTorch | https://pytorch.org/ |
| Differential evolution reference | https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.differential_evolution.html |
| Project paper (if available) | <DOI / journal link, to be added> |

## Citation

If you use the data or code from this repository in your research, please cite:

```
<To be added: paper BibTeX>
```


