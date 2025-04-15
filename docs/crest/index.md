---
hide:
  - navigation
---
[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: **CREST**
# CREST

This is the webpage for containing everything to do with CREST.


Introduction paragraph to crest.

## CREST Documentation

The CREST Documentation is really informative and descriptive. I would recommend you take a look at it. Also you should check out the xTB documentation which is the main QM/MM calculator CREST uses.

* CREST: [https://crest-lab.github.io/crest-docs/](https://crest-lab.github.io/crest-docs/)
* xTB: [xtb-docs.readthedocs.io/](xtb-docs.readthedocs.io/)

## How to Install CREST using conda

* If you are on Windows and have Anaconda/miniconda installed, go to search bar, look for "Anaconda Prompt" and open it. We can run CREST locally in this terminal.

* If you are on Mac or Linux and you have conda/miniconda installed, open the terminal. We can run CREST locally in this terminal.

* If you are on the HPCC, make sure you have conda installed. When you run crest, you need to run it either in an SLURM script (that you sbatch to run) or on an interactive node which you can do so by running the command below ```salloc -p quanah -N 1 -n 1 -t 60```. This salloc command will request and give you an interactive node on quanah for 1 hour. **DO NOT RUN CREST ON THE LOGIN NODES ON THE HPCC!!! IF YOU DO THIS, 1) IT IS ILLEGAL and 2) IT MAKES IT SLOW FOR EVERYONE ELSE USING THE HPCC.**

For all operating systems, run the commands below. This command creates a new conda environment named crest with CREST and xTB downloaded in it. To activate the conda environment and load CREST you type ```conda activate crest```.

``` conda
conda create -n crest conda-forge::crest

```

To know if you crest is loaded. You should see (crest) on the left of the terminal prompt line, such as the example below.

``` bash
(crest) jeremy@CPU-NAME:~$

```

## How to use CREST for Conformational Sampling

The example we are going to use is Squalene ($\mathrm{C_{30}H_{50}}$). Squalene is an organic molecule with two possible ways to draw it on a 2D surface. It has many rotatable C-C bonds with each bond rotation being multiple possible different conformations.

=== "SMILE String"

    SMILE String for Squalene:

    ```
    CC(=CCC/C(=C/CC/C(=C/CC/C=C(/CC/C=C(/CCC=C(C)C)\C)\C)/C)/C)C

    ```


=== "Image 1"
    ![Squalene 2D1](../images/crest/squalene_2d1.png)

    From [https://www.sigmaaldrich.com/US/en/product/mm/821068](https://www.sigmaaldrich.com/US/en/product/mm/821068)

=== "Image 2"
    ![Squalene 2D2](../images/crest/squalene_2d2.png)

    From [https://www.researchgate.net/figure/Squalene-chemical-structure-Squalene-is-a-natural-dehydrotriterpenic-hydrocarbon-C-30-H_fig2_335133970](https://www.researchgate.net/figure/Squalene-chemical-structure-Squalene-is-a-natural-dehydrotriterpenic-hydrocarbon-C-30-H_fig2_335133970)



For CREST to run, we need an initial .xyz structure. Lets generate it using the [RDKit](https://www.rdkit.org/docs/api-docs.html) library and the SMILE string of Squalene. Run the below code either in a python file or the python kernel.

``` python 
from rdkit import Chem
from rdkit.Chem import AllChem
import os

smile_string = r"CC(=CCC/C(=C/CC/C(=C/CC/C=C(/CC/C=C(/CCC=C(C)C)\C)\C)/C)/C)C" #we placed r before the string to make it a raw string because of the backslashes present in the smile string. without the r and python could interpret them as special characters.
xyz_filename = "squalene_initial.xyz" #file you want the molecule to be saved to.

rdkit_mol = Chem.AddHs(Chem.MolFromSmiles(smile_string)) #generates a 2d rdkit_mol object and adds Hydrogens where it is not specified in the SMILE string
AllChem.EmbedMolecule(rdkit_mol) #makes the 2d rdkit_mol object into a 3d rdkit_mol object
Chem.MolToXYZFile(rdkit_mol, os.path.join(os.getcwd(), xyz_filename)) #saves rdkit_mol object to a file in an .xyz format

```
CREST documentation reccomends to pre optimize the initial structure using the same level of theory we will use in CREST so, lets first run xTB to optimize squalene_initial.xyz. Let's run this command in a new directory. Also xTB, is downloaded when we install CREST so we can use the same conda environment.

```
xtb squalene_initial.xyz --gfn2 > xtb.out
cp xtbopt.xyz squalene_opt.xyz

```

Now lets run CREST! Run the command below in a new directory. We can add `> crest.out` to the command to direct the stdout to a file so we can save the CREST terminal output. The default algorithim CREST uses is the iMTD-GC algorithim which is explained [HERE](https://crest-lab.github.io/crest-docs/page/overview/workflows.html#imtd-gc-algorithm).

```
crest squalene_opt.xyz --gfn2 > crest.out

```

