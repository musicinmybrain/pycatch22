# _pycatch22_ - CAnonical Time-series CHaracteristics in python

## About

[_catch22_](https://github.com/DynamicsAndNeuralSystems/catch22) is a collection of 22 time-series features coded in C that can be run from Python, as well as [R](https://github.com/hendersontrent/Rcatch22), [Matlab](https://github.com/DynamicsAndNeuralSystems/catch22), and [Julia](https://github.com/brendanjohnharris/Catch22.jl).

This package provides a python implementation as the module _pycatch22_.

### What do the features do?

This [GitBooks website](https://feature-based-time-series-analys.gitbook.io/catch22-features/) is dedicated to describing the features. For code implementation, see the [main _catch22_ repository](https://github.com/DynamicsAndNeuralSystems/catch22).
There is also information in the paper [&#x1F4D7; Lubba et al. (2019). _catch22_: CAnonical Time-series CHaracteristics](https://doi.org/10.1007/s10618-019-00647-x).

## Installation

Using `pip` for [`pycatch22`](https://pypi.org/project/pycatch22/):

```
pip install pycatch22
```

If this doesn't work, make sure you are using the latest `setuptools`: `pip install setuptools --upgrade`.

If you come across errors with version resolution, you should try something like: `pip install pycatch22==0.4.2 --use-deprecated=legacy-resolver`.

It is also a [package on anaconda](https://anaconda.org/conda-forge/pycatch22) thanks to [@rpanai](https://github.com/rpanai), which you can install via `conda`:

```
conda install -c conda-forge pycatch22
```

or `mamba`:

```
mamba install -c conda-forge pycatch22
```

[A manual install (bottom of this page) is a last resort.]

## Testing

```
python3 tests/testing.py
```

If `pycatch22` is installed correctly, this should output results for 24 features for each of two test time series.

## Usage

Each feature function can be accessed individually and takes arrays as tuple or lists (not `numpy` arrays).
For example, for loaded data `tsData` in Python:

```python3
import pycatch22
tsData = [1,2,4,3] # (or more interesting data!)
pycatch22.CO_f1ecac(tsData)
```

All features are bundled in the method `catch22_all`, which also accepts `numpy` arrays and gives back a dictionary containing the entries `catch22_all['names']` for feature names and `catch22_all['values']` for feature outputs.

Usage (computing 22 features: catch22):

```python3
pycatch22.catch22_all(tsData)
```

Usage (computing 24 features: catch24 = catch22 + mean + standard deviation):

```python3
pycatch22.catch22_all(tsData,catch24=True)
```

### Template analysis script

Thanks to @jmoo2880 for putting together a [demonstration notebook](https://github.com/jmoo2880/c22-usage-examples/) for using pycatch22 to extract features from a time-series dataset.

### Usage notes

- When presenting results using _catch22_, you must identify the version used to allow clear reproduction of your results. For example, `CO_f1ecac` was altered from an integer-valued output to a linearly interpolated real-valued output from v0.3.
- __Important Note:__ _catch22_ features only evaluate _dynamical_ properties of time series and do not respond to basic differences in the location (e.g., mean) or spread (e.g., variance).
  - From _catch22_ v0.3, If the location and spread of the raw time-series distribution may be important for your application, we suggest applying the function argument `catch24 = True` to your call to the _catch22_ function in the language of your choice.
  This will result in 24 features being calculated: the _catch22_ features in addition to mean and standard deviation.

### Manual install

If you find issues with the `pip` install, you can also install using `setuptools`:

```
python3 setup.py build
python3 setup.py install
```
