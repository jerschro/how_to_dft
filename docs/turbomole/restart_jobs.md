[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **Restart Jobs**

# Instructions to Restart Turbomole Jobs

## Not Converged Geometry Optimization

1. If files not.converged and GEO_OPT_FAILED are present in the geometry optimization directory you submitted from, that means the calculation did not converge in the amount of iteration steps you gave it.
1. Run define and press enter multiple times to reset the coord file.
1. Re submit the job. You may want to increase the iteration steps in jobex line.
    *  For example, change ```jobex -ri -c 700``` to ```jobex -ri -c 2000```.

## Job Failed Due to Running Out of Time For Geometry Optimization

1. If no Turbomole job completion files (job.start, job.last, energy etc...) are in the directory the job was submitted in, that means the calculation timed out.
1. Look for the slurm-XXXXXXXX.out file where X are integers. This was the SLURM JOB ID of the job that ran out of time.
1. Go to /lustre/scratch/eraider/XXXXXXXX where XXXXXXXX is the SLURM JOB ID and eraider is your HPC username.
1. Copy all of these files to the original job submission directory.
    * Remember you can use * or -r with cp to make your life easier.
1. From there, follow the instructions above to resubmit the job.



## Frequency Job Restart

1. If the job submission directory is missing the completed frequency job files (vib_spectrum, vib_normal_modes etc...), then the frequency job ran out of time.
1. Look for the slurm-XXXXXXXX.out file where X are integers. This was the SLURM JOB ID of the job that ran out of time.
1. Go to /lustre/scratch/eraider/XXXXXXXX where XXXXXXXX is the SLURM JOB ID and eraider is your HPC username.
1. Copy all of these files to the original job submission directory.
    * Remember you can use * or -r with cp to make your life easier.
1. If you did a geometry optimization with a finer convergence criteria, you can check if this finished by seeing the geometry optimization completed files (job.start, job.last, energy etc...). You can uncomment the jobex line in the slurm submission file, run define like described above to reset control file, and resubmit the job.
1. If you did not do a geometry optimization and you job time is set to the maximum amount of time (48:00:00) in the SLURM file, this means the frequency job ran out of time. You could try to increase the amount of cpus or you will need to run the job on Dr. Aqunio's QOS. To do this ask either Jeremy or Dr. Aquino. This is because there is no nice way to restart a Turbomole frequency job if it runs out of time. All of the intermediate structures and calculations are saved in memory and it is all lost when the time runs out and job stops, therefore we need to re submit it over again with more time than what was requested the first time.



## Hints to Figure out Reasons of Failed Turbomole Jobs

* The two best files to check out is the job.last file and slurm-XXXXXX.out file.
* You can also do ```t2x coord > OO``` and ```molden OO``` to see an animation of the geometry optimization. If you click on ++"Geom Convergence"++ then ++"Movie"++ in MOLDEN, you can watch the calculation structure and total energy amount across the iterations. 
    * If there is not a a smooth parabola converging to a value, that means it is still working on converging and needs more iteration steps. See above instructions to restart the geometry optimization.
    * If the Geom Convergence line is ocillating then that means you probably won't converge to a global minimum structure and shoul drestart the calculation with a different initial geometry. Oscillations tend to happen between two local minimas so you could take one of the geometries of the structures, preturb the structure some, and start the geometry optimization again. 


