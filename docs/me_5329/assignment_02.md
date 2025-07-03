[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Assignment 2**

# Assignment 2

![Assignment_2_Instructions.pdf](../assets/pdfs/me_5329/Assignment_2_Instructions.pdf#toolbar=0&navpanes=0&scrollbar=0){ type=application/pdf style="min-height:100vh;width:100%" }

## Code Block in Instructions

```python title="create_dimer_structure.py"
import molecule_lib as mlb
monomer_mol = mlb.read_xyz("NUCLEOTIDE.xyz")
dimer_mol = monomer_mol.add_coords(molecule=monomer_mol, 
                    absorbent_reference="Bottom", 
                    surface_reference="Top", 
                    dist=4, 
                    axis="z")
dimer_mol.to_xyz("NUCLEOTIDE_DIMER.xyz")

```