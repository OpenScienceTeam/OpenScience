---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'

title: Author Template - 1. Basics
abstract:
  Contains examples of all basic _MyST markdown_ syntax
---

# Writing Syntax Section

This file demonstrates all the main syntax of MyST Markdown (MyST v2).  
All examples are adapted using the MOF (Metal–Organic Framework) theme,  
and the latest recommended `:::` fenced directive syntax is adopted throughout.

Authors can directly copy these templates and modify the content. Each section includes an official documentation link with more extensible functions.

---

## 0. Document (Frontmatter)

[Frontmatter Documents](https://mystmd.org/guide/frontmatter)

Place this at the very beginning of each markdown file. Below is a sample for this tutorial.

```
---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'

title: Author Template - 1. Basics
abstract:
  Contains examples of all basic _MyST markdown_ syntax
---
```

_kernelspec_: Specifies the local jupyter execution environment for interactive Python code blocks.

_title_: The title of the chapter, shown in the table of contents in the left sidebar.

_abstract_: A brief introduction to the chapter.

---

## 1. Typography

[Typography Document](https://mystmd.org/guide/typography)

### 1.0 


### 1.1 Emphasis and Inline Formatting

Regular text  
```**Bold Text**  ``` **Bold Text**  
```*Italic Text*  ``` *Italic Text*  
```***Bold Italic***  ``` ***Bold Italic***  

Showcase of ``` `inline code` ```.  Example: `inline code` part.

---

### 1.2 Block Quote

```> MOF-5 consists of **Zn₄O** secondary building units (SBUs) and *benzene dicarboxylate ligands (BDC)*.  ```
> MOF-5 consists of **Zn₄O** secondary building units (SBUs) and *benzene dicarboxylate ligands (BDC)*.

---

### 1.3 Horizontal Rule

```---```

---

### 1.4 Footnotes

As shown in the following reference[^1]

[^1]: This is a review about AI for MOFs.

```
As shown in the following reference[^1]

[^1]: This is a review about AI for MOFs.
```

(The Footnotes section at the bottom will show the footnote content.)

---

## 2. Admonitions

[Callouts & Admonitions Documents](https://mystmd.org/guide/admonitions)

The latest MyST recommendation is to use:

```
:::{type}
Content
:::
```

Available types:  
- note  
- tip  
- important  
- warning  
- admonition  

---

### 2.1 tip

```
:::{tip} What is coordination polymerization?
MOFs are essentially crystalline frameworks formed by metal ions and multidentate organic ligands through coordination bonds.
:::
```

:::{tip} What is coordination polymerization?
MOFs are essentially crystalline frameworks formed by metal ions and multidentate organic ligands through coordination bonds.
:::

---

### 2.2 note

```
:::{note}
UiO-66 is one of the most stable and widely used Zr-based MOF structures.
:::
```
:::{note}
UiO-66 is one of the most stable and widely used Zr-based MOF structures.
:::

---

### 2.3 warning

```
:::{warning}
HKUST-1 is prone to hydrolysis in humid environments, resulting in structural collapse.
:::
```

:::{warning}
HKUST-1 is prone to hydrolysis in humid environments, resulting in structural collapse.
:::

---

### 2.4 General admonition

```
:::{admonition} Custom Block Title
Content...
:::
```

:::{admonition} Notes on MOF Modeling
Before performing MOF molecular simulations, check whether the crystal structure has defects, incomplete coordination, or solvent residue.
:::

---

## 3. Figures

[Figures Documents](https://mystmd.org/guide/figures)

MyST recommends using the fenced directive:
```
:::{figure} path/to/image
:name: image-label   
:width: 70%
:align: center
Figure Caption  (If the :name: tag is not added, the caption will not be automatically numbered as Figure N)
:::
```

### 3.1 Local Images

:::{figure} ../images/Figure-1.png
:name: MOF-structure
:width: 70%
:align: center
Schematic diagram of MOF structure.
:::

---

### 3.2 Web Images

:::{figure} https://upload.wikimedia.org/wikipedia/commons/1/1d/MIL101_synthesis.png
:name: Wiki-MOF
:width: 60%
:align: center
Structure diagram of MIL-101 (Wikimedia).
:::

---

## 4. Math

[Math and Equation Documents](https://mystmd.org/guide/math)

MyST supports all LaTeX math syntax.

### 4.1 Inline Formulas

The porosity of a MOF can be written as $\phi = V_\text{void} / V_\text{cell}$.

`$\phi = V_\text{void} / V_\text{cell}$`

---

### 4.2 Block Formulas

```
$$
V_\text{cell} = abc\sqrt{
1 + 2\cos\alpha\cos\beta\cos\gamma -
\cos^2\alpha - \cos^2\beta - \cos^2\gamma
}
$$
```

$$
V_\text{cell} = abc\sqrt{
1 + 2\cos\alpha\cos\beta\cos\gamma -
\cos^2\alpha - \cos^2\beta - \cos^2\gamma
}
$$

```
$$
\begin{aligned}
q(P) &= q_{\max} \frac{bP}{1 + bP} \\
\phi &= \frac{V_\text{void}}{V_\text{cell}}
\end{aligned}
$$
```

$$
\begin{aligned}
q(P) &= q_{\max} \frac{bP}{1 + bP} \\
\phi &= \frac{V_\text{void}}{V_\text{cell}}
\end{aligned}
$$

---

## 5. Tables

[Tables Documents](https://mystmd.org/guide/tables)

### 5.1 Standard Markdown Table

```
| Name | Metal Center | Ligand | Feature |
| :--- | :--- | :--- | :--- |
| MOF-5 | $\mathrm{Zn}^{2+}$ | BDC | Classic MOF |
| UiO-66 | $\mathrm{Zr}^{4+}$ | BDC | Exceptional Stability |
```

| Name | Metal Center | Ligand | Feature |
| :--- | :--- | :--- | :--- |
| MOF-5 | $\mathrm{Zn}^{2+}$ | BDC | Classic MOF |
| UiO-66 | $\mathrm{Zr}^{4+}$ | BDC | Exceptional Stability |

---

### 5.2 Block Table

```
:::{table} Table caption
:label: table
:align: center
| head | head |
| --- | --- |
| content | content |
:::
```

:::{table}
:label: table
:align: center
|Structure| BET Surface Area (m²/g)|
| --- | --- |
|MOF-5|3800|
|MIL-101|4500|
:::

---

## 6. Cross References

[Cross Reference Documents](https://mystmd.org/guide/cross-references)

You can add a :name: to any block and reference it.

```
In Section2, cite the figure as:

:::{figure} ../images/Figure-1.png
:name: MOF-structure
:width: 70%
:align: center
Schematic diagram of MOF structure.
:::
```

`See [](#MOF-structure).`

See [](#MOF-structure).

`[Section 1.2 Typical Structures and Unit Cells in Chapter 1](./ch1-mof-basics#target-struct).`

[Section 1.2 Typical Structures and Unit Cells in Chapter 1](./ch1-mof-basics#target-struct).

---

## 7. External References

Websites like wiki and github can be referenced directly:

```<wiki:Metal–organic_framework>```

<wiki:Metal–organic_framework>

Other external references:

```[External Reference Documents](https://mystmd.org/guide/external-references)```

[External Reference Documents](https://mystmd.org/guide/external-references)

---

## 8. Embedding

[Embedding Documents]

You can embed content from this document or other documents. For example, to embed Figure 1 from Chapter 1 of the MOF-book:

```
:::{embed} ch1-mof-basics.md/#fig-mof-schematic
:::
```

:::{embed} ch1-mof-basics.md/#fig-mof-schematic
:::


---

## 9. Citations

[Citation Documents](https://mystmd.org/guide/citations)

Use DOI to cite:

Citation example:

```[MOF paper](doi.org/10.1038/s41578-025-00772-8)```

[MOF paper](doi.org/10.1038/s41578-025-00772-8)

Repeated citation:

```[MOF paper](doi.org/10.1038/s41578-025-00772-8)```

[MOF paper](doi.org/10.1038/s41578-025-00772-8)

```As shown in [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8).```

As shown in [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8).

(No repeated reference will show in the References section at the end if the same DOI is cited multiple times.)

---

## 10. Proofs and Theorems

[Theorems Documents](https://mystmd.org/guide/proofs-and-theorems)

You can add theorems, definitions, proofs, etc. by using `{prf:keyword}`, where keyword may be theorem, lemma, definition, etc.

```
:::{prf:theorem} Stability Criterion for MOFs
:label: theorem-1
MOFs are generally more stable if the coordination number of the metal node is sufficiently high.
:::

:::{prf:proof} Proof
:label: proof-theorem-1
A high coordination number restricts the degrees of freedom of the framework structure, thereby increasing its stability.
:::
```

:::{prf:theorem} Stability Criterion for MOFs
:label: theorem-1
MOFs are generally more stable if the coordination number of the metal node is sufficiently high.
:::

:::{prf:proof} Proof
:label: proof-theorem-1
A high coordination number restricts the degrees of freedom of the framework structure, thereby increasing its stability.
:::


---

## 11. Exercises

[Exercise Documents](https://mystmd.org/guide/exercises)

```
:::{exercise} 
:label: my-exercise
Porosity Exercise
Calculate the unit cell volume of a simple cubic cell with an edge length of 3 nm and a porosity of 0.5.
:::
```

:::{exercise} 
:label: my-exercise
Porosity Exercise
Calculate the unit cell volume of a simple cubic cell with an edge length of 3 nm and a porosity of 0.5.
:::


```
:::{solution} my-exercise
$V = 27\text{ nm}^3$.
:::
```
:::{solution} my-exercise
$V = 27\text{ nm}^3$.
:::

*Note*: use a label for exercise, and the corresponding label for solution.

---

## 12. Blocks and Comments

[Blocks and Comments Documents](https://mystmd.org/guide/blocks)

### 12.1 Blocks

Blocks are used to segment formatting:

```
+++ {"cell": "one"}
cell 1
```
+++ {"cell": "one"}
cell 1

### 12.2 Comments

Comments are used to add annotations within code.

```
This next line won't render, but it is in the HTML and LaTeX!
% Markdown comment line
```

This next line won't render, but it is in the HTML and LaTeX!
% Markdown comment line

---

## 13. Diagrams

Flowcharts and similar structures are supported and it is recommended to use Mermaid diagrams.

[Diagram Documents](https://mystmd.org/guide/diagrams)

[Mermaid Official Documents](https://mermaid.js.org/)

```
:::{mermaid} 
graph TD
    A[Metal Node] --> B[Ligand]
    B --> C[3D Network]
:::
```

:::{mermaid} 
graph TD
    A[Metal Node] --> B[Ligand]
    B --> C[3D Network]
:::

---

## 14. Asides

[Asides and Margin Documents](https://mystmd.org/guide/asides)

Used for sidenotes, which will appear in the right sidebar:
```
:::{aside}
ZIF series materials exhibit outstanding performance in gas separation.
:::
```

:::{aside}
ZIF series materials exhibit outstanding performance in gas separation.
:::


---

## 15. Dropdowns, Cards, Tabs

[Dropdowns, Cards, Tabs Documents](https://mystmd.org/guide/dropdowns-cards-and-tabs)

### 15.1 Dropdown

```
:::{dropdown} Click to Expand MOF Description
MOFs are porous materials consisting of metal nodes and organic ligands.
:::
```

:::{dropdown} Click to Expand MOF Description
MOFs are porous materials consisting of metal nodes and organic ligands.
:::

---

### 15.2 Tabs

```
::::{tab-set}

:::{tab-item} Structure
MOF frameworks rely on metal nodes and organic linkers.
:::

:::{tab-item} Pores
Pore size determines adsorption selectivity.
:::

::::
```

::::{tab-set}

:::{tab-item} Structure
MOF frameworks rely on metal nodes and organic linkers.
:::

:::{tab-item} Pores
Pore size determines adsorption selectivity.
:::

::::

---

## 16. Glossaries and Terms

[Glossaries Documents](https://mystmd.org/guide/glossaries-and-terms)

```
:::{glossary}

MOF
: Metal–Organic Framework

SBU
: Secondary Building Unit

:::
```

:::{glossary}

MOF
: Metal–Organic Framework

SBU
: Secondary Building Unit

:::

---

