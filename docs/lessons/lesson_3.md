[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Lessons](index.md) :fontawesome-solid-angle-right: **Lesson 3**

# Lesson 3 - Using Molecular Mechanics (MM) to Learn About Geometry Optimization

Written by Jeremy Schroeder.

## Introduction

Geometry Optimizations are the backbone of DFT calculations. It is the first calculation you initiate with a new system or with new initial conditions. Below will describe in short detail how a geometry optimization happens using a force field method, [AMBER94](https://ttu-primo.hosted.exlibrisgroup.com/permalink/f/1j33bpi/TN_cdi_proquest_miscellaneous_15853065). This is a simplification of how DFT programs actually optimize structures but I believe it is a good start to understanding how DFT actually works. The below information is found in the github repository [tmpchem/computational_chemistry](https://github.com/tmpchem/computational_chemistry).

## Optimization Process Flow

=== ":fontawesome-solid-house:"

    Click through to look at the broad overview for how a molecular mechanics geometry opitimization works.

=== "Main Flow"

    ``` mermaid
    flowchart TD
    A[Initial Setup Step] ---> B[Main Step]
    B ---> C[Check for Convergence]
    C -- If Convergence \nCriteria is met --> D[Finish Calculation]
    C -- If Convergence \nCriteria is not met --> B

    ```

=== "Initial Setup Step"

    1. Finds Energy
    1. Finds Gradient
    1. Makes Initial Trajectory
    1. Sets initial convergence criteria values

=== "Main Step"

    1. Choses Step Direction
    1. Line Search (Moves Atoms) (two methods, conjugate gradient and steepest direction)
    1. Finds New Energy
    1. Finds New Gradient
    1. Edits Trajectory
    1. Updates convergence criteria values

## How to Find Energy

=== ":fontawesome-solid-house:"

    Click through to look at the equations to find the total energy of the system that is used every iteration step. These equations originate from the AMBER94 paper.

=== "Total Energy"

    $E_{total} = E_{potential} + E_{kinetic}$

    $E_{total} = (E_{bonded} + {E_{non\:bonded}} + E_{boundary}) + E_{kinetic}$

    $E_{total} = ((E_{bond} + E_{angle} + E_{torsion} + E_{out\:of\:plane}) + (E_{van\:der\:waals} + {E_{electrostatic}}) + E_{boundary}) + E_{kinetic}$

=== "Potential Energy"

    <h3>$E_{potential} = E_{bonded} + {E_{non\:bonded}} + E_{boundary}$</h3>

=== "Bonded Energy"

    For each bond, the energies below are calculated:
        
    * If not noted, the argument is a float value.

    <h3>$E_{bond} = k_b * (r_{ij} - r_{eq})^2$</h3>
        
    Energy [kcal/mol] of bond ij.
        
    * $r_{ij}$ - Distance [Angstrom] between atoms i and j.
    * $r_{eq}$ - Equilibrium bond length [Angstrom] of bond ij.
    * $k_b$ - Spring constant [kcal/(mol*A^2)] of bond ij.
    
    <h3>$E_{angle} = k_a * ( \frac{\pi}{180} * (a_{ijk} - a_{eq}) )^2$</h3>
    
    Energy [kcal/mol] of angle ijk.

    * $a_{ijk}$ - Angle [degrees] between atoms i, j, and k.
    * $a_{eq}$ - Equilibrium bond angle [degrees] of angle ijk.
    * $k_a$ - Spring constant [kcal/(mol*rad^2)] of angle ijk.

    <h3>$E_{torsion} = v_n * \frac{1.0 + cos(\frac{\pi}{180} * (nfold*t_{ijkl} - \gamma))}{paths}$</h3>

    Energy [kcal/mol] of torsion ijkl.

    * $t_{ijkl}$ - Torsion [degrees] between atoms i, j, k, and l.
    * $v_n$ - Half-barrier height [kcal/mol] of torsion ijkl.
    * $\gamma$ - Barrier offset [degrees] of torsion ijkl.
    * $nfold$ - (int) Barrier frequency of torsion ijkl.
    * $paths$ - (int) Number of distinct paths in torsion ijkl.

    <h3>$E_{out\:of\:plane} = v_n * (1.0 + cos(\frac{\pi}{180} * (2.0 * o_{ijkl} - 180)))$</h3>

    Energy [kcal/mol] of outofplane ijkl.

    * $o_{ijkl}$ - Outofplane angle [degrees] between atoms i, j, k, and l.
    * $v_n$ - Half-barrier height [kcal/mol] of torsion ijkl.    

=== "Non Bonded Energy"
    
    For every atom pair, the energies below are calculated

    <h3>$E_{van\:der\:waals} = \epsilon_{ij} * ( r_{6ij}^2 - 2.0 * r_{6ij} )$</h3>
    
    Where $r_{6ij} = (r_{oij} / r_{ij})^6$
    
    Van der waals energy [kcal/mol] between pair ij.

    * $r_{ij}$ - Distance [Angstrom] between atoms i and j.
    * $\epsilon_{ij}$ - Van der Waals epsilon [kcal/mol] between pair ij.
    * $r_{oij}$ - Van der Waals radius [Angstrom] between pair ij.

    <h3>$E_{electrostatic} = \frac{332.06375 * q_i * q_j } {\epsilon * r_{ij}}$</h3>

    Electrostatic energy [kcal/mol] between pair ij.
    
    * $r_{ij}$ - Distance [Angstrom] between atoms i and j.
    * $q_i$ - Partial charge [e] of atom i.
    * $q_j$ - Partial charge [e] of atom j.
    * $\epsilon$ - Dielectric constant of space (>= 1.0).
    * 332.06375 is the conversion of electrostatic energy from [ceu] to [kcal/mol]. 

=== "Boundary energy"

    Calculate simulation boundary energy of an atom.

    <h3>$E_{boundary\:cubic} = k_{box} * (|n_{atom} - n_{origin}| - bound)^2$ where $n = x,y,z$</h3>

    For all atoms outside the boundary box,

    * $k_{box}$ - Spring constant [kcal/(mol*A^2)] of boundary.
    * $bound$ - Distance from origin [Angstrom] of boundary. Aka how large the boundary is.
    * $atom\:coords$ - Array of cartesian coordinates [Angstrom] of atom.
    * $origin\:coords$ - Array of cartesian coordiantes [Angstrom] of origin of simulation.

    <h3>$E_{boundary\:spherical} = k_{box} * (r_{io} - bound)**2$</h3>
    
    For all atoms outside the boudary sphere,
    
    * $r_{io}$ - 3d distance between origin and atom.
        * $r_{io} = \sqrt{(x_{atom} - x_{origin})^2 + (y_{atom} - y_{origin})^2 + (z_{atom} - z_{origin})^2}$
    * $k_{box}$ - Spring constant [kcal/(mol*A^2)] of boundary.
    * $bound$ - Distance from origin [Angstrom] of boundary. Aka how large the boundary is.

=== "Kinetic Energy"

    For every atom,

    <h3>$E_{kinetic} = mass_{atom} * n_{velocity}^2$ where $n = x,y,z$</h3>
    
    * $mass_{atom}$ - Mass [g/mol] of atom.
    * velocity - Array of velocities [Angstrom/ps] of atom.
        * Either you use the velocities of step n (default method) or an average of step n and step n-1 (leapfrog method).
    

=== "Equations in python code"

    Below are links to each equation in a python codebase.

    * Bonded Energy Consists of:
        * Bond Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L15)
        * Angle Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L29)
        * Torsion Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L43)
        * Out of Plane Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L59)
    * Non Bonded Energy Consists of:
        * Van der Waals Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L72)
        * Electrostatic Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L87)
    * Potential Energy consists of:
        * Bonded Energy
        * Non Bonded Energy
        * Bound Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L102)
    * Total Energy consists of:
        * Potential & Kinetic Energy [Source](https://github.com/tmpchem/computational_chemistry/blob/master/scripts/molecular_mechanics/mmlib/energy.py#L277)


## How to Find the Gradient and Convergence

=== ":fontawesome-solid-house:"

    Click through to look at the details of how the gradient is created and how a calculation finishes by convergence.


=== "Perturbation"

    Each atom is perturbed and moved in each axis direction (6 times) and the energy of the system is recorded for each pertubation.

    This in turn is calculating the Energy gradient or the first derivative of it.

    The picture below shows a potential energy surface for a water molecule with x axis being the H-O-H bond angle, y axis being 1 O-H bond length and z axis being the total energy of that particular structure.

    ![Gradient 2](../images/lessons/lesson_3/gradient_2.png)

=== "Finding the lowest energy"

    There are different techniques to do a search method on a 3d matrix such as conjugate gradient and steepest direction. We want to choose the perturbed structure that produces the lowest energy is a global minima not just a local minima.

    ![Gradient 1](../images/lessons/lesson_3/gradient_1.png)

=== "Steepest Direction"



=== "Conjugate Gradient"




=== "Convergence"

    After multiple optimization steps, if you compare the change in total energy and the displacement of each atom among other values. If the change is less than $10^-6$ (standard value) then the calculation is converged and it will stop.

    ![Convergence X](../images/lessons/lesson_3/convergence_X.jpg)


## Example Optimization


=== ":fontawesome-solid-house:"

    Lets look at an example optimization.

=== "Two Initial Guess Geometries"

    I 

=== "Bond Angle vs. H-O Distance"

    <div class="grid">
    ![Graph 1](../images/lessons/lesson_1/xyz_file1.png)
    ![Graph 2](../images/lessons/lesson_1/xyz_file2.png)
    </div>

=== "Gradient Files"

    Left is Linear, Right is Bent

    <div class="grid">
    ```
    $grad          cartesian gradients
    cycle =      1    SCF energy =      -76.0342679285   |dE/dxyz| =  0.163929
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      2.83458918693865      h
        0.00000000000000      0.00000000000000     -2.83458918693865      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.11591534585240D+00
    0.00000000000000D+00  0.00000000000000D+00  -.11591534585240D+00
    cycle =      2    SCF energy =      -76.0596732050   |dE/dxyz| =  0.174584
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      2.72852316976067      h
        0.00000000000000      0.00000000000000     -2.72852316976067      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.12344954946510D+00
    0.00000000000000D+00  0.00000000000000D+00  -.12344954946510D+00
    cycle =      3    SCF energy =      -76.1018958862   |dE/dxyz| =  0.187963
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      2.56420640250912      h
        0.00000000000000      0.00000000000000     -2.56420640250912      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.13290982031451D+00
    0.00000000000000D+00  0.00000000000000D+00  -.13290982031451D+00
    cycle =      4    SCF energy =      -76.1596051298   |dE/dxyz| =  0.193897
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      2.35207436815316      h
        0.00000000000000      0.00000000000000     -2.35207436815316      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.13710563521874D+00
    0.00000000000000D+00  0.00000000000000D+00  -.13710563521874D+00
    cycle =      5    SCF energy =      -76.2157454303   |dE/dxyz| =  0.174690
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      2.13994233379720      h
        0.00000000000000      0.00000000000000     -2.13994233379720      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.12352457383284D+00
    0.00000000000000D+00  0.00000000000000D+00  -.12352457383284D+00
    cycle =      6    SCF energy =      -76.2595733307   |dE/dxyz| =  0.106472
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.92781029944124      h
        0.00000000000000      0.00000000000000     -1.92781029944124      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.75286839099578D-01
    0.00000000000000D+00  0.00000000000000D+00  -.75286839099578D-01
    cycle =      7    SCF energy =      -76.2702771677   |dE/dxyz| =  0.056687
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.71567826508528      h
        0.00000000000000      0.00000000000000     -1.71567826508528      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  -.40083718067586D-01
    0.00000000000000D+00  0.00000000000000D+00  0.40083718067586D-01
    cycle =      8    SCF energy =      -76.2722751113   |dE/dxyz| =  0.015156
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.78938026381887      h
        0.00000000000000      0.00000000000000     -1.78938026381887      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.10716639972244D-01
    0.00000000000000D+00  0.00000000000000D+00  -.10716639972244D-01
    cycle =      9    SCF energy =      -76.2724601684   |dE/dxyz| =  0.001564
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.77383238549401      h
        0.00000000000000      0.00000000000000     -1.77383238549401      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.11058002061091D-02
    0.00000000000000D+00  0.00000000000000D+00  -.11058002061091D-02
    cycle =     10    SCF energy =      -76.2724620679   |dE/dxyz| =  0.000046
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.77204348385007      h
        0.00000000000000      0.00000000000000     -1.77204348385007      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  -.32185184110745D-04
    0.00000000000000D+00  0.00000000000000D+00  0.32185184110745D-04
    cycle =     11    SCF energy =      -76.2724620769   |dE/dxyz| =  0.000001
        0.00000000000000      0.00000000000000      0.00000000000000      o
        0.00000000000000      0.00000000000000      1.77209407863737      h
        0.00000000000000      0.00000000000000     -1.77209407863737      h
    0.00000000000000D+00  0.00000000000000D+00  0.00000000000000D+00
    0.00000000000000D+00  0.00000000000000D+00  0.92775614040734D-06
    0.00000000000000D+00  0.00000000000000D+00  -.92775614040734D-06
    $end

    ```
    ``` 
    $grad          cartesian gradients
    cycle =      1    SCF energy =      -76.1347138816   |dE/dxyz| =  0.216399
        0.00000000000000      0.00000000000000     -1.33623815730826      o
    -2.00435723596239      0.00000000000000      0.66811907865413      h
        2.00435723596239      0.00000000000000      0.66811907865413      h
    0.00000000000000D+00  0.00000000000000D+00  -.15371733855228D+00
    -.75477380628687D-01  0.00000000000000D+00  0.76830655553477D-01
    0.75477380628687D-01  0.00000000000000D+00  0.76830655553477D-01
    cycle =      2    SCF energy =      -76.1675265527   |dE/dxyz| =  0.220386
        0.00000000000000      0.00000000000000     -1.22969984449440      o
    -1.95203906581968      0.00000000000000      0.61484992224720      h
        1.95203906581968      0.00000000000000      0.61484992224720      h
    0.00000000000000D+00  0.00000000000000D+00  -.15308474743820D+00
    -.81925569931974D-01  0.00000000000000D+00  0.76522365091220D-01
    0.81925569931974D-01  0.00000000000000D+00  0.76522365091220D-01
    cycle =      3    SCF energy =      -76.2185166712   |dE/dxyz| =  0.215606
        0.00000000000000      0.00000000000000     -1.07129348121312      o
    -1.86159257305167      0.00000000000000      0.53564674060656      h
        1.86159257305167      0.00000000000000      0.53564674060656      h
    0.00000000000000D+00  0.00000000000000D+00  -.14288670976270D+00
    -.89053162213362D-01  0.00000000000000D+00  0.71443003123186D-01
    0.89053162213362D-01  0.00000000000000D+00  0.71443003123186D-01
    cycle =      4    SCF energy =      -76.2783872549   |dE/dxyz| =  0.175003
        0.00000000000000      0.00000000000000     -0.87701985220224      o
    -1.73238995000087      0.00000000000000      0.43850992610112      h
        1.73238995000087      0.00000000000000      0.43850992610112      h
    0.00000000000000D+00  0.00000000000000D+00  -.10397104877942D+00
    -.84885712092734D-01  0.00000000000000D+00  0.51985627775374D-01
    0.84885712092734D-01  0.00000000000000D+00  0.51985627775374D-01
    cycle =      5    SCF energy =      -76.3159623408   |dE/dxyz| =  0.060638
        0.00000000000000      0.00000000000000     -0.70332981988096      o
    -1.58281110957128      0.00000000000000      0.35166490994048      h
        1.58281110957128      0.00000000000000      0.35166490994048      h
    0.00000000000000D+00  0.00000000000000D+00  -.17922348819494D-01
    -.39969834075857D-01  0.00000000000000D+00  0.89591488223048D-02
    0.39969834075857D-01  0.00000000000000D+00  0.89591488223048D-02
    cycle =      6    SCF energy =      -76.3176797903   |dE/dxyz| =  0.069593
        0.00000000000000      0.00000000000000     -0.64839020814579      o
    -1.47666834594709      0.00000000000000      0.32419510407290      h
        1.47666834594709      0.00000000000000      0.32419510407290      h
    0.00000000000000D+00  0.00000000000000D+00  0.53161274481013D-01
    0.17373981638171D-01  0.00000000000000D+00  -.26582949687105D-01
    -.17373981638171D-01  0.00000000000000D+00  -.26582949687105D-01
    cycle =      7    SCF energy =      -76.3201811000   |dE/dxyz| =  0.019796
        0.00000000000000      0.00000000000000     -0.69705865799665      o
    -1.50059541673130      0.00000000000000      0.34852932899833      h
        1.50059541673130      0.00000000000000      0.34852932899833      h
    0.00000000000000D+00  0.00000000000000D+00  0.11804823085072D-01
    -.95577394813818D-02  0.00000000000000D+00  -.59086095256087D-02
    0.95577394813818D-02  0.00000000000000D+00  -.59086095256087D-02
    cycle =      8    SCF energy =      -76.3208794990   |dE/dxyz| =  0.013103
        0.00000000000000      0.00000000000000     -0.72222671697600      o
    -1.47912469960123      0.00000000000000      0.36111335848800      h
        1.47912469960123      0.00000000000000      0.36111335848800      h
    0.00000000000000D+00  0.00000000000000D+00  0.45270136763901D-02
    -.83930225197870D-02  0.00000000000000D+00  -.22692931950739D-02
    0.83930225197870D-02  0.00000000000000D+00  -.22692931950739D-02
    cycle =      9    SCF energy =      -76.3214031408   |dE/dxyz| =  0.004152
        0.00000000000000      0.00000000000000     -0.76097424664092      o
    -1.43256977376970      0.00000000000000      0.38048712332046      h
        1.43256977376970      0.00000000000000      0.38048712332046      h
    0.00000000000000D+00  0.00000000000000D+00  -.28446928249342D-02
    -.16030338863389D-02  0.00000000000000D+00  0.14162429448356D-02
    0.16030338863389D-02  0.00000000000000D+00  0.14162429448356D-02
    cycle =     10    SCF energy =      -76.3214124086   |dE/dxyz| =  0.000510
        0.00000000000000      0.00000000000000     -0.75800719327388      o
    -1.43132051238261      0.00000000000000      0.37900359663694      h
        1.43132051238261      0.00000000000000      0.37900359663694      h
    0.00000000000000D+00  0.00000000000000D+00  -.31697586547436D-03
    -.23729936771934D-03  0.00000000000000D+00  0.15265473113057D-03
    0.23729936771932D-03  0.00000000000000D+00  0.15265473113057D-03
    cycle =     11    SCF energy =      -76.3214125819   |dE/dxyz| =  0.000008
        0.00000000000000      0.00000000000000     -0.75782366494463      o
    -1.43084805415747      0.00000000000000      0.37891183247231      h
        1.43084805415747      0.00000000000000      0.37891183247231      h
    0.00000000000000D+00  0.00000000000000D+00  -.43526811906157D-05
    0.27302497020015D-05  0.00000000000000D+00  -.36308920330075D-05
    -.27302497020154D-05  0.00000000000000D+00  -.36308920330075D-05
    $end

    ```
    </div>

## Recap

A geometry optimization is an iterative process that takes an initial structure, then calculates the total energy of the structure and the energy gradient and iterates on the structure until the total energy converges to a stable value. For DFT calculations, the energy calculation step is more complicated but the main idea of finding a gradient and the structure changing is the same. Check out [Assignment 2](assignment_2.md) if you are interested in understanding more about an optimization and creating a Potential Energy Surface (PES).