[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [VASP](index.md) :fontawesome-solid-angle-right: **Slurm Script**
# SLURM Script

Below is an example SLURM script you can use. 

The command to invoke VASP is ```mpirun  vasp_std >& vasp.out``` once the correct modules have been loaded.

``` bash title="run_vasp.sh"
#!/bin/bash
#SBATCH --job-name=JOB_NAME             # Job name
#SBATCH --time=48:00:00               # Time limit hrs:min:sec
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH --ntasks-per-node=64

#this vasp slurm script is for one job on nocona

# Modules
module load gcc/10.1.0 openmpi/4.1.4 vasp/6.3.2-openmp
#module load gcc/10.1.0 openmpi/4.0.4 vasp/5.4.4-openmp

SDIR=`pwd`
ex=$$
echo "---------------------------------------------------------" > $SDIR/job.$ex
echo "        JOB STARTED ON: " `date` >> $SDIR/job.$ex
echo "        NODE NAME:      " `hostname` >> $SDIR/job.$ex
echo "        DIR:            " `pwd` >> $SDIR/job.$ex

if [ !  -f POSCAR ]
then
  echo "!!!Job stopped. File POSCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f INCAR ]
then
  echo "!!!Job stopped. File INCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f KPOINTS ]
then
  echo "!!!Job stopped. File KPOINTS is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f POTCAR  ]
then
  echo "!!!Job stopped. File POTCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi

echo "        RUNNING VASP at  `date` "  >> $SDIR/job.$ex

mpirun  vasp_std >& vasp.out

rm -f  WAVECAR CHG* TMPCAR REP* EIG*
rm -f DOSCAR IBZKPT ICONST PCDAT

echo "        JOB FINISHED ON: " `date` >> $SDIR/job.$ex
echo "---------------------------------------------------------" >> $SDIR/job.$ex

```

## VASP With VTST Tools

Thanks to Jerimiah Zamora, we have VASP compiled with UT Austin's Transition State Tools for VASP (VTST Tools). Below is the SLURM Script that envokes VASP VTST Tools.

``` bash title="run_vasp_vtst.sh"
#!/bin/bash
#SBATCH --job-name=JOB_NAME             # Job name
#SBATCH --time=48:00:00               # Time limit hrs:min:sec
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH --ntasks-per-node=64

#this vasp slurm script is for one job on nocona

# Modules
module load gcc/10.1.0
module load openmpi/4.1.4
module load netlib-scalapack/2.2.0-mpi
module load openblas/0.3.12-openmp
module load fftw/3.3.8-mpi-openmp
module load netlib-lapack/3.10.1

export VASP_DIR=/home/jerizamo/vasp/vasp.6.3.2/bin


SDIR=`pwd`
ex=$$
echo "---------------------------------------------------------" > $SDIR/job.$ex
echo "        JOB STARTED ON: " `date` >> $SDIR/job.$ex
echo "        NODE NAME:      " `hostname` >> $SDIR/job.$ex
echo "        DIR:            " `pwd` >> $SDIR/job.$ex

if [ !  -f POSCAR ]
then
  echo "!!!Job stopped. File POSCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f INCAR ]
then
  echo "!!!Job stopped. File INCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f KPOINTS ]
then
  echo "!!!Job stopped. File KPOINTS is missing!!! " >> $SDIR/job.$ex
  exit
fi
if [ !  -f POTCAR  ]
then
  echo "!!!Job stopped. File POTCAR is missing!!! " >> $SDIR/job.$ex
  exit
fi

echo "        RUNNING VASP at  `date` "  >> $SDIR/job.$ex

mpirun $VASP_DIR/vasp_std >& vasp.out

rm -f  WAVECAR CHG* TMPCAR REP* EIG*
rm -f DOSCAR IBZKPT ICONST PCDAT

echo "        JOB FINISHED ON: " `date` >> $SDIR/job.$ex
echo "---------------------------------------------------------" >> $SDIR/job.$ex

```