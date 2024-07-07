[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **define**

# Geometry Optimization using DFT Steps

1. You can follow the steps below or look at the attached PowerPoint ["Guide-Turbomole_Files_&_Menus.pptx"](guide_ppt.md)
2. Convert the .xyz file to Turbomole format using command `x2t file_to_convert.xyz > coord`
3. Run `define`
4. Press enter twice to skip importing a prebuilt control file.
5. Now we are in the molecular geometry menu:
6. Import the coord file: Type "a coord"
7. Make sure #ATOMS is equal to the amount of atoms you have.
8. See if there is symmetry in structure: Type "desy"
9. Continue to the next menu: Type "*"
10. Answer the prompt if you are using internal coordinates: Type "no"
11. Now we are in the basis set menu:
12. Choose a basis set: Type "b all SVP" for the adenine calculations.
13. Ensure the #atoms is equal to #bas to confirm the basis set was defined cor=
rectly.
14. Continue to the next menu: Type "*"
15. Have define give a guess of electron occupation: Type "eht"
16. Accept the parameters: Type "y"
17. Give the total charge: The total charge for our structures is zero so type =
"0"
18. Accept charge orbitals occupation: Type "y"
19. Now we are in the main menu of define.
20. Set the dft functional:
     * Type "dft"
     * Type "func b3-lyp" for adenine calculations
     * Type "on"
     * Make sure it says "DFT is used" and the correct functional you want is listed.
     * Press enter to exit
21. Turn on ri (optimization algorithm):
     * Type "ri"
     * Type "on"
     * Make sure it says "RI IS USED"
     * Press enter to exit
22. Turn on marij (optimization algorithm):
     * Type "marij"
     * Press enter to exit
23. Turn on dft-3 dispersion correction:
     * Type "dsp"
     * Type "on"
     * Make sure it says "DFT-D3 correction is used"
     * Press enter to exit
24. Set the iteration limit higher:
     * Type "scf"
     * Type "iter"
     * Type "300"
     * Press enter twice to exit
25. Type "q" to finish the define menu.
26. Ensure define created all of the necessary files: auxbasis, basis, control, coord and mos should be in the directory now.
27. Check control file to see parameters are correct: Use command "vi control" or "nano control" to open the file
     * Ensure the basis set for each species is set which is listed under "$atoms"
     * Ensure "$scfiterlimit 300" is correct
     * Ensure under '$dft", the functional listed is correct
     * Ensure "$rij", "$marij" and "$dsp3" are in the control file. (Located near the bottom)
     * Exit nano by pressing "Ctrl-x", "y" and enter.
28. Open the SLURM file (run_turbomole.sh): Use vi or nano.
     * Change the job-name to something unique so you can remember it.
     * Edit time limit if necessary.
     * Edit partition, nodes, and ntasks amounts if necessary.
     * Ensure line "jobex -ri -c 700" is not commented out. This is the geometry optimization function for Turbomole. None of the other functions (NumForce and aoforce) should be uncommented in this area of the SLURM file.
29. Submit the job using command "sbatch run_turbomole.sh"
