[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **Collect Results**

# Collecting Turbomole Results

### To Find Geometry Optimization and Solvent Total Energy
While being in the directory. Run command `grep "total energy" job.last`. This command reads the file job.last and prints the any line in that file that contains the string "total energy". You can also open the job.last file, scroll to near the very bottom and there is a box where the total energy of the optimization is located.

### To Find Frequency Results
Read the instructions Tristan made that are in the attached word document [Freq_instruction.docx](frequency_docx.md). We typically only report the values at T = 298.15K and P = 0.1 MPA but you can also find a range of temperature or pressure values.