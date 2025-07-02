[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [VASP](index.md) :fontawesome-solid-angle-right: **POTCAR**
# POTCAR <a href="https://www.vasp.at/wiki/index.php/POTCAR" class="md-button small-button">VASP Wiki</a>

This file contains the pseudopotentials for each species in the POSCAR file. The order of the species in the POSCAR file MUST match the order of the species in the POTCAR file. This also means if you have the same species written twice (seperated by a different species) in the species line, you need to have the potentials copied twice in the POTCAR file. This is because VASP pairs the first species to the first potential, second species to the second potential, etc.


## How to Make the POTCAR File

You can follow the instructions below or read the instructions on the VASP Wiki [Here](https://www.vasp.at/wiki/index.php/Preparing_a_POTCAR).

For every species in your POSCAR file, you need to have the corresponding potential in the POTCAR file. Let's look at line 6 of thymine.vasp seen in the POSCAR which is where the species information is stored.

``` title="thymine.vasp" linenums="1"
C8 H9 N3 O2
1.0
    11.2596998215         0.0000000000         0.0000000000
        0.0000000000         4.4117999077         0.0000000000
    -2.5300564938         0.0000000000        17.4430679131
    N    C    O    H
12   32    8   36
Direct
...

```

So we need to get the potentials for ```N C O H``` in that order. We can do it in two lines, as shown below. To access the POTCAR Directory, you need to be on the VASP License as the POTCAR file is copyrighted and proprietary to VASP. The VASP License agreement states that only users on the research group's VASP License can obtain and access POTCAR files.

``` bash
PATH_TO_POTCARS=/home/jerschro/VASP/POTCARS
cat $PATH_TO_POTCARS/N/POTCAR $PATH_TO_POTCARS/C/POTCAR $PATH_TO_POTCARS/O/POTCAR $PATH_TO_POTCARS/H/POTCAR > POTCAR

```

Then we can run this command ```grep "TITEL" POTCAR``` to confirm that the POTCAR file contains the right pseudopotentials in the right order, as shown below. You could also use vi and search for ```TITEL``` test.

``` bash
hpc-login-node$ grep "TITEL" POTCAR
   TITEL  = PAW_PBE N 08Apr2002
   TITEL  = PAW_PBE C 08Apr2002
   TITEL  = PAW_PBE O 08Apr2002
   TITEL  = PAW_PBE H 15Jun2001

```

If you don't see the species in the right order vertically, try creating the POTCAR file again. VASP will not reorder or notice the species in the wrong order. If you have the wrong order in the POTCAR file, VASP will still run but you will have a very weird looking and wrong optimization because the species were switched around.

After the POTCAR file is confirmed to be in the right order, you can use it for the VASP calculation. You NEVER need to modify any details or information in the POTCAR file.
