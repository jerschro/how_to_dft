---
hide:
  - navigation
---
[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: **Gaussian**
# Gaussian

This is the webpage for containing everything to do with Gaussian.

Gaussian was one of the first quantum chemistry programs released (Gaussian 70) and it is still a very popular DFT program today. The most latest version of Gaussian is Gaussian 16 (released in 2016). To use Gaussian on the TTU HPCC, it is important you are on the our research group's Gaussian License, as Gaussian is a proprietary software.

## Gaussian Documentation

Gaussian has a documentation manual and you can use the search function to find more information on topics. It is very detailed and will help with determining input parameters. You can also google the topic with Gaussian 16 for example "basis sets Gaussian 16" and one of the top results will be a webpage from [gaussian.com](https://gaussian.com/) which is the Gaussian 16 documentation.

* [Gaussian 16 Manual](https://gaussian.com/man/)

## Gaussian Input Files

The initial files required for Gaussian are:

* input.gjf 
    * The filename doesn't actually matter, but input.gjf will be used from here on out as a consistent input filename.
* SLURM file
* initial coordinates in .xyz format (optional because you can supply coordinates in input.gjf).

## input.gjf

The input.gjf file is the main input file for Gaussian. The first line is the input line that will contain all of the calculation settings you want Gaussian to do that starts with "#p". Gaussian is not case sensitive.

Below the input line, you supply two integers and then the .xyz coordinates below the two integers or the .xyz filename with an @ before the filename. The first integer is the molecular charge of the system. The second integer is the multiplicity of the system. The multiplicity of the system is almost always 1 if the charge is 0 for a molecule that has the correct charge and is a closed shell system. The multiplicity describes the amount of possible spin states in the system and it is defined as $2S + 1$ where $S$ is the total spin quantum number. For a closed shell system, the multplicity is 1 also called a singlet and for example an unpaired electron has a doublet spin or multiplicity of 2.

## Example input.gjf

The below input.gjf file will run a DFT geometry optimization and a frequency calculation with PBE functional and SVP basis set.

``` title="input.gjf"
%chk=gaussian.chk
#p PBE/SVP Opt Freq

Title Card - Optimization

0 1
@initial_geometry.xyz
```

The below example input.gjf file includes the geometry. It is a simple initial linear H2O molecule. Notice that "Title Card..." is a comment and Gaussian disregards all text not in the #p line or below "0 1" line as comments unless it is containing a special character defined by Gaussian.

``` title="input.gjf"
%chk=gaussian.chk
#p PBE/SVP Opt Freq

Title Card - Optimization

0 1
O 0.0 0.0 1.5
H 0.0 0.0 3.0
H 0.0 0.0 0.0

```

## Gaussian Output Files

There is one main output file for Gaussian. The filename will depend on how you run Gaussian. For this tutorial and in the SLURM script, the output file will be called output.log. All of the energy values and other values we could possibly want are located somewhere in the output.log. The final geometry of a Gaussian 16 calculation can be found in the output.log file below the last occurrence of the string "Standard Orientation". In a finished Gaussian 16 calculation directory, there will be a fort.7 file which contains the archived entry of that calculation (the contents are also at the bottom of the output.log file). There will also be the Gaussian checkpoint file (named gaussian.chk in this tutorial which is defined in the input.gjf file). The checkpoint file is a large binary file that contains all of the internal information Gaussian was storing and using to do the calculation. If you have the checkpoint file, you can restart a calculation. You can use [formchk](https://gaussian.com/formchk/) and other utilities to convert the binary checkpoint file into text so you can parse the data. You can load the output.log file into GaussView to visualize and gather the results easier.


## GaussView

We have GaussView which is a visualization program specifically made for Gaussian calculation output. To use GaussView, add the below alias to the .bashrc file and lauch GaussView with the command ```gv```. Jerimiah Zamora currently has the most experience with using GaussView in our Research Group.

``` bash
alias gv='export LD_LIBRARY_PATH=/home/aderezen/gaussview/tar/gv/lib:$LD_LIBRARY_PATH && export PATH=/home/aderezen/gaussview/tar/gv:/home/aderezen/gaussview/tar/gv/exec:/home/aderezen/gaussview/tar/gv/bin:$PATH && export PATH=/home/aderezen/G16/AVX2/g16:$PATH && gv'

```

## SLURM Script for Gaussian 16

Below is an example SLURM script for Gaussian 16. After loading the correct modules and environment variables, you can invoke Gaussian 16 with the command ```g16 < input.gjf  > output.log```.


``` bash title="run_gaussian.sh"
#!/bin/bash
#SBATCH --job-name=JOBNAME               # Job name
#SBATCH --time=48:00:00               # Time limit hrs:min:sec
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH --ntasks-per-node=12

echo "SBATCH_GET_USER_ENV"
echo $SBATCH_GET_USER_ENV

export g16root="/home/aderezen/G16/AVX2/"
export GAUSS_SCRDIR="/lustre/scratch/$USER/$SLURM_JOB_ID"
mkdir $GAUSS_SCRDIR

. $g16root/g16/bsd/g16.profile

echo job start `date`

g16 < input.gjf  > output.log

echo job done `date`
rm -r $GAUSS_SCRDIR

```


