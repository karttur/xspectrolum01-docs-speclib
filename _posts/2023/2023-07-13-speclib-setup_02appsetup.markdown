---
layout: post
title: "Spectral system setup: 2. App setup"
categories: "xspectrolum-setup"
excerpt: "Setup of the xspectrolum spectral processing system; part 2: Setup applications"
tags:
  - spectral library
  - postgres
  - postgresql
image: ts-mdsl-rntwi_RNTWI_id_2001-2016_AS
date: '2023-07-13 11:27'
modified: '2024-01-13 T15:57:25.000Z'
comments: true
share: true
---

## Introduction

In the [previous post](../speclib-setup_01appinstall) you installed the applications required for managing and running the xspectrolum spectral processing system on your local machine. In this post you will setup the applications with required customizations to fit the spectral processing system.

## Prerequisits

To follow these instructions in detail you must have installed [Anaconda](https://www.anaconda.com/), [Eclipse](https://www.eclipse.org) and [PostgreSQL](https://www.postgresql.org/) as outlined in the [previous post](../speclib-setup_01appinstall).

## Setup Anaconda, Eclipse and PostgreSQL

This section only contains the particular details for setting up Anaconda, Eclipse and PostgresSQL that differs from the general instructions found in the blog on [Install and setup Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/).

### Anaconda virtual python environment

Create a python virtual environment (for details see the blog-post on [Python virtual environments](https://karttur.github.io/geoimagine03-docs-main/prep/prep-conda-environ/)).

The python packages that are needed and available through <span class='terminalapp'>conda</span> channels include:

- numpy,
- pandas,
- scikit-learn,
- psycopg2, and
- requests.

You should preferably install them with the basic Python installation. <span class='terminalapp'>Conda</span> will then look for conflicts and resolve coherence between versions. You can also install the packages after you have created the base package but that is not the preferred route. If your <span class='terminalapp'>conda</span> installation is setup with default packages you need to include the <span class='terminalapp'>–-no-default-packages</span> key if you do not want the default packages installed with the new virtual environment.

NOTE that in July 2023 <span class='terminalapp'>conda</span> did not accept the command:

<span class='terminal'>$ conda create –-no-default-packages --name xspectralib_py38 python=3.8 numpy pandas scikit-learn psycopg2 requests</span>

There seems to be a problem with command _–-no-default-packages_. Thus you must either accept the default packages, or temporary remove or rename the hidden file <span class='file'>.condarc</span> in your home directory that defines the default packages. Then rerun the <span class='terminalapp'>conda</span> command:

<span class='terminal'>$ conda create --name xspectralib_py38 python=3.8 numpy pandas scikit-learn psycopg2 requests</span>

And for me this solved the issues and <span class='terminalapp'>conda</span> setup the requested virtual environment.

#### Install additional conda packages

Instead of installing <span class='terminalapp'>conda</span> packages with the initial creation, you can add them as separate packages afterwards. Just make sure that you are in the correct environment or define the right environment explicitly.

<span class='terminal'>$ conda activate xspectralib_py38</span>

If your active environment is the target for the installation:

<span class='terminal'>$ conda install psycopg2</span>

<span class='terminal'>$ conda install -c anaconda requests</span>

If you are in the base environment:

<span class='terminal'>$ conda install --name xspectralib_py38 psycopg2</span>

<span class='terminal'>$ conda install --name xspectralib_py38 -c anaconda requests</span>

#### Additional pypi packages

Some of the python packages required for the spectral library processing are only available as pypi installations. These packages must be installed posterior.

##### jcamp

[jcamp](https://pypi.org/project/jcamp/) is a package for reading JCAMP-DX format spectral data files.

At time of writing this in July 2023, [jcamp](https://pypi.org/project/jcamp/) is not available at any conda channel. To test if it has become avaliable in the meantime, use <span class='terminalapp'>conda</span> to search for the package:

<span class='terminal'>$ conda search jcamp</span>

If [jcamp](https://pypi.org/project/jcamp/) is available install it using <span class='terminalapp'>conda</span> as instructed, otherwise you need to use the <span class='terminalapp'>pip</span> installation manager. Remember to active the target environment,

<span class='terminal'>$ conda activate xspectralib_py38/span>

and then use <span class='terminalapp'>pip install</span>

<span class='terminal'>$ pip install jcamp</span>

### Eclipse for PyDev

With the virtual environment defined you can setup [Eclipse](https://www.eclipse.org) for PyDev with this environment. Just follow the steps outlined in the post [Setup Eclipse for PyDev](https://karttur.github.io/setup-ide/setup-ide/install-eclipse/) but replace the virtual environment with the one you just created.

### PostgreSQL

Follow the online instructions in my post on [Install postgreSQL and postGIS](https://karttur.github.io/setup-ide/setup-ide/install-postgres/). I recommend that you also install one of the graphical interfaces for inspecting the postgreSQL database. Remember that you have to set a role (user) and give that role in a <span class='file'>.netrc</span> file if you want to follow the rest of this blog in its details.
