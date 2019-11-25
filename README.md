This is a FABM (Fortran) code to model different protist functional types.                                    
This model is a development of previous works (Flynn & Mitra 2009 J Plankton Res, Mitra et al. 2016 Protist)  
and is described in full in Leles et al 2018 J Plankton Res.                                                 
                                                                                                             
Note that the code requires external dependencies from ERSEM, which can be obtained upon registration at:              
http://www.shelfseasmodelling.org                                                                            


# Obtaining the code and building 
## Linux

First obtain the FABM source code:

    git clone git://git.code.sf.net/p/fabm/code <FABMDIR>

(Replace `<FABMDIR>` with the directory with the FABM code, e.g., ~/fabm-git.)

Obtain the ERSEM code for FABM:

    git clone git@gitlab.ecosystem-modelling.pml.ac.uk:stable/ersem.git <ERSEMDIR>

(Replace `<ERSEMDIR>` with the directory with the ERSEM code, e.g., ~/ersem-git.) Note that for this to work, you have to provide [the PML GitLab server](https://gitlab.ecosystem-modelling.pml.ac.uk/profile/keys) with your public SSH key.

FABM and ERSEM use object-oriented Fortran and therefore require a recent Fortran compiler, such as Intel Fortran 12.1 or higher and gfortran 4.7 or higher. Compilation is regularly tested with Intel Fortran 12.1, 13.0 and 14.0. as well as gfortran 4.7, 4.8 and 4.9.

FABM and ERSEM use a platform-independent build system based on [cmake](http://www.cmake.org). You'll need version 2.8.8 or higher. First check whether you have that installed: execute `cmake --version` on the command line.

### GOTM + FABM + ERSEM

First obtain the latest (developers') version of the GOTM code from its git repository:

    git clone https://github.com/gotm-model/code.git gotm-git

To build GOTM with FABM support, create a build directory, call cmake to generate makefiles, and make to compile and install. For instance:

    mkdir -p ~/build/gotm && cd ~/build/gotm
    cmake <GOTMDIR>/src -DFABM_BASE=<FABMDIR> -DFABM_ERSEM_BASE=<ERSEMDIR>
    make install

In the above, replace `<GOTMDIR>` with the directory with the GOTM source code, e.g., ~/gotm-git if you executed `git clone` in you home directory. Also, replace `<FABMDIR>` with the directory with the FABM code, e.g., ~/fabm-git and `<ERSEMDIR>` with the directory with the ERSEM code, e.g., ~/ersem-git.

Now you should have a GOTM executable with FABM and ERSEM support at `~/local/gotm/bin/gotm`.

It is good practice to keep up to date with the latest code from the ERSEM, FABM and GOTM repositories by regularly executing `git pull` in a directory of each repository.

If either the ERSEM, FABM or GOTM source codes change (e.g., because changes you made to the code yourself, or after `git pull`), you will need to recompile. This does NOT require rerunning cmake. Instead, you need to return to the build directory and rerun `make install`. For instance `cd ~/build/gotm && make install`.
