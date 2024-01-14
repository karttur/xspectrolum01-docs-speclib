---
layout: post
title: "Spectral library setup: 3. python package db_setup"
categories: "speclib-setup"
excerpt: "Setup of the xspectrolum spectral system; part 3: access and setup the python package db_setup"
tags:
  - spectral library
  - postgres
  - postgresql
image: ts-mdsl-rntwi_RNTWI_id_2001-2016_AS
date: '2023-07-17 11:27'
modified: '2023-07-17 T18:17:25.000Z'
comments: true
share: true
---

## Introduction

In this post you will access a [GitHub](https://github.com) repo with a python package that is prepared for defining the xspectrolum spectral system. Once you have the python package restored on your local machine you can setup the complete database, including some default records, by running the script.

## Prerequisits

To follow these instructions in detail you must have [Anaconda](https://www.anaconda.com/), [Eclipse](https://www.eclipse.org) and [PostgreSQL](https://www.postgresql.org/) installed and setup as outlined in the two previous posts ([app installation](../speclib-setup_01appinstall) and [app setup](../speclib-setup_01appsetup)).

## Python package - setup_db

The python package for setting up the xspectrolum spectral system postgreSQL database is available at [https://github.com/karttur/xspectrolum01-setup_db](https://github.com/karttur/xspectrolum01-setup_db). Click the link (or write the url string in your browser) and you will see the front page for the repo.

<figure>
<img src="../../images/xspectrolum01-setup_db_01githubrepo.png">
<figcaption>xspectrolum01-setup_db repo on GitHub</figcaption>
</figure>

### Clone or download repo

You have (at least) four options for accessing the python package [xspectrolum01-setup_db](https://github.com/karttur/xspectrolum01-setup_db):

1. Download as a stand alone package,
2. Clone directly into Eclipse,
3. Clone as a stand alone git repo, or
4. Fork and then clone the git repo

Which route to take depends on your objectives; if you just want to run the script chose one of the first two, if you want to participate in the development or develop your own version of the package, chose one of the latter two.

#### Download as a stand alone package

if you are not familiar with git and repos this is probably the easiest path. In the repo, click the green button <span class='button'>code</span> and select <span 'textfield'>Download ZIP</span>

<figure>
<img src="../../images/xspectrolum01-setup_db_02downloadzip.png">
<figcaption>Access the python package xspectrolum01-setup_db from GitHub by simple downloading.</figcaption>
</figure>

The complete package is downloaded as a zipfile to your local computer. Expand it, rename it to _setup_db_ and import it to Eclipse.

#### Clone directly into Eclipse

TO BE COMPLETED

#### Clone as a stand alone git repo

TO BE COMPLETED

#### Fork and then clone the git repo

TO BE COMPLETED
