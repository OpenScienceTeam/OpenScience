---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'

title: MOF Book Example Chapter 1 (Basics)
---

> This chapter introduces the basic concepts of MOFs and demonstrates fundamental features and formatting.

# Chapter 1: Basic Concepts and Structure of MOFs

## 1.1 What is a MOF?

A Metal–Organic Framework (MOF) is a class of porous crystalline material constructed from **metal nodes** and **organic linkers**.

:::{tip} History of MOFs
The explosive growth of the MOF field began in the late 1990s, with pioneering contributions from Professor Omar Yaghi.
:::

- Metal nodes: Typically metal ions or clusters (such as Zn²⁺, Cu²⁺, Zr⁴⁺, etc.)
- Organic linkers: Multidentate ligands containing carboxyl, pyridyl, or other coordinating groups
- Features: Exceptionally high specific surface area, tunable structure, and versatile functionalization

:::{hint}
You can imagine a MOF as a three-dimensional framework where "metal atoms are the nodes and organic molecules are the struts."
:::


> The main characteristics of MOF materials are their **extremely high specific surface area** and **tunable pore structures**. You can think of them as nano-sized Lego blocks.


As shown in the literature [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8)[^1]

[^1]: This is a review about AI for MOFs.

---


(target-struct)=
## 1.2 Typical Structure Illustration and Unit Cell

%(target-struct)=   This part is used for cross-reference linking

### 1.2.1 Structure Illustration

:::{figure} ../images/Figure-1.png
:name: fig-mof-schematic
:width: 60%
:align: center
A schematic diagram of a MOF structure.
:::

## 1.3 Simple Crystallographic Expressions

Below are formulas describing the basic cell size and porosity of a MOF framework.

### 1.3.1 Volume and Porosity

Unit cell volume:

$$
V_{\text{cell}} = a \cdot b \cdot c \cdot \sqrt{
1 + 2\cos\alpha\cos\beta\cos\gamma \cos^2\alpha - \cos^2\beta - \cos^2\gamma
}
$$

If the void volume of a MOF, $V_{\text{void}}$, is obtained via molecular simulation or adsorption experiments, the porosity $\phi$ can be expressed as:

$$
\phi = \frac{V_{\text{void}}}{V_{\text{cell}}}
$$

:::{admonition} Discussion
Why do MOFs generally have a higher degree of designability than traditional porous materials such as activated carbon or silica gel?
:::

## 1.4 Table: Some Typical MOFs

:::{table}
:name: tab-common-mofs
:align: center

| Name        | Metal Center | Organic Linker                | Features                      |
|-------------|--------------|-------------------------------|-------------------------------|
| MOF-5       | Zn²⁺         | 1,4-benzenedicarboxylate (BDC)| Early classic MOF, high surface area    |
| UiO-66      | Zr⁴⁺         | BDC                           | Excellent thermal/chemical stability    |
| HKUST-1     | Cu²⁺         | 1,3,5-benzenetricarboxylate (BTC)| Classic copper-based MOF               |
| MIL-101(Cr) | Cr³⁺         | BDC                           | Extra-large pore volume, good water stability |
:::

## 1.5 Describing MOFs with Python Code

% This is a non-visible comment: The following code block will not be executed as a code cell.

:::{code} python
def describe_mof(name, metal, linker):
    return f"{name} is a MOF with {metal} as the metal center and {linker} as the organic linker."

print(describe_mof("UiO-66", "Zr⁴⁺", "BDC"))
:::

The above is a Python code example for MOF description, using the `describe_mof` function.



## 1.6 Calculating the Relationship Between Porosity and Pore Volume in Python

% The following code block will be executed as a code cell, and the display can be controlled by modifying :tags:.

:::{code-cell} python
:tags: [hide-input]

import math

def pore_volume(cube_length_nm, void_fraction):
    """
    Simple cubic model.
    cube_length_nm: cell edge length (nm)
    void_fraction: porosity (void fraction)
    Returns pore volume (nm^3)
    """
    v_cell = cube_length_nm**3
    return v_cell * void_fraction

for phi in [0.3, 0.5, 0.8]:
    print(f"Porosity {phi:.1f} -> Pore volume: {pore_volume(2.5, phi):.2f} nm^3")
:::


## 1.7 Simple 2D Plot Example

:::{code-cell}python

import numpy as np
import matplotlib.pyplot as plt

phis = np.linspace(0.1, 0.9, 9)
surface_area = 1500 * phis * 2  # Hypothetical relation

plt.figure()
plt.plot(phis, surface_area, marker="o")
plt.xlabel("Porosity φ")
plt.ylabel("Surface Area (m²/g)")
plt.title("Simple Relationship Between Porosity and Surface Area")
plt.grid(True)
plt.show()
:::

## 1.8 Exercise Zone (task list)

:::{exercise} 1. calculate the porosity
- Manually calculate the porosity of a simple MOF.
:::

:::{exercise} 2. Find MOF
- Find the structural information of a MOF you are interested in.
:::

:::{exercise} 3. Visualize a structure
- Try visualizing a CIF file using pymatgen or ASE.
:::