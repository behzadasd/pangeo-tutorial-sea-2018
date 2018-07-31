Getting Started with Pangeo
===============

This notebooks in this tutorial are designed to run on the Cheyenne High-Performance Computer, Pangeo's JupyterHub deployed on Google Compute Platform, or on a local computer (see Running Locally below). Most of the datasets used in the tutorial are small and are packaged with xarray. The larger sample datasets may only be available on GCP and/or Cheyenne.

## Setup Python for working on a personal computer or on Cheyenne

#### Download Miniconda

    # for linux
    $ wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh

    # for osx
    $ wget https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -O miniconda.sh

    # for windows
    # go to: https://conda.io/miniconda.html

#### Install Miniconda

    $ bash miniconda.sh
    # follow instructions

#### Clone the tutorial repository

    $ git clone https://github.com/NCAR/pangeo-tutorial-august-2018
    $ cd pangeo-tutorial-august-2018
    
#### Install Pangeo Environment

*This step can take some time.  If it fails, just run it again and it will pick up where it left off.*

    $ conda env create --file environment.yml

#### Activate the Pangeo Environment

    $ source activate pangeo

#### Install the necessary Jupyter Plugins

    $ jupyter labextension install jupyterlab_bokeh

#### Run a quick test

    $ python

    >>> import xarray as xr
    >>> xr.show_versions()  
    >>> xr.tutorial.load_dataset('air_temperature')
    >>> xr.tutorial.load_dataset('rasm')


## Launching Jupyter locally

    $ jupyter lab

## Launching Jupyter and Dask on Cheyenne

  1. Install dask-jobqueue

         $ pip install git+https://github.com/dask/dask-jobqueue.git

  1. Launching jupyter lab requires a few extra steps (on Cheyenne)

         $ export PBS_ACCOUNT=STDD0006
         $ qinteractive -l walltime=4:00:00
         $ export LD_LIBRARY_PATH=
         $ source activate pangeo
         $ start-notebook
         
  1. Run the ssh command returned by `start-notebook` on your local computer, and then open up `localhost:8888` in your browser
  
  1. Once you start the `distributed` cluster, you can create another ssh tunnel to the Dashboard.

## Access to Pangeo on Google Cloud

We are running a JupyterHub on Google Compute Platform. To access this service:
  - Go to http://pangeo.pydata.org/
  - Authenticate with your GitHub Account. If you don't have a Github Account, go here first: https://github.com/join
  - Open a new terminal using the jupyer lab interface
  - Clone this repository

        git clone https://github.com/pangeo-data/pangeo-tutorial-sea-2018.git tutorial

  - The base conda environment has most of what we need but you may want to add a few packages, from within your terminal, run:

        conda install -c conda-forge cartopy holoviews geoviews graphviz=2.38.0 xorg-libxrender xorg-libxpm
        jupyter labextension install jupyterlab_bokeh
