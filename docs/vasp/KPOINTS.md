[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [VASP](index.md) :fontawesome-solid-angle-right: **KPOINTS**
# KPOINTS <a href="https://www.vasp.at/wiki/index.php/KPOINTS" class="md-button small-button">VASP Wiki</a>

This file defines the KPOINTS for the VASP calculation. For every calculation other than a bulk structure we will use Γ-point (aka 1x1x1) as our KPOINTS. This is file defines discrete points in the reciprocal space used for Brillouin zone sampling for the VASP calculation. Different KPOINTS lead to more accuracy at a higher computational cost. Γ-point is the least computationally intense calculation and that is the preferred KPOINTS for any VASP optimization or phonopy displacement calculation we do because it produces only 1 KPOINT.

##  Γ-point KPOINTS File

``` title="KPOINTS"
Automatic
 0
Monkhorst
 1  1  1
 0. 0. 0.


```

## KPOINTS Test


=== ":fontawesome-solid-house:"
    Click through to see different KPOINTS files for a KPOINTS test.

    In a KPOINTS test directory, you can run the command ```head */KPOINTS``` to see all of the KPOINTS files.

    Jeremy has a script ```/home/jerschro/Scripts/vasp/generate_kpoint_test.sh``` that will generate and submit a KPOINTS test for you. Below is the help message for the script.


    ```
    hpc-login-node:/home/jerschro/Scripts/vasp$ bash generate_kpoint_test.sh -h
    usage: generate_kpoint_test.sh [-h]

    Script that generates kpoint test directories for vasp and submits jobs (if uncommented).

    generate_kpoint_test.sh reads orig/ directory in submit directory. Below are files needed in orig/
    -POSCAR
    -INCAR
    -$slurm_file
    -POTCAR

    defined variables (located in top of file):
    start                 Initial kpoint integer value.
    end                   Last kpont integer value.
    jobname               Jobname added to slurm_file.
    slurm_file            Name of slurm_file. Should have JOB_NAME where you want the jobname.

    current variables defined in top of file:
    $start = 1
    $end = 10
    $jobname = ex_kpoint_test
    $slurm_file = run_vasp.sh

    options:
    -h, --help            show this help message and exit.

    Written by Jeremy Schroeder 4-13-2024


    ```

=== "1x1x1"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     1  1  1
     0. 0. 0.

    ```

=== "1x2x2"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     1  2  2
     0. 0. 0.

    ```

=== "2x2x2"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     2  2  2
     0. 0. 0.

    ```

=== "2x3x3"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     2  3  3
     0. 0. 0.

    ```

=== "3x3x3"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     3  3  3
     0. 0. 0.

    ```

=== "3x4x4"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     3  4  4
     0. 0. 0.

    ```

=== "4x4x4"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     4  4  4
     0. 0. 0.

    ```

=== "4x5x5"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     4  5  5
     0. 0. 0.

    ```

=== "5x5x5"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     5  5  5
     0. 0. 0.

    ```

=== "5x6x6"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     5  6  6
     0. 0. 0.

    ```

=== "6x6x6"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     6  6  6
     0. 0. 0.

    ```

=== "6x7x7"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     6  7  7
     0. 0. 0.

    ```

=== "7x7x7"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     7  7  7
     0. 0. 0.

    ```

=== "7x8x8"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     7  8  8
     0. 0. 0.

    ```

=== "8x8x8"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     8  8  8
     0. 0. 0.

    ```

=== "8x9x9"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     8  9  9
     0. 0. 0.

    ```

=== "9x10x10"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     9  10  10
     0. 0. 0.

    ```


=== "9x9x9"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     9  9  9
     0. 0. 0.
    ```


=== "10x10x10"

    ``` title="KPOINTS"
    Automatic
     0
    Monkhorst
     10  10  10
     0. 0. 0.

    ```

