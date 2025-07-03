[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Assignment 3**

# Assignment 3

![Assignment_3_Instructions.pdf](../assets/pdfs/me_5329/Assignment_3_Instructions.pdf#toolbar=0&navpanes=0&scrollbar=0){ type=application/pdf style="min-height:100vh;width:100%" }


## butane.xyz

Click the link to download the butane.xyz file: [butane.xyz](../assets/downloads/me_5329/butane.xyz){:butane.xyz}

You may also copy the .xyz file below.

```xyz title="butane.xyz"
14
Butane at 0 deg dihedral for ME 5329 Project 3 
C     0.000000    0.000000    0.000000
C    -1.528951    0.000073   -0.000042
C     0.605451   -0.000019    1.395212
C    -2.134394   -0.000051    1.395172
H     0.373159   -0.866008   -0.559027
H     0.347936    0.894003   -0.531125
H    -1.902109    0.866140   -0.558978
H    -1.876891   -0.893872   -0.531260
H     1.694633    0.090529    1.331830
H     0.229682    0.840789    1.986742
H     0.380954   -0.927652    1.929780
H    -1.758627   -0.840922    1.986612
H    -1.909891    0.927524    1.929837
H    -3.223578   -0.090588    1.331786

```

## create_water_pes_heatmap.ipynb

Click the link to download the Jupyter notebook: [create_water_pes_heatmap.ipynb](../assets/downloads/me_5329/create_water_pes_heatmap.ipynb){:create_water_pes_heatmap.ipynb}

You may also copy the Python code below. The code is the same in both files.

```python title="create_water_pes_heatmap.py"
import os
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


#EXAMPLE DATA
x = np.arange(0.8, 1.3, 0.1)  
y = np.arange(130, 89, -1)
X, Y = np.meshgrid(x, y) # This is necessary to create a 2d grid of the x and y values.
Z = np.sin(X*5) * np.cos(Y*0.1)
Z = Z - np.min(Z)


# YOUR DATA
x = np.arange(0.8, 1.3, 0.1)  
y = np.arange(130, 89, -1)
X, Y = np.meshgrid(x, y) # This is necessary to create a 2d grid of the x and y values.
Z = ? 
# you need to create the Z variable which is a 2d matrix of energy values that will be the "color" on the heatmap. Each matrix element will contain a relative energy water structure that its x,y index matches the x and y list index for bond angle and bond distance. Pandas may help you in the collecting of data and ordering it in a organized manner for the Z 2d matrix.


#GRAPHING CODE IS BELOW, YOU DO NOT NEED TO CHANGE THIS CELL other than the title

# Find the index of minimum Z
min_index = np.unravel_index(np.argmin(Z), Z.shape)

print("Heatmap shape:", Z.shape)
print("Minimum index (row, col):", min_index)

# Get corresponding x, y values
x_min = x[min_index[1]]  # col index → x-axis
y_min = y[min_index[0]]  # row index → y-axis
z_min = Z[min_index]

print(f"Lowest point: x={x_min:.3f}, y={y_min}, z={z_min:.3f}") #this prints out the lowest structure

# Plotting
plt.contourf(X, Y, Z, levels=50, cmap='jet')
plt.plot(x_min, y_min, c="gold", marker="*", markersize=15)
cbar = plt.colorbar()
cbar.set_label("$E_{relative}$ (kcal/mol)") 

plt.title("Assignment 3: ME 5329\nWater Potential Surface Example Graph")
plt.xlabel("O-H Bond Length (Å)")
plt.ylabel("H-O-H Bond Angle (°)")
plt.show()
```