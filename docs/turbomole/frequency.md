[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **aoforce/NumForce**

# Frequency Calculation Steps

1.  Create a new directory.
2. Copy the whole geometry optimization directory to the new frequency directory.
    * Remember `*` is a bash shortcut for all files. The cp command should look something like this `cp /path_of_geometry_opt_directory/* /path_of_frequency_directory/.`
3. Remove files not needed or that are recreated for the frequency calculation. You should remove the slurm-xxxxxxx.out, converged and GEO_OPT_CONVERGED.
     * Remember the command to remove files is `rm filename`. If you want to remove a directory you need to have the -r flag. If you want to remove multiple files, you need to have the -f tag if you don't want to approve every file deletion.
4. Run `define`
5. Press enter until you get to main menu then type ++q++ to exit. This is just to reset the control file.
6. Open control file and change "$scfconv 6" to $scfconv 8". This is to get a more accurate convergence criteria.
7. Now open the SLURM file.
     * *The below bullet points may contain incorrect information*
     * It is not necessary to do another geometry optimization so comment the "jobex -ri -c 700 "line.
     * If there are frozen atoms in the system, uncomment the line "NumForce -frznuclei"
     * If there are no frozen atoms in the system, uncomment the line "aoforce > force.out". This is what you should do for the adenine calculations.
8. Submit the job.