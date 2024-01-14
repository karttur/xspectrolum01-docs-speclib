---
layout: post
title: "Spectral system setup: 1. App installation"
categories: "xspectrolum-setup"
excerpt: "Setup of the xspectrolum spectral processing system; part 1: install required applications"
tags:
  - spectral processing system
  - installation
  - postgresql
  - anaconda
  - eclipse
image: ts-mdsl-rntwi_RNTWI_id_2001-2016_AS
date: '2023-07-01 11:27'
modified: '2024-01-13 T15:17:25.000Z'
comments: true
share: true
---

## Introduction

The xspectrolum spectral system is a processing environment for spectral data built around xSpectre's [spectrometer<b>+</b>](https://www.environimagine.com/spectrometerv080.html). The spectral system includes specific processing for the spectrometer<b>+</b> but can also import and process spectra from other sensors and open datasets. The database holding all the spectral data is partly modelled after the [Open Soil Spectral Library (OSSL)](https://soilspectroscopy.org) database. But whereas the OSSL database is a document based MongoDB, the xspectrolum database is a relational postgreSQL database.

This post covers the installation of the applications required for defining, managing and using the xspectrolum spectral system postgreSQL database on your local machine. The next post covers the customized setup to prepare the installed apps for use with the xspectrolum database.

If you interest is mainly spectral data, spectral databases and modeling physico-chemical properties from spectral data, my blog on [Soil spectral libraries](https://karttur.github.io/soil-spectro/) is a better starting place.

## Prerequisits

To follow this post you do not need any prior installations. The post is written for MacOS. If you use Linux you can use my blog post [SPIDE for Ubuntu 18.04](https://karttur.github.io/setup-ide/blog/ubuntu-setup-spide/). If you are a windows user you need to check the documentation of each app for differences in the syntax.

## Applications

This shorthand instructions covers the installation of the following applications:

- [Anaconda](https://www.anaconda.com/)
- [Eclipse](https://www.eclipse.org)
- [PostgreSQL](https://www.postgresql.org/)

### Anaconda

[Anaconda](https://www.anaconda.com/) is a free platform for scientific Python and is used for defining the virtual python environment for the xspectrolum spectral system. Installation and setup is covered in the post [Install Anaconda](https://karttur.github.io/setup-ide/setup-ide/install-anaconda/) in my blog on [Install and setup Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/). The virtual environment required for the xspectrolum spectral system setup differs compared to these instructions. This is covered in the [next post](../speclib-setup_02appsetup/).

### Eclipse

[Eclipse](https://www.eclipse.org) is a general application for developing scripts and applications, or an Integrated Development Environment (IDE). Installation and setup is covered in the post [Setup Eclipse for PyDev](https://karttur.github.io/setup-ide/setup-ide/install-eclipse/) in my blog on [Install and setup Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/). The only difference compared to the published instructions is the definition of the virtual environment (i.e. defined using Anaconda), which is covered in the [next post](../speclib-setup_02appsetup/).

### PostgreSQL

[PostgreSQL](https://www.postgresql.org/) (or postgres for short) is an advanced open source object-relational database system. Installation and setup is covered in the post [Install postgreSQL and postGIS](https://karttur.github.io/setup-ide/setup-ide/install-postgres/) in my blog on [Install and setup Spatial Data Integrated Development Environment (SPIDE)](https://karttur.github.io/setup-ide/). The instructions include setting up a default user (role) with a password and how to save the password using a <span class= 'file'>.netrc</span> file. The following posts in this blog assumes that you have setup postgreSQL with that solution. Details for defining the role (user) for accessing the full postgreSQL database is in the [next post](../speclib-setup_02appsetup/).
