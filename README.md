# PSO inverse design of a coaxial microdroplet generator

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mfgerard/PSO_inverse_design/blob/main/PSO_inverse_design.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Companion notebook for the paper

> D. G. Harispe, M. Gerard, P. A. Kler. *Microdroplet Generator Surrogate Enhancement and Inverse Design Through an Uncertainty-Guided Framework.* arXiv:2611.06464 (2026). <https://arxiv.org/abs/2611.06464>

Given a target droplet diameter, the notebook searches for operating and design parameters of a coaxial microdroplet generator (capillary and Weber numbers, phase viscosities, inner capillary radius) that produce it in the dripping regime. Particle Swarm Optimization (PSO) minimizes an uncertainty-aware fitness function evaluated with two ensembles of trained neural-network surrogates: a regime classifier and a droplet-diameter regressor, each with 20 members.

## Contents

| Path | Description |
|---|---|
| `PSO_inverse_design.ipynb` | Notebook: configuration, surrogate loading, fitness function, PSO, independent runs and search report |
| `models/regime_ensemble.pt` | Regime classifier ensemble (dripping / narrowing jet / widening jet), 20 members |
| `models/diameter_ensemble.pt` | Droplet-diameter regressor ensemble, 20 members |

Each `.pt` file holds the weights of all members of an ensemble together with their normalization statistics and metadata, and can be read with `torch.load(path, weights_only=True)`.

## Usage

**Google Colab.** Click the badge above and run all cells (*Runtime → Run all*). The models are downloaded from this repository; no installation is needed.

**Locally.** Clone the repository and open the notebook in Jupyter:

```bash
git clone https://github.com/mfgerard/PSO_inverse_design.git
cd PSO_inverse_design
pip install torch numpy scipy pandas matplotlib jupyter
jupyter notebook PSO_inverse_design.ipynb
```

To read the models from the cloned folder instead of downloading them, set `MODELS_SOURCE = "."` in Section 2.1.

The design problem (target diameter, search variables, fixed parameters and bounds), the PSO hyperparameters and the fitness constants are set in Section 2 of the notebook. The defaults are the values used in the paper. The search runs in seconds on a CPU.

> The surrogates are only reliable inside the parameter ranges of the training set (Table 4 of the paper). Candidate designs should be confirmed by a CFD simulation or by experiment.

## Citation

If you use this notebook or the trained models, please cite the paper above.

## License

[MIT](LICENSE)
