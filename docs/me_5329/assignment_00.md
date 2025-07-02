[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Assignment 0**

# Assignment 0

![Assignment_0_Instructions.pdf](../pdfs/me_5329/Assignment_0_Instructions.pdf){ type=application/pdf style="min-height:100vh;width:100%" }

## Code Block in Instructions

``` python title="generate_structure.py"
from rdkit import Chem
from rdkit.Chem import AllChem
import os

smile_string = "CCCC"
filename = "butane.xyz"

rdkit_mol = Chem.AddHs(Chem.MolFromSmiles(smile_string))
AllChem.EmbedMolecule(rdkit_mol)
AllChem.MMFFOptimizeMolecule(rdkit_mol)
filepath = os.path.join(os.getcwd(), filename)
Chem.MolToXYZFile(rdkit_mol, filepath)

```