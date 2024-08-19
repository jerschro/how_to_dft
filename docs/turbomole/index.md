[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Turbomole](index.md) :fontawesome-solid-angle-right: **Turbomole**
# Turbomole

This is the homepage for containing everything to do with Turbomole. 

## Turbomole Section Pages

* [Turbomole Guide](guide_ppt.md) - Powerpoint containing basic description of Turbomole and DFT geometry optimization instructions.
* [define](define.md) - Instructions for DFT geometry optimization.
* [cosmoprep](cosmoprep.md) - Instructions for DFT solvent calculations.
* [cosmoprep Guide](cosmo_docx.md) - Word Document containing instructions for DFT solvent calculations.
* [aoforce/NumForce](frequency.md) - Instructions for DFT vibrational frequency calculations.
* [Collect Results](collect_results.md) - Instructions on how to retrieve Turbomole calculation results.
* [freeh](frequency_docx.md) - Word document containing instructions on how to retrieve Turbomole frequency calculation results.

## Turbomole Brief Overview
The description below was written by Tristan Fisher.

There are three main types of calculations we will perform in this process. Each of these are part of the overall Turbomole program: 

* Geometry Optimization: This allows us to find an approximated ground-state energy for a given molecular structure in gaseous form.  
    * Program Name: [define](define.md) 
    * Input: Coordinates, Charge, DFT-functional, & Basis-Set 
    * Output: Energy 
* Solvent Calculation: This is done in parallel to the optimization process and allows us to emulate the ground-state in a solution (water in our case). 
    * Program Name: [cosmoprep](cosmoprep.md) 
    * Input: Dielectric-constant of solution (Permittivity of solution)  
    * Output: Energy 
* Frequency Analysis: This computation finds the normal vibrational modes for each atom in a molecule which is used to compute various thermodynamic properties of a reaction (Gibbs-free energy & enthalpy). The vibrational spectra produced by this calculation can also be used to identify whether a model is presenting a transition-state or a true ground-state.  
    * Program Name: [freeh](frequency.md) 
    * Input: Temperature, Pressure, & Vibrational-spectrum from numerical calculation 
    * Output: Energy, Enthalpy, Gibbs-Free Energy, Entropy, & specific-heat 

## Turbomole Documentation

If you are interested in the Official Turbomole Documentation click [Here](https://www.turbomole.org/turbomole/turbomole-documentation/)