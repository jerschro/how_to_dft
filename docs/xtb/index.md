---
hide:
  - navigation
---
[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: **xTB**

# xTB

This is the webpage for containing everything to do with xTB.

xTB is a lightweight semi-emperical QM/MM calculator from xTB. It is the calculator that CREST uses.

## xTB Documentation

The xTB Documentation is really informative and descriptive. I would recommend you take a look at it. Good examples on how xTB and CREST operate are on the Grimme-Lab Workshops webpage linked below.

* xTB: [https://xtb-docs.readthedocs.io/](https://xtb-docs.readthedocs.io/)
* Grimme-Lab Workshops: [https://grimme-lab.github.io/workshops/](https://grimme-lab.github.io/workshops/)

## How to Install xTB using conda

* If you are on Windows and have Anaconda/miniconda installed, go to search bar, look for "Anaconda Prompt" and open it. We can run CREST locally in this terminal.

* If you are on Mac or Linux and you have conda/miniconda installed, open the terminal. We can run CREST locally in this terminal.

If you need to install conda, read my install conda tutorial [Here](../hpcc/install_conda.md).

For all operating systems, run the commands below. This command creates a new conda environment named crest with CREST and xTB downloaded in it. To activate the conda environment and load CREST you type ```conda activate crest```.

``` conda
conda create -n xtb conda-forge::xtb

```

To know if you xtb is loaded. You should see (xtb) on the left of the terminal prompt line, such as the example below.

``` bash
(xtb) jeremy@CPU-NAME:~$

```

## How to Run xTB

All you need is xTB environment loaded and an .xyz file. It is perfectly ok to run xTB in the local terminal. 

```
xtb initial_geom.xyz --opt tight > xtb.out

```

## Looking at the Output Files xTB Generates

The list below is what files CREST generates for a conformational sampling. Important files are listed below and the rest are in the table:

* **xtb_opt.xyz** - the optimized structure of the xTB calculation.
* **xtb.out** - the terminal output of CREST. The total energy xTB calculates is located in this file.

