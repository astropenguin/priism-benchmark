# priism-benchmark
Python 3 environment for benchmarking PRIISM


## Usage

### Install [Poetry]

This repository manages dependent Python packages by [Poetry].
Please install it to your environment if you do not have it.

```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
```

### Clone this repository and install dependencies

This will create a virtual environment and install the dependencies on it.

```bash
git clone https://github.com/astropenguin/priism-benchmark.git
cd priism-benchmark
poetry install
```

### Run benchmark (HL Tau)

This will download the HL Tau SV data and run SpM imaging with multiple PRIISM versions and numbers of threads:

```bash
poetry run bin/hltau/benchmark priism-0.7.15,priism-0.7.16 32,64
```

where the first argument should be comma-separated PRIISM versions (i.e. tag or commit ref.) and the second argument should be comma-separated `OMP_NUM_THERADS`s.

Output FITS images and a log file will be put in `/path/to/repository/log/hltau`.
The format of the log file (`benchmark.csv`) is like:

```plaintext
PRIISM version,Number of threads,Elapsed time (s)
priism-0.7.15,32,113.62
priism-0.7.15,64,144.67
priism-0.7.16,32,97.42
priism-0.7.16,64,106.51
```

where the first, second, and third columns correspond to the PRIISM version, the number of threads used for imaging, and the elapsed time (in seconds) of imaging (i.e. `imager.solve(...)`), respectively.

### PRIISM build options

PRIISM build options can be specified by an environment variable `PRIISM_BUILD_OPTIONS`:

```bash
PRIISM_BUILD_OPTIONS="-X yes" poetry run bin/hltau/benchmark priism-0.7.15,priism-0.7.16 8,32,64
```

[Poetry]: https://python-poetry.org/
