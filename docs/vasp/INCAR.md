[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [VASP](index.md) :fontawesome-solid-angle-right: **INCAR**
# INCAR <a href="https://www.vasp.at/wiki/index.php/INCAR" class="md-button small-button">VASP Wiki</a>

This file is the main input file to tell VASP what to calculate and what settings you want VASP to use. There are a lot of different tags you can add and many tags affect multiple different settings.

Follow the link for a list of all INCAR tags: [Link](https://www.vasp.at/wiki/index.php/Category:INCAR_tag)

## Important INCAR Tags

### IBRION [:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/IBRION)

Tells VASP what method to do. 

* IBRION=0 is for Molecular Dynamics.
* IBRION=2 is for Conjugate Gradient Geometry Optimization. 
* IBRION=5 is for calculating finite differences for phonopy displacements.

### ISIF[:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/ISIF)

Tells VASP what constraints you want the calculation to have.

* ISIF = 2 is to optimize the atom positions with a fixed unit cell shape and volume.
* ISIF = 3 is to optimize the unit cell shape, volume and atom positions.
* ISIF = 4 is to optimize unit cell shape and atom positions with a fixed unit cell volume.
* ISIF = 7 is to optimize unit cell volume with a fixed shape and atom positions.

### PREC [:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/PREC)

Tells VASP how precise you want the calculation. It provides cut off energies, convergence criteria etc. The two main options are PREC = Normal or PREC = Accurate

### ENCUT [:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/ENCUT)

Defines the energy cutoff for the basis set used in the VASP calculation. This value is set by the PREC INCAR tag automatically but the VASP Wiki suggests you should manually set it anyway. The amount of ENCUT could determine if a calculation fully converges and finds a minima structure.


### NCORE [:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/NCORE) and NPAR [:fontawesome-solid-link:](https://www.vasp.at/wiki/index.php/NPAR) 

These tags are for parallelization of VASP. You need to use one or the other tag in the INCAR file.

* NCORE is equal to the number of cores per compute node. 

Or if you are using more than one node:

* NPAR is equal to the square root of the number of cores being used.

For 1 node jobs on Nocona:

***NCORE = number of ntasks/cpus requested in SLURM file. (I am not sure if this is right...)***


## Geometry Optimization INCAR

Below is a example INCAR file for Geometry Optimization.

``` title="INCAR"
SYSTEM = GEO OPT
NSW = 600
LREAL = A
IALGO = 48
ISMEAR = 0
IBRION = 2       #   ionic relax: 0-MD 1-quasi-New 2-CG, 5,6- freq.calc
ISIF = 2         #const. cell and volume, opt.ions
#ISIF = 3         #opt cell shape and volume and ions
#ISIF = 4         # opt cell shape and ions at const. volume
#ISIF = 7         # opt cell volume - fixed shape and ion pos.
NSIM = 1
ISYM=0
#ENCUT=350
#ENCUT=600
#PREC=High
#PREC=Accurate
PREC=Medium
#EDIFF = 1E-5
#EDIFFG = -0.015
#NPAR = 8
NCORE=4
#AMIN=0.02
#dispersion corrections D3
IVDW=12

```

Note: If a line is commented, VASP will not read it (Just like Bash and Python).


## Phonopy Displacement INCAR

Below is an example of the INCAR you would need to use for a phonopy displacement calculation using VASP.

``` title="INCAR"
SYSTEM = Phonopy
PREC = Accurate
ENCUT = 800 #obtained using ENCUT convergence TEST
IBRION = -1 #static calcs
ISIF = 2 #stress tensor and forces of atomic displacemnts. 1 DOF
EDIFF = 1E-5
ISMEAR = 0
SIGMA = 0.01 # Recommended
NSW = 0
LCHARG = .TRUE.
LWAVE = .TRUE.
NCORE = 4

```