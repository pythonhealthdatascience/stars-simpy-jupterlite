[![lite-badge](https://jupyterlite.rtfd.io/en/latest/_static/badge.svg)](https://pythonhealthdatascience.github.io/stars-simpy-jupterlite/notebooks/?path=01_urgent_care_model.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/release/python-3100/)
[![License: MIT](https://img.shields.io/badge/ORCID-0000--0001--5274--5037-brightgreen)](https://orcid.org/0000-0001-5274-5037)
[![License: MIT](https://img.shields.io/badge/ORCID-0000--0003--2631--4481-brightgreen)](https://orcid.org/0000-0003-2631-4481)

#  Towards Sharing Tools and Artifacts for **Reproducible** Simulation **(v1.5)**: a JuypterLite template for `simpy` models

## Overview

The materials and methods in this repository support work towards developing the S.T.A.R.S healthcare framework version 1.5 (**S**haring **T**ools and **A**rtifacts for **R**eproducible **S**imulations in healthcare).  The code and written materials here are a work in progress to demonstrate the application of S.T.A.R.S' version to sharing a `simpy` discrete-event simuilation model and associated research artifacts. 

The model will run on a users browser without the need to install any components.  This is achieved using Web Assembly technology i.e. [JupterLite](https://github.com/jupyterlite/jupyterlite) and [xeus-python](https://github.com/jupyter-xeus/xeus-python).  A model notebook is downloaded to the users local machine and all dependencies are pre-installed via conda-forge. The model then lives in the browsers cache. The user can make changes to the model or create new files and these are persisted (until the browser cache is cleared).  

### Use case

* A researcher wishes to share a runnable version of a simulation model with their publication (e.g. written in `simpy`).  The code allows others to replicate the simulation results, tables and charts in a paper and allows others to reuse the model.
* The researcher wants the model to be immediately usable. Users should not need to install python, `simpy` or any dependencies.
* The researcher either wants to reduce load on online open science compute infrastructure (e.g. mybinder.org) or does not want to rely on it. 
* Users may want to use a version of their own data due to governance, ethics or other reasons cannot upload this to a remote instance of the model.
* Loading the model is as simple as clicking a URL.

### Credits ✨

We would like to thank the [JupterLite](https://github.com/jupyterlite/jupyterlite) and [xeus-python](https://github.com/jupyter-xeus/xeus-python) developers for making this work possible. This discrete-event simulation focussed repository was based on the learning materials and template provided by [Jupyterlite xeus-python demo](https://github.com/jupyterlite/xeus-python-demo) and [tutorial given at PyData 2023](https://www.youtube.com/watch?v=WXRslU9D3bo) by Jeremy Tuloup.

## ✨ Try it in your browser ✨

https://jupyterlite.github.io/xeus-python-demo/notebooks/?path=demo.ipynb

## ≠ How does it compare to the Pyodide kernel?

#### Pyodide kernel:

- Is based on [Pyodide](https://github.com/pyodide/pyodide)
- Uses [IPython](https://github.com/ipython/ipython) for the code execution (access to IPython magics, support for the inline Matplotlib backend, *etc*)
- Provides a way to dynamically install packages with ``piplite`` (**e.g.** ``await piplite.install("ipywidgets")``)
- **Does not support** sleeping with ``from time import sleep``
- **Does not support** pre-installing packages

#### jupyterlite-xeus-python:

- Is based on [xeus-python](https://github.com/jupyter-xeus/xeus-python)
- Uses [IPython](https://github.com/ipython/ipython) for the code execution (access to IPython magics, support for the inline Matplotlib backend, *etc*)
- **Does not provide** a way to dynamically install packages (yet. We are working on building a ``mamba`` package manager for WASM)
- **Supports** sleeping with ``from time import sleep``
- **Supports** pre-installing packages from ``emscripten-forge`` and ``conda-forge``, by providing an ``environment.yml`` file defining the runtime environment

## 💡 How to make your own deployment

![Deploy your own](deploy.gif)

Then your site will be published under https://{USERNAME}.github.io/{DEMO_REPO_NAME}

## 📦 How to install extra packages

You can pre-install extra packages for xeus-python by adding them to the ``environment.yml`` file.

For example, if you want to create a JupyterLite deployment with NumPy and Matplotlib pre-installed, you would need to edit the ``environment.yml`` file as following:

```yml
name: xeus-python-kernel
channels:
  - https://repo.mamba.pm/emscripten-forge
  - conda-forge
dependencies:
  - xeus-python
  - numpy
  - matplotlib
```

Only ``no-arch`` packages from ``conda-forge`` and packages from ``emscripten-forge`` can be installed.
- **How do I know if a package is ``no-arch`` on ``conda-forge``?** ``no-arch`` means that the package is OS-independent, usually pure-python packages are ``no-arch``. To check if your package is ``no-arch`` on ``conda-forge``, check if the "Platform" entry is "no-arch" in the https://beta.mamba.pm/channels/conda-forge?tab=packages page. If your package is not ``no-arch`` but is a pure Python package, then you should probably update the feedstock to turn your package into a ``no-arch`` one.
![](noarch.png)
- **How do I know if my package is on ``emscripten-forge``?** You can see the list of packages pubished on ``emscripten-forge`` [here](https://beta.mamba.pm/channels/emscripten-forge?tab=packages). In case your package is missing, or it's not up-to-date, feel free to open an issue or a PR on https://github.com/emscripten-forge/recipes.
