---
hide:
  - navigation
---
[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: **Quantum Espresso**
# Quantum Espresso

This is the webpage for containing everything to do with Quantum Espresso.

[Quantum Espresso](https://www.quantum-espresso.org/) is an Italian open source solid state quantum chemistry code. It is a very popular DFT code and is pretty reliable. It's main executable is called **pw.x** and this is main script we will use to run Quantum Espresso.

The documentation for Quantum Espresso does exist but it is very convulated and not user friendly. It is dependent on what QE executable you call. So for PWscf, this is the documentation for it [Here](https://www.quantum-espresso.org/Doc/pw_user_guide/). This is the documentation for describing **pw.in** file, [Here](https://www.quantum-espresso.org/Doc/INPUT_PW.html).

## Quantum Espresso Input

Quantum Espresso only requires one input file named **pw.in**. This format of this input file is Fortran 90 which means that the QE input is very strict on syntax such as white space, commas, semi colons, and etcetera. If the QE calculation fails immediately, there is probably an issue in the input. For example, the issue could be you having a trailing white space after a comma.

There are different sections of the **pw.in** file; and below we will discuss them in detail

### "CONTROL" Section

This is the main calculation settings for QE. To tell QE what kind of routine you want it to do, you will change the calculation parameters. It's currently defined as 'qe_routine'. You may also change the title parameter but this is not important. The 'calculation' parameter is the only setting that should be changed in this section.


```title="control pw.in section"
&control
    title = 'Si_pristine',
    calculation = 'qe_routine',
    restart_mode = 'from_scratch',
    outdir = './out',
    pseudo_dir = '/home/jerizamo/precPS',
    prefix = 'new',
    disk_io = 'none',
    verbosity = 'default',
    etot_conv_thr = 0.000001,
    forc_conv_thr = 0.001,
    nstep = 400,
    tstress = .true.,
    tprnfor = .true.
/
```

### "SYSTEM" Section

In this section of the **pw.in** file, you will tell Quantum Espresso information about your system. The parameter 'nat' stands for the *number of atoms* and the parameter 'ntyp' stands for the *number of atom species* (Si, B, P etc.). The other parameters should not be changed.

```title="SYSTEM pw.in section"
&SYSTEM
    ibrav = 0,
    nat = 8,
    ntyp = 1,
    ecutwfc = 68,
    vdw_corr = 'dft-d3'
/
```

### "ELECTRONS", "IONS" and "CELL" Sections

These sections define other calculation settings about the input and should not be changed unless it is necessary.

```title="ELECTRONS, IONS, and CELL pw.in sections"
&ELECTRONS
    electron_maxstep = 1000,
    conv_thr = 1.0D-8,
    diago_thr_init = 1e-2,
    startingpot = 'atomic',
    startingwfc = 'atomic',
    mixing_mode = 'plain',
    mixing_beta = 0.5,
    mixing_ndim = 8,
    diagonalization = 'david'
/
&IONS
    ion_dynamics = 'bfgs'
/
&CELL
    cell_dynamics = 'bfgs'
/

```

### "ATOMIC SPECIES" Section

This section of the **pw.in** is where we define the following: what atomic species are in the file, their atomic masses (in kg), and the specific pseudopotential we want to use. Using the atomic mass from Google for each species will be accurate for our calculations. To define a pseudopotential, use the format "XX.upf" where XX is the species. For the purposes of ME 5329, every pseudopotential you will need should be avaliable in this format. If you specify a specific file in the "pseudo_dir" (/home/jerizamo/precPS/), QE will read this pseudopotential file.

```title="ATOMIC_SPECIES pw.in section"
ATOMIC_SPECIES
Si    28.0855  Si.upf

```

### "ATOMIC POSITIONS" Section

This is where the atomic positions of the initial geometry are defined for Quantum Espresso. These are the positional coordinates listed in Angstrom. To get the cartesian coordinates from a .vasp file, you may use the below code in molecule_lib and copy paste the position lines into this section of **pw.in**.

```python title="get_qe_atomic_positions.py"
import molecule_lib as mlb

abc_mol = mlb.read_vasp("initial.vasp")
xyz_mol = mol.convert()
xyz_mol.to_xyz("initial.xyz")
xyz_mol.print()

```

```title="ATOMIC_POSITIONS pw.in section"
ATOMIC_POSITIONS angstrom
Si         4.08277         4.08277         1.36092
Si         0.00000         2.72185         2.72185
Si         4.08277         1.36092         4.08277
Si         0.00000         0.00000         0.00000
Si         1.36092         4.08277         4.08277
Si         2.72185         2.72185         0.00000
Si         1.36092         1.36092         1.36092
Si         2.72185         0.00000         2.72185


```

### "K POINTS" Section

This section in the **pw.in** file is where you define the k-point grid mesh that you want QE to use. A k-point of "1x2x3" is represented in the code box below.

```title="ATOMIC_POSITIONS pw.in section"
K_POINTS automatic
1 2 3 0 0 0

```

### "CELL PARAMETERS" Section

This is the final section of **pw.in**. This is where we define the unit cell box lattice matrix. We can copy the unit cell lattice matrix from the top of a .vasp file and paste it here. Please note that there is no lattice constant for **pw.in** which means if we want to compress the unit cell, we need to **manually change the atomic positions and lattice matrix** instead of just changing a constant (This information is important for Project 5 of ME 5329).


```title="CELL_PARAMETERS pw.in section"
CELL_PARAMETERS angstrom
        5.44370         0.00000         0.00000
       -0.00000         5.44370         0.00000
        0.00000         0.00000         5.44370

```


### Complete pw.in File

This is  and example of a Si_pristine k-points calculations for ME 5329 Project 3.

```title="pw.in"
&control
    title = 'Si_pristine',
    calculation = 'vc-relax',
    restart_mode = 'from_scratch',
    outdir = './out',
    pseudo_dir = '/home/jerizamo/precPS',
    prefix = 'new',
    disk_io = 'none',
    verbosity = 'default',
    etot_conv_thr = 0.000001,
    forc_conv_thr = 0.001,
    nstep = 400,
    tstress = .true.,
    tprnfor = .true.
/
&SYSTEM
    ibrav = 0,
    nat = 8,
    ntyp = 1,
    ecutwfc = 68,
    vdw_corr = 'dft-d3'
/
&ELECTRONS
    electron_maxstep = 1000,
    conv_thr = 1.0D-8,
    diago_thr_init = 1e-2,
    startingpot = 'atomic',
    startingwfc = 'atomic',
    mixing_mode = 'plain',
    mixing_beta = 0.5,
    mixing_ndim = 8,
    diagonalization = 'david'
/
&IONS
    ion_dynamics = 'bfgs'
/
&CELL
    cell_dynamics = 'bfgs'
/

ATOMIC_SPECIES
Si    28.0855  Si.upf

ATOMIC_POSITIONS angstrom
Si         4.08277         4.08277         1.36092
Si         0.00000         2.72185         2.72185
Si         4.08277         1.36092         4.08277
Si         0.00000         0.00000         0.00000
Si         1.36092         4.08277         4.08277
Si         2.72185         2.72185         0.00000
Si         1.36092         1.36092         1.36092
Si         2.72185         0.00000         2.72185

K_POINTS automatic
1 1 1 0 0 0

CELL_PARAMETERS angstrom
        5.44370         0.00000         0.00000
       -0.00000         5.44370         0.00000
        0.00000         0.00000         5.44370
 
 
 
```



## Quantum Espresso SLURM File

Below is the **run_qe.sh** SLURM file for Quantum Espresso. The command to invoke QE is ```mpirun pw.x < pw.in  > pw.out```.


```bash title="run_qe.sh"
#!/bin/bash
#SBATCH --job-name=QE_job
#SBATCH --time=01:00:00
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH -n 12
#SBATCH --mem-per-cpu=4G
#SBATCH -o slurm.o-%j
#SBATCH -e slurm.e-%j

shopt -s extglob; ulimit -s unlimited; 

home=$SLURM_SUBMIT_DIR; START_TIME=$(date); cd $SLURM_SUBMIT_DIR; 
keepFileList=" OUTCAR mos alpha beta *.in *.inp XDATCAR "

JOBTYPE="QE"
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

# Quantum Espresso
module load gcc/10.1.0 openmpi/4.1.4 quantum-espresso/7.2-mpi-openmp

mpirun pw.x < pw.in  > pw.out

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



## Quantum Espresso Output

The main and **only** output file of QE is **pw.out**. ***More details of this section will be made if there is a demand. Please ask Jeremy to make this section more complete if it will be helpful to your studies. <3 Jeremy :fontawesome-solid-heart:***