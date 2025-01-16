# Custom Pandas Wheels

Pandas 1.5.3 does not provide pre-built wheels for Python 3.12. PandasAI library has strict dependency on Pandas 1.5.3.

When building image for Python 3.12, the Pandas package is compiled from source, leading to build time exceeding 10 minutes.

Here, we will pre-build wheels for pandas 1.5.3 compatible with Python 3.12.7

## How to create new wheel?

### Using Docker
```shell
# Use an official Python image with a Linux environment to build the wheel.
docker run --rm -it -v "$(pwd):/src" python:3.12.7-slim bash

# Install Build Tools in Docker
apt-get update && apt-get install -y build-essential python3-dev
pip install --upgrade pip setuptools wheel

# Build the Wheel
# # pinning numpy for pandas compatibility https://stackoverflow.com/a/78641304/25470373 https://github.com/pandas-dev/pandas/blob/main/requirements-dev.txt#L17C1-L17C8
pip wheel --wheel-dir=./pandas_wheels pandas==1.5.3 "numpy<2"

# copy pandas_wheels from container to ./pandas_wheels/ directory

exit
```
