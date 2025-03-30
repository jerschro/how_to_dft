[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [VASP](index.md) :fontawesome-solid-angle-right: **OUTCAR**
# OUTCAR <a href="https://www.vasp.at/wiki/index.php/OUTCAR" class="md-button small-button">VASP Wiki</a>

This is the main output file of the VASP calculation. Below will list certain values we want from the VASP calculation and the ```grep``` command to get them.

## Total energy

``` bash
grep "free energy" OUTCAR

```


The total energy value is in units of eV.


## Number of KPOINTS

``` bash
grep "irreducible k-points:" OUTCAR

```

For Γ-point, this value will be 1.

## Volume of Unit Cell

``` bash
grep "volume of cell :" OUTCAR

```

The volume of the unit cell is in units of cubic angstroms $\text{Å}^3$.

## Total Time of VASP Calculation

``` bash
grep "Elapsed time (sec):" OUTCAR

```

The elapsed time unit is given in seconds.

## OUTCAR Values Collection Script

You can use Jeremy's script to collect these values mentioned above.

``` bash
alias vasp_energy='/home/jerschro/conda/bin/python3 /home/jerschro/Scripts/vasp/read_outcars_ssh.py'

```

Below is the help output of vasp_energy.

```
hpc-login-node:$ vasp_energy -h
usage: vasp_energy [-h] [-f FILENAME] [-e] [-k] [-v] [-t] [-a SORTHIGH] [-d SORTLOW]

finds values from OUTCAR files

options:
  -h, --help            show this help message and exit
  -f FILENAME, --filename FILENAME
                        if the outcarfile has a different file name
  -e, --energy          turn off energy value print out
  -k, --kpoints         turn on kpoint values print out
  -v, --volume          turn on volume values print out
  -t, --time            turn on time values print out
  -a SORTHIGH, --sorthigh SORTHIGH
                        sort highest value first
  -d SORTLOW, --sortlow SORTLOW
                        sort lowest value first

written by jeremy schroeder 2-27-2024


```