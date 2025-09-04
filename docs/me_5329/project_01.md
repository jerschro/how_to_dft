[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Project 1**

# Project 1

![Project_1_Instructions.pdf](../assets/pdfs/me_5329/Project_1_Instructions.pdf){ type=application/pdf style="min-height:100vh;width:100%" }

## Code Block in Instructions

```python
import molecule_lib as mlb
monomer_mol = mlb.read_xyz("NUCLEOTIDE.xyz")
dimer_mol = monomer_mol.add_coords(molecule = monomer_mol,
            absorbent_reference = "Bottom",
            surface_reference = "Top",
            dist = 4,
            axis = "z")
dimer_mol.to_xyz("NUCLEOTIDE_DIMER.xyz")

```