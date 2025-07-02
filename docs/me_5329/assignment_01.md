[:fontawesome-solid-house:](../index.md) :fontawesome-solid-angle-right: [ME 5329](index.md) :fontawesome-solid-angle-right: **Assignment 1**

# Assignment 1

![Assignment_1_Instructions.pdf](../pdfs/me_5329/Assignment_1_Instructions.pdf#toolbar=0&navpanes=0&scrollbar=0){ type=application/pdf style="min-height:100vh;width:100%" }

## create_ir_spectrum_plot.ipynb

Click the link to download the Jupyter notebook: [create_ir_spectrum_plot.ipynb](../files/me_5329/create_ir_spectrum_plot.ipynb){:create_ir_spectrum_plot.ipynb}

You may also copy the Python code below. The code is the same in both files.

```python title="create_ir_spectrum_plot.py"
import os
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

orca_out_filepath = os.path.join(os.getcwd(), "orca.out")
#read orca.out file and grab out IR Spectrum Section
reading = False
ir_spectrum_text = ""
with open(orca_out_filepath, "r") as file:
    for line in file:
        if "IR SPECTRUM\n" == line:
            reading = True
        if "--------------------------\n" == line:
            reading = False
            break
        if reading:
            ir_spectrum_text += line
ir_spectrum_text_list = ir_spectrum_text.split("\n")
#Filter through IR Spectrum section and get frequencies and intensities from the table
freq_list = list()
ints_list = list()
for row in ir_spectrum_text_list[6:-9]:
    split_row = row.split()
    freq_list.append(float(split_row[1]))
    ints_list.append(float(split_row[3]))

# Define a wavenumber range for plotting
x = np.linspace(300, 4000, 5000)

# Gaussian broadening
spectrum = np.zeros_like(x)
fwhm = 20  # adjust to simulate resolution (cm^-1)
sigma = fwhm / (2 * np.sqrt(2 * np.log(2)))  # convert FWHM to sigma

for freq, intensity in zip(freq_list, ints_list):
    spectrum += intensity * norm.pdf(x, freq, sigma)

# Plot
plt.figure(figsize=(8, 4))
plt.plot(x, spectrum, color='black')
plt.xlabel('Wavenumber (cm$^{-1}$)')
plt.ylabel('Intensity (km/mol)')
plt.title('Theoretical IR Spectrum for Molecule')
plt.xlim(4000, 300)  # IR spectra are conventionally plotted with decreasing wavenumber
plt.tight_layout()
plt.show()
```