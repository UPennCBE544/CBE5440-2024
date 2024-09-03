---
layout: page
mathjax: false 
permalink: /Clusters/
---

# Getting Started
We are going to set up our local terminals to do some practice with Python coding and introduce ASE

## Contents
1. [Installation](#installation)
2. [Logging On](#logging)
3. [First Time Logging On](#first-time)
4. [Making Sure Everything Works](#testing)

<a name='installation'></a>

## Installations
### Installing a display server:
#### Mac OSX
Download and install:

* [XQuartz](http://www.xquartz.org/)

#### Windows

Download and install:

* [PuTTY](http://www.putty.org/)
* [Xming](http://sourceforge.net/projects/xming/) (Note: disable automatic installation of PuTTY with Xming. The above installer is a newer version)

Launch Xming. You will always need to have this open in order to forward graphical windows from the external clusters.

### Installing Anaconda:
1. Go to this link: https://www.anaconda.com/download/success#downloads
2. Download the installer
3. Open the pkg and install

### Installing ASE:
In terminal: conda install conda-forge::ase
In terminal: conda install tk
Confirm ASE works by typing ase gui

### Installing GPAW (an example ASE calculator):
In terminal: python3 -m pip install gpaw

### Installing JupyterNotebook:
In terminal: jupyter notebook

<a name='logging'></a>

## Playing around with ASE
Download the ASE_Practice.ipynb() file and open in jupyter notebook. We will fill this out together.
 


