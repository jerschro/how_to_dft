[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 4331](index.md) :fontawesome-solid-angle-right: **Assignment 1**
# Assignment 1 - Linux Intro and Turbomole Test Calculations

Made for use in ME 4331.

## Task 1 - Make your account public

* Listen to the commands Jeremy will give during the meeting and run them.

``` bash
bash /home/jerschro/Scripts/chmod/fix_chmod.sh
```

    * This is a bandaid to the issue of not everyone being in the same group but it works.

## Task 2 - Add Turbomole .bashrc information.

* Copy the text below to your .bashrc file. You may also want to add the aliases listed [here](../hpcc/bashrc_file.md). When added, run the command ```source .bashrc```.

``` bash
export TURBODIR=/home/aaquino/Programs/TURBOMOLE

source $TURBODIR/Config_turbo_env

export PATH=$TURBODIR/scripts:$PATH
export PATH=$TURBODIR/bin/`sysname`:$PATH
``` 

## Task 3 - Copy Test Calculations from Jeremy's Directory

* Create 3 directories names ```test_opt```, ```test_solv```, &```test_freq```.

* Copy the Turbomole input files from each directory in this path ```/home/jerschro/UG/test_calculations/``` into each directory you just created respectively.

## Task 4 - Run each test calculation

* Navigate into each test calculation directory and run this command ```sbatch run_turbomole.sh```.

## Task 5 - Check to see if calculations finished correctly

* For ```test_opt``` and ```test_solv```, see if the files ```converged``` , ```GEO_OPT_CONVERGED``` and ```job.last``` exists. This means the optimization and solvent calculation finished correctly.

* For ```test_freq```, see if the files ```freq.out``` , ```vib_normal_modes``` and ```vibspectrum``` exists. This means the frequency calculation finished correctly.

## Task 6 - Create directory structure for DNA molecules

* Create the file structure described below:
    * (You can name the DNA_molecule folder what DNA molecule you have been assigned.)


```
home
|
└── DNA_molecule
    |
    ├── gas
    |   |
    |   └── opt
    |   |
    |   └── solvent
    |
    └──freq
```



## Task 7 - Install Conda

* Follow the instructions [here](../hpcc/install_conda.md). You need a local conda installation for next week.

## Task 8 - Done!

* We will get started with the DNA molecule calculations next week. Good Work!