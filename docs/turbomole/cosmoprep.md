[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **cosmoprep**

# Solvent Calculation Steps (cosmoprep)

1.  You can follow these instructions below or the instructions Tristan made in the attached word document [COSMO_instructions.docx](cosmo_docx.md)
2.  Take the optimized geometry "coord" file from the geometry optimization and place in solvent directory. Use the command "cp /file_path_you_want_to_copy/ /path_of_destination_of_copied_file/. "
     * Remember ".." is shorthand for the parent directory (aka the directory above the one you are currently in), "~" is short hand for your home directory (/home/eraider/), and "." is short hand for the current directory you are in.
     * Remember the basis set we are using for the adenine calculations are SVP and the functional is b3-lyp
3.  After setting up normal geometry optimiztion settings using define and the powerpoint or steps above, run the command "cosmoprep" like you run "define".
4.  If you want to have the solvent be other than default (polar/water environment), when epsilon =3D infinity is shown (1st input of cosmoprep), type the new epsilon or dielectric constant and press enter.
5.  Then press enter around 10 times until the radius definition menu appears.
6.  Then define optimized radius for all of the atoms by typing command "r all o".
7.  If you have aluminum in the system, you will need to type "r al b". (This is bc aluminum does not have a defined cosmoprep radius in Turbomole).
8.  Ensure the #atoms is equal to the number of #radius.
9.  Type "*" to exit the radius define menu. Then press enter around 2 more times to exit.
10. Make sure cosmoprep tags ("$cosmo" as an example) are at the top in the control file. If you changed the epsilon value (dielectric constant), the new value should be in line 2 of the control file.
11. Change the SLURM file as necessary and run "sbatch SLURM_filename.sh"
