# L4 model set up 

This is a water column model setup designed to explore the dynamics of different protist trophic strategies (autotrophy, mixotrophy, and heterotrophy) at the [L4 station in the Western English Channel](https://westernchannelobservatory.org.uk). The protist model is implemented in the [Framework for Aquatic Biogeochemical Models (FABM)](http://fabm.net) and further depends on the [European Regional Seas Ecosystem Model (ERSEM)](http://ersem.com). The simulation of 1D hydrodynamics and transport is handled by the [General Ocean Turbulence Model (GOTM)](https://gotm.net/).

The protist model is a development of previous works ([Flynn & Mitra 2009 J Plankton Res](https://doi.org/10.1093/plankt/fbp044), [Mitra et al. 2016 Protist](https://doi.org/10.1016/j.protis.2016.01.003))
and is described in full in [Leles et al 2018 J Plankton Res](https://doi.org/10.1093/plankt/fby044). 

## Obtaining the source code

### FABM

First obtain the FABM source code:

    git clone git@github.com:fabm-model/fabm.git <FABMDIR>

(Replace `<FABMDIR>` with the directory where the FABM code should go, e.g., ~/fabm.)

### ERSEM

First [register for access to the ERSEM source code](https://www.pml.ac.uk/Modelling_at_PML/Code_Registration).

After you receive an e-mail indicating that access to ERSEM was granted, obtain the source code:

    git clone git@gitlab.ecosystem-modelling.pml.ac.uk:stable/ersem.git <ERSEMDIR>
    cd <ERSEMDIR>
    git checkout faa6a31

(Replace `<ERSEMDIR>` with the directory where the ERSEM code shoulf go, e.g., ~/ersem.)

For the above command to succeed, you have to provide [the PML GitLab server](https://gitlab.ecosystem-modelling.pml.ac.uk/profile/keys) with your public SSH key. Alternatively, you can use HTTPS instead of SSH/GIT: replace the above URL (git@...) with https://gitlab.ecosystem-modelling.pml.ac.uk/stable/ERSEM.git.

### GOTM

Now obtain the latest (developers') version of the GOTM code:

    git clone git@github.com:gotm-model/code.git <GOTMDIR>
    cd <GOTMDIR>
    git checkout 1cd920

(Replace `<GOTMDIR>` with the directory where the GOTM code should go, e.g., ~/gotm.)

## Building

In addition to the source code (see previous section), you will need:

* a Fortran compiler, such as Intel Fortran 12.1 or higher or gfortran 4.7 or higher
* [cmake](http://www.cmake.org), version 3.0 or higher. First check whether you have that installed: execute `cmake --version` on the command line.

To build the model executable, you will need to create a build directory, call cmake to generate makefiles, then call make to compile and install. For instance:

    mkdir -p ~/build/gotm && cd ~/build/gotm
    cmake <GOTMDIR>/src -DFABM_BASE=<FABMDIR> -DFABM_ERSEM_BASE=<ERSEMDIR>
    make install

In the above, replace `<GOTMDIR>` with the directory with the GOTM source code, e.g., ~/gotm if you executed `git clone` in you home directory. Also, replace `<FABMDIR>` with the directory with the FABM code, e.g., ~/fabm and `<ERSEMDIR>` with the directory with the ERSEM code, e.g., ~/ersem.

Now you should have a GOTM executable with FABM and ERSEM support at `~/local/gotm/bin/gotm`.

## Performing a simulation

Open a terminal window in the current directory (the one that contains this README file), and run `~/local/gotm/bin/gotm`.

The model generates output in [NetCDF format](https://en.wikipedia.org/wiki/NetCDF), which can be read from many programs including Python, R and MATLAB. There is also a variety of viewer applications available, among which [PyNcView](https://github.com/BoldingBruggeman/pyncview).