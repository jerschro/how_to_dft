[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Assignment 5**

# Assignment 5

![Assignment_5_Instructions.pdf](../pdfs/me_5329/Assignment_5_Instructions.pdf#toolbar=0&navpanes=0&scrollbar=0){ type=application/pdf style="min-height:100vh;width:100%" }


## Example ORCA input file from instructions

```title="orca.inp"
! B3LYP 6-31G* NEB-TS freq

%maxcore 4000

%pal
nprocs 12
end

%NEB NEB_END_XYZFILE "final_well_opt.xyz"
END

* xyzfile 0 1 initial_well_opt.xyz

```