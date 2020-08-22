---
layout: default
title: Maintaining YoWASP
---

## Maintaining YoWASP

This document describes the process used to modify, update, test, and release YoWASP packages. It is not useful to users of YoWASP, though it might be informative if you want to reproduce YoWASP's approach for some other software.

### Building and testing locally

YoWASP packages are developed on a Linux system.

All YoWASP repositories use an unified approach for building and packaging. Let's use Yosys as an example. Check out the repository:

```
git clone --recurse-submodules git@github.com:YoWASP/yosys
cd yosys
```

Download any necessary dependencies and build the WASM binaries:

```
./build.sh
```

Build the Python packages for PyPI:

```
rm -rf py-env && python3 -m venv py-env
. py-env/bin/activate
pip install setuptools_scm
./package-pypi.sh
```

Install the binary wheels directly and test their functionality:

```
pip install pypi/dist/*.whl
yowasp-yosys --help
```

Alternatively, serve and install them from a local PyPI index:

```
pip install pypiserver
pypi-server .
pip install -i http://localhost:8080/simple yowasp-yosys
```

### Releasing packages

All packages uploaded to the package repositories are produced without manual intervention using GitHub Actions. To produce a new build, simply push to the `develop` branch, or merge a pull request into it:

```
git push origin develop
```

This will build packages in a clean environment and upload the Python wheels to [Test PyPI](https://test.pypi.org). They can be installed directly from Test PyPI:

```
pip install -i https://test.pypi.org/simple yowasp-yosys
```

Once the packages are verified to work correctly, advance the `release` branch to the `develop` branch:

```
git push origin develop:release
```

Branch protection ensures that the history remains linear (which is important for the automatic versioning to work) and that the `release` branch can only point to commits which successfully build and pass tests.

### Maintenance automation

Every day, the `develop` branch is automatically updated with the latest upstream code. The update is pushed directly to the branch, so this can actually break the build.

Every week, a pull request from the `develop` branch to the `release` branch is automatically created if it does not already exist. This allows a last-minute human review of any packages that are pushed to PyPI while ensuring that keeping the PyPI packages up to date is as easy as clicking a single button.
