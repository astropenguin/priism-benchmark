# priism-benchmark
Python 3 environment for benchmarking PRIISM


## Usage

### Install [Poetry]

This repository manages dependent Python packages by [Poetry].
Please install it to your environment if you do not have it.

```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
```

### Clone this repository

```bash
git clone https://github.com/astropenguin/priism-benchmark.git
```

### Install Python dependencies

This will create a virtual environment and install the dependencies on it.

```bash
cd priism-benchmark
poetry install
```

### Download the HL Tau SV data

This will download the data in `path/to/repository/data`:

```bash
bin/download-hltau
```

### Run benchmark

This will create output FITS images and a log file in `/path/to/repository/log`:

```bash
poetry run bin/benchmark priism-0.7.15,priism-0.7.16 32,64
```

where the first argument should be comma-separated PRIISM versions (i.e. tag or commit ref.) and the second argument should be comma-separated `OMP_NUM_THERADS`s.

The format of the output log file (`/path/to/repository/benchmark.log`) contains comma-separated values:

```plaintext
priism-0.7.15,32,113.62
priism-0.7.15,64,144.67
priism-0.7.16,32,97.42
priism-0.7.16,64,106.51
```

where the first, second, and third columns correspond to the PRIISM version, `OMP_NUM_THREADS`, and the elapsed time for `imager.solve(...)`, respectively.

### PRIISM build options

PRIISM build options can be specified by an environment variable `PRIISM_BUILD_OPTIONS`:

```bash
PRIISM_BUILD_OPTIONS="-X yes" poetry run bin/benchmark priism-0.7.15,priism-0.7.16 8,32,64
```

[Poetry]: https://python-poetry.org/
