[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [Lessons](index.md) :fontawesome-solid-angle-right: **Lesson 4**
# Lesson 4 - Details on DFT Geometry Optimization

Written by Jeremy Schroeder

## Introduction

As seen in the previous lesson, calculating the energy of the structure and optimization of structures is complicated. I used the Molecular Mechanics (MM) example to show equations and hopefully have a more sinplified understanding of the logic because as you increase the level of theory, the complicatedness and logic become more abstract. To understand every inner logic and workings of DFT would take years of math, quantum mechanics and chemistry classes to truly understand. So In this lesson I will show an example and particular steps of how DFT works.

## Pauli-Exclusion Principle

How electrons are assigned in each orbital. 



## Calculated Orbital Energies and Locations

=== ":fontawesome-solid-house:"

    Click through to see each orbital energy of a water molecule that the program Orca found. These pictures are from the visulization program JMol and you can also use Molden or GaussView to see orbitals visualized.

    Try to identify the LUMO (Lowest Unoccupied Molecular Orbital) and the HOMO (Highest Occupied Molecular Orbital). You can also find the Energy Gap which is the equation below.

    $E_{gap} = LUMO - HOMO$

    When looking at the pictures, the Red atom is Oxygen, the White atoms are Hydrogens, the red transparent cloud is the "positive" orbitals and the blue transparent cloud are the "negative" orbitals.
        
    * The reason "positive" and "negative" are in quotations is that it's really two electrons that have opposite spin of each other and are not attracted to each other. Think like spin-up and spin-down.
    
    This website linked below goes into more details about the orbitals a water molecule has. 

    * [https://water.lsbu.ac.uk/water/h2o_orbitals.html](https://water.lsbu.ac.uk/water/h2o_orbitals.html)
        

=== "Orbital 01"

    <div class="grid">
    ![011](../images/lessons/lesson_4/mo/011.jpg)
    ![012](../images/lessons/lesson_4/mo/012.jpg)
    ![013](../images/lessons/lesson_4/mo/013.jpg)
    </div>

=== "Orbital 02"

    <div class="grid">
    ![021](../images/lessons/lesson_4/mo/021.jpg)
    ![022](../images/lessons/lesson_4/mo/022.jpg)
    ![023](../images/lessons/lesson_4/mo/023.jpg)
    </div>

=== "Orbital 03"

    <div class="grid">
    ![031](../images/lessons/lesson_4/mo/031.jpg)
    ![032](../images/lessons/lesson_4/mo/032.jpg)
    ![033](../images/lessons/lesson_4/mo/033.jpg)
    </div>

=== "Orbital 04"

    <div class="grid">
    ![041](../images/lessons/lesson_4/mo/041.jpg)
    ![042](../images/lessons/lesson_4/mo/042.jpg)
    ![043](../images/lessons/lesson_4/mo/043.jpg)
    </div>

=== "Orbital 05"

    <div class="grid">
    ![051](../images/lessons/lesson_4/mo/051.jpg)
    ![052](../images/lessons/lesson_4/mo/052.jpg)
    ![053](../images/lessons/lesson_4/mo/053.jpg)
    </div>

=== "Orbital 06"

    <div class="grid">
    ![061](../images/lessons/lesson_4/mo/061.jpg)
    ![062](../images/lessons/lesson_4/mo/062.jpg)
    ![063](../images/lessons/lesson_4/mo/063.jpg)
    </div>

=== "Orbital 07"

    <div class="grid">
    ![071](../images/lessons/lesson_4/mo/071.jpg)
    ![072](../images/lessons/lesson_4/mo/072.jpg)
    ![073](../images/lessons/lesson_4/mo/073.jpg)
    </div>

=== "Orbital 08"

    <div class="grid">
    ![081](../images/lessons/lesson_4/mo/081.jpg)
    ![082](../images/lessons/lesson_4/mo/082.jpg)
    ![083](../images/lessons/lesson_4/mo/083.jpg)
    </div>

=== "Orbital 09"

    <div class="grid">
    ![091](../images/lessons/lesson_4/mo/091.jpg)
    ![092](../images/lessons/lesson_4/mo/092.jpg)
    ![093](../images/lessons/lesson_4/mo/093.jpg)
    </div>

=== "Orbital 10"

    <div class="grid">
    ![101](../images/lessons/lesson_4/mo/101.jpg)
    ![102](../images/lessons/lesson_4/mo/102.jpg)
    ![103](../images/lessons/lesson_4/mo/103.jpg)
    </div>

=== "Orbital 11"

    <div class="grid">
    ![111](../images/lessons/lesson_4/mo/111.jpg)
    ![112](../images/lessons/lesson_4/mo/112.jpg)
    ![113](../images/lessons/lesson_4/mo/113.jpg)
    </div>

=== "Orbital 12"

    <div class="grid">
    ![121](../images/lessons/lesson_4/mo/121.jpg)
    ![122](../images/lessons/lesson_4/mo/122.jpg)
    ![123](../images/lessons/lesson_4/mo/123.jpg)
    </div>

=== "Orbital 13"

    <div class="grid">
    ![131](../images/lessons/lesson_4/mo/131.jpg)
    ![132](../images/lessons/lesson_4/mo/132.jpg)
    ![133](../images/lessons/lesson_4/mo/133.jpg)
    </div>

=== "Orbital 14"

    <div class="grid">
    ![141](../images/lessons/lesson_4/mo/141.jpg)
    ![142](../images/lessons/lesson_4/mo/142.jpg)
    ![143](../images/lessons/lesson_4/mo/143.jpg)
    </div>

=== "Orbital 15"

    <div class="grid">
    ![151](../images/lessons/lesson_4/mo/151.jpg)
    ![152](../images/lessons/lesson_4/mo/152.jpg)
    ![153](../images/lessons/lesson_4/mo/153.jpg)
    </div>

=== "Orbital 16"

    <div class="grid">
    ![161](../images/lessons/lesson_4/mo/161.jpg)
    ![162](../images/lessons/lesson_4/mo/162.jpg)
    ![163](../images/lessons/lesson_4/mo/163.jpg)
    </div>
                                                        
=== "Orbital 17"

    <div class="grid">
    ![171](../images/lessons/lesson_4/mo/171.jpg)
    ![172](../images/lessons/lesson_4/mo/172.jpg)
    ![173](../images/lessons/lesson_4/mo/173.jpg)
    </div>
    
=== "Orbital 18"

    <div class="grid">
    ![181](../images/lessons/lesson_4/mo/181.jpg)
    ![182](../images/lessons/lesson_4/mo/182.jpg)
    ![183](../images/lessons/lesson_4/mo/183.jpg)
    </div>
    
=== "Answers"

    HOMO is Orbital 5, with energy -0.28665087 H
    LUMO is Orbital 6, with energy 0.068232216 H
    So $E_{gap} = 0.354883086$ H