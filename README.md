# fgbias

Code for estimating CMB lensing biases, due to foregrounds, using simulations.

Given a "foreground-only" map, Schaan and Ferraro (https://arxiv.org/abs/1804.06403) introduce a 
quick way of estimating the bias to the CMB lensing power sepctrum (measured via a quadratic estimator),
which calculates the primary bispectrum, secondary bispectrum and trispectrum seperately and then sums. 
This package provides code to do this. 

# Dependencies

- [pixell](https://github.com/simonsobs/pixell/tree/master) (`pip install pixell`)
- [falafel](https://github.com/simonsobs/falafel/tree/master)
- [tempura](https://github.com/simonsobs/tempura/tree/main)

# Installation

git clone, then `cd fgbias` then `pip install .`

# Usage/examples

- See `examples/example1.ipynb` for basic usage.
- `examples/dr6_bias.ipynb` for a DR6-like example.

# To do
- Port over code for asymmetric estimators (e.g. "gradient-cleaned")
- MV estimator biases (pretty straightforward to get from the TT biases though)
- Add a galaxy cross-correlation example

# Caveats

There are some subtleties in estimating foreground biases that are difficult to account for within such a framework e.g.
- Masking/inpainting of sources and clusters is often performed to mitigate foregrounds. The mask can be correlated with the lensing
  convergence (see https://arxiv.org/abs/2109.13911), which can impart a bias that is not included in the estimates here. 
- As part of foreground mitigation, you may have applied source/cluster model subtraction to the foreground-only map. But these models
may have been inferred from maps containing CMB + noise (to ensure realistic performance) in which case they will contain residuals related
to the value of the CMB + noise at the source/cluster locations. These residuals would then be subtracted from the "foreground-only" map,
and could impart some additional bias.
- Relatedly, a survey mask may have been applied to the simulations to ensure realism of the simulation. This would introduce a mean-field
  to the foregound-bias estimate that may need to be estimated using simulations. If foregrounds are small, it may well be negligible.
