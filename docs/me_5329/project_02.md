[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Project 2**

# Project 2

![Project_2_Instructions.pdf](../assets/pdfs/me_5329/Project_2_Instructions.pdf){ type=application/pdf style="min-height:100vh;width:100%" }


## orca.inp Input Block in Instructions

```
! FUNCTIONAL BASIS_SET NEB-TS FREQ

%maxcore 4000

%pal
nprocs 12
end

%NEB NEB_END_XYZFILE "final_structure_opt.xyz"
END

* xyzfile 0 1 initial_structure_opt.xyz
 


```