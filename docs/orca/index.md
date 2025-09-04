---
hide:
  - navigation
---
[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: **ORCA**
# ORCA

This is the webpage for containing everything to do with ORCA.

ORCA is an open source DFT program that has a lot of flexibility and is very easy to use. Check out the detailed ORCA manual which has alot of information on the basis sets, functionals, and specifics of how ORCA does the calculation. You can use the search function in the ORCA manual to help answer a question you may have. ORCA also has tutorials that will help show you how it works. There is also another documentation website that is focused on the input of ORCA that is a good resource.

## ORCA Documentation

* [ORCA 6.0 Manual](https://www.faccts.de/docs/orca/6.0/manual/)
* [ORCA 6.0 Tutorials](https://www.faccts.de/docs/orca/6.0/tutorials/)
* [ORCA 5.0 Tutorials](https://www.faccts.de/docs/orca/5.0/tutorials/)
* [ORCA Input Library](https://sites.google.com/site/orcainputlibrary/home)


## ORCA Input Files

The initial files required for ORCA are:

* orca.inp
* SLURM file
* initial coordinates in .xyz format (optional because you can supply coordinates in orca.inp)
    * Make sure it is a unique filename and not a name ORCA will overwrite for the output like orca.xyz which is the final geometry of the ORCA calculation.

## orca.inp

The orca.inp file is the main input file for ORCA. The first line is the input line that will contain all of the calculation settings you want ORCA to do that starts with "!". Anything with a "%" is a setting for ORCA to read and there is alot of customizability with ORCA. You define the coordinates with an "*" as you will see below. ORCA is not case sensitive.

Near the coordinate definition ("\* xyz X X" or "\* xyzfile X X filename.xyz") you will need two integers. The first integer is the molecular charge of the system. The second integer is the multiplicity of the system. The multiplicity of the system is almost always 1 if the charge is 0 for a molecule that has the correct charge and is a closed shell system. The multiplicity describes the amount of possible spin states in the system and it is defined as $2S + 1$ where $S$ is the total spin quantum number. For a closed shell system, the multplicity is 1 also called a singlet and for example an unpaired electron has a doublet spin or multiplicity of 2.

## Example orca.inp

The below orca.inp file will run a DFT geometry optimization and a frequency calculation with B3LYP functional, 6-31G* basis set, using RI (Resolution of Identity) Algorithms. 

``` title="orca.inp"
! B3LYP 6-31G* OPT RIJCOSX FREQ

%maxcore 4000

%pal
nprocs 12
end

* xyzfile 0 1 initial_geom.xyz

```

The below example orca.inp file includes the geometry. It is a simple initial linear H2O molecule.

``` title="orca.inp"
! B3LYP 6-31G* OPT RIJCOSX FREQ

%maxcore 4000

%pal
nprocs 12
end

* xyz 0 1
O 0.0 0.0 1.5
H 0.0 0.0 3.0
H 0.0 0.0 0.0
*

```

## ORCA Output Files

The main output file for ORCA is orca.out . You can open orca.out to see everything ORCA calculates. There are also alot of other files ORCA generates. The final geometry is in the orca.xyz file. Jeremy has also wrote a script that you can use get values from ORCA calculations. Put the alias below into your .bashrc and type ```orca_energy --help``` to see everything the script will find.

``` bash 
alias orca_energy='/home/jerschro/conda/bin/python3 /home/jerschro/Scripts/orca/orca_energy.py'

```

## SLURM Script for ORCA

Below is an example SLURM script for ORCA. After loading the correct modules and environment variables, you can invoke ORCA with the command ```$ORCADIR/orca orca.inp >> orca.out```. There are two SLURM script versions below. The first one runs one job and the second one runs multiple .inp files in the same node.

``` bash title="run_orca.sh"
#!/bin/bash
#SBATCH --job-name=JOBNAME
#SBATCH --partition nocona
#SBATCH --nodes=1
#SBATCH --ntasks=12
#SBATCH --time=03:00:00
#SBATCH --mem-per-cpu=4G

#export ORCADIR=/lustre/work/ddecastr/orca_4_2_1_linux_x86-64_shared_openmpi314
#export ORCADIR=/home/rnieman/PROGRAMS/orca_4_2_1_linux_x86-64/orca_4_2_1_linux_x86-64_openmpi314
export ORCADIR=/lustre/work/rnieman/orca_5_0_1_linux_x86-64_shared_openmpi411
export PATH=$ORCADIR:$PATH
export LD_LIBRARY_PATH=$ORCADIR:$LD_LIBRARY_PATH

module load gcc/10.2.0 openmpi/4.0.4

mkdir -p /lustre/scratch/$USER/$SLURM_JOB_ID
WRKDIR=/lustre/scratch/$USER/$SLURM_JOB_ID
cd $WRKDIR
cp $SLURM_SUBMIT_DIR/* . -f

# control echoes
echo "ORCADIR :$ORCADIR"
echo "PATH     :$PATH"
echo "start up"
echo "HOME=$HOME"
echo "WRKDIR=$WRKDIR"
echo "HOSTNAME=$HOSTNAME"
echo "JOBID=$SLURM_JOB_ID"
echo "SUBMIT_DIR=$SLURM_SUBMIT_DIR"
echo "NSLOTS=$SLURM_NTASKS, NPEFF=$NPEFF"
echo "P_PER_N_eff=$P_PER_N_eff"
echo "P_PER_N=$P_PER_N"
echo "==============================="

#-----------------------------------------------------------------------
# NOW EXECUTION of the Turbomole JOB.
# This has to be changed according to particular Turbomole specification.
##########################################
echo "STARTING AT " `date`
lista=orca.inp

for inp in $lista
  do
        out=${inp%inp}out
        date > $out
        hostname >> $out
        $ORCADIR/orca $inp >> $out
        date >> $out
done

## *********************************************************************
echo "FINISHED AT " `date`
##########################################
echo "FINAL COPY: WRKDIR=$WRKDIR"
cd $WRKDIR
rm slurm* -f
pwd
rmfiles="`find . -size +50M`"
echo "rmfiles=$rmfiles"
if [ "$rmfiles" == "" ]
then
    echo 'No big files to remove.'
else
    echo 'Removing big files:'
    echo $rmfiles
    rm -f $rmfiles
fi
    mv -f $WRKDIR/* $SLURM_SUBMIT_DIR
    rm $WRKDIR -rf

```


``` bash title="run_orca.sh"
#!/bin/bash
#SBATCH --job-name=ORCA_job
#SBATCH --time=06:00:00
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -o slurm.o-%j
#SBATCH -e slurm.e-%j

shopt -s extglob; ulimit -s unlimited; 

home=$SLURM_SUBMIT_DIR; START_TIME=$(date); cd $SLURM_SUBMIT_DIR; 
keepFileList=" OUTCAR mos alpha beta *.in *.inp XDATCAR "

JOBTYPE="ORCA"
WRKDIR=/lustre/scratch/$USER/$JOBTYPE/$SLURM_JOB_ID
#WRKDIR=/lustre/work/$USER/$JOBTYPE/$SLURM_JOB_ID

[ -z $WRKDIR ] && [ -z $JOBTYPE ] && exit;
[[ $JOBTYPE == "XTB" ]] && [[ ! "$SLURM_NTASKS" == "1" ]] && exit;
mkdir -p $WRKDIR

echo "JOB-TYPE: " $JOBTYPE; 		echo "Job ID: " $SLURM_JOB_ID
echo "Start Time: " $START_TIME; 	echo "Submit Directory:  " $SLURM_SUBMIT_DIR
echo "Work Directory: " $WRKDIR

#JOB--------------------------------------------------------------------
cp $SLURM_SUBMIT_DIR/!(slurm*) $WRKDIR -pf
ln -s $WRKDIR 0.$JOBTYPE-$SLURM_JOB_ID; cd $WRKDIR; 

#______Orca
	export ORCADIR=/lustre/work/rnieman/orca_6_0_0_shared_openmpi416
	export PATH=$ORCADIR:$PATH;	export LD_LIBRARY_PATH=$ORCADIR:$LD_LIBRARY_PATH
	module load gcc/10.2.0 openmpi/4.0.4
		for inp in *.inp; do out=${inp%inp}out; $ORCADIR/orca $inp >> $out; done;

#EXIT--------------------------------------------------------------------

cd $WRKDIR; smallSlurm="`find slurm* -maxdepth 1 -size -50w`" 2> /dev/null; 
rm -f $smallSlurm; keepFileList="$keepFileList *.out *.log"; 
if [[ -f $WRKDIR ]] && [[ -f $SLURM_SUBMIT_DIR ]]; then
	cd $WRKDIR;
	for i in $keepFileList; do 
		[ -f $i ] && mv -f $i $SLURM_SUBMIT_DIR; 
	done
	largeFiles="`find . -maxdepth 1 -size +80M`"
	for j in $largeFiles; do 
		rm -f $j 
	done
fi
cp -pf $WRKDIR/* $SLURM_SUBMIT_DIR 2> /dev/null; cd $SLURM_SUBMIT_DIR
[ -z $largeFiles ] && echo -e "\nRemoved Files:\n"$largeFiles
echo -e "\nKept Files:\n"$keepFileList

#-----------------------------------------------------------------------
END_TIME=$(date) 
time_diff=$(($(date -d "$END_TIME" +%s) - $(date -d "$START_TIME" +%s)))
time_diff=$(date -u -d @"$time_diff" +'%H:%M:%S')
echo "End Time: " $END_TIME; echo "Total Calculation Time: " $time_diff
#-----------------------------------------------------------------------

```


