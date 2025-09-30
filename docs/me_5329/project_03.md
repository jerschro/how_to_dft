[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Project 2**

# Project 3

![Project_3_Instructions.pdf](../assets/pdfs/me_5329/Project_3_Instructions.pdf){ type=application/pdf style="min-height:100vh;width:100%" }


## Code Block in Instructions

```python
import molecule_lib as mlb

pristine = mlb.read_vasp("Si_pristine_OPT.vasp")
supercell = pristine.generate_supercell(x=2, y=2, z=2)
supercell.to_vasp("Si_supercell.vasp")
    

```


## pw.in Block in Instructions

```
&SYSTEM
    ibrav = 0,
    nat = 64,
    ntyp = 2,
    ecutwfc = 68,
    vdw_corr = 'dft-d3',
    occupations = 'smearing',
    smearing = 'mp',
    degauss = 0.01
/
    
```