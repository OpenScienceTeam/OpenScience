---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
title: MOF Book 写作者模板
abstract:
  包含所有 _MyST markdown_ 语法示例
---


# 写作语法部分

本文件示例展示 MyST Markdown（MyST v2）的全部主要语法，  
所有示例都使用 MOF（金属有机骨架）主题进行改写，  
并全部采用最新推荐的 `:::` 块指令语法（fenced directives）。

写作者可直接复制这些模板并改写内容，每个部分后面配有官方格式教程链接，包含更多可扩展的功能。

---

## 0. Document (页面前部)

放置在每个markdown文件最开头，以下是本教程的示例。

```
---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
title: MOF Book 写作者模板
abstract:
  包含所有 _MyST markdown_ 语法示例
---
```

_kernelspec_: 内容为交互python块的jupyter执行环境。
_title_: 本章的标题，显示在左边栏的内容大纲中
_abstract_: 本章的简介 

---

## 1. Typography（排版示例）

[Typography Document](https://mystmd.org/guide/typography)

### 1.1 强调与行内格式

普通文本  
```**加粗文本**  ``` **加粗文本**  
```*斜体文本*  ``` *斜体文本*  
```***粗斜体***  ``` ***粗斜体***  

展示``` `行内代码` ```部分。  展示`行内代码`部分。 


---

### 1.2 引用块（Block Quote）

```> MOF-5 由 **Zn₄O** 次级构筑单元（SBU）与 *对苯二甲酸配体（BDC）* 组成。  ```
> MOF-5 由 **Zn₄O** 次级构筑单元（SBU）与 *对苯二甲酸配体（BDC）* 组成。  

---

### 1.3 水平线

```---```

---

### 1.4 脚注

如Zach的文献所示[^1]

[^1]: This is a review about AI for MOFs.

```
如Zach的文献所示[^1]

[^1]: This is a review about AI for MOFs.
```

（最下方会有Footnotes部分，显示脚注内容。）

---

## 2. Admonitions（提示、警告等）

[Callouts & Admonitions Documents](https://mystmd.org/guide/admonitions)

最新 MyST 推荐使用：

```
:::{类型}
内容
:::
```

可用类型：  
- note  
- tip  
- important  
- warning  
- admonition  

---

### 2.1 tip

```
:::{tip} 什么是配位聚合？
MOF 本质上是由金属离子与多齿有机配体通过配位键形成的晶体骨架。
:::
```

:::{tip} 什么是配位聚合？
MOF 本质上是由金属离子与多齿有机配体通过配位键形成的晶体骨架。
:::

---

### 2.2 note

```
:::{note}
UiO-66 是 Zr 基 MOF 中最稳定、使用最广的结构之一。
:::
```
:::{note}
UiO-66 是 Zr 基 MOF 中最稳定、使用最广的结构之一。
:::

---

### 2.3 warning

```
:::{warning}
HKUST-1 在潮湿环境下容易发生水分解反应，导致结构崩塌。
:::
```

:::{warning}
HKUST-1 在潮湿环境下容易发生水分解反应，导致结构崩塌。
:::

---

### 2.4 通用 admonition

```
:::{admonition} 自定义块标题
内容……
:::
```

:::{admonition} MOF 建模注意事项
在进行 MOF 分子模拟前，应检查晶体结构是否存在缺陷、配位不全或溶剂残留。
:::

---

## 3. Figures（图像）

[Figures Documents](https://mystmd.org/guide/figures)

MyST 推荐使用 fence directive：
```
:::{figure} path/to/image
:width: 70%
:align: center
图片说明
:::
```

### 3.1 本地图片

:::{figure} ../images/Figure-1.png
:name: MOF-structure
:width: 70%
:align: center
MOF 结构示意图。
:::

---

### 3.2 网络图片

:::{figure} https://upload.wikimedia.org/wikipedia/commons/1/1d/MIL101_synthesis.png
:width: 60%
:align: center
MIL-101 的结构示意图（Wikimedia）。
:::

---

## 4. Math（数学公式）

[Math and Equation Documents](https://mystmd.org/guide/math)

MyST 支持全部 LaTeX 数学语法。

### 4.1 行内公式

MOF 孔隙率可写为 $\phi = V_\text{void} / V_\text{cell}$。
```$\phi = V_\text{void} / V_\text{cell}$```

---

### 4.2 块级公式

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

## 5. Tables（表格）

[Tables Documents](https://mystmd.org/guide/tables)

### 5.1 常规 Markdown 表格

```
| 名称 | 金属中心 | 配体 | 特点 |
| :--- | :--- | :--- | :--- |
| MOF－5 | $\mathrm{Zn}^{2+}$ | BDC | 经典 MOF |
| UiO－66 | $\mathrm{Zr}^{4+}$ | BDC | 极高稳定性 |
```

| 名称 | 金属中心 | 配体 | 特点 |
| :--- | :--- | :--- | :--- |
| MOF－5 | $\mathrm{Zn}^{2+}$ | BDC | 经典 MOF |
| UiO－66 | $\mathrm{Zr}^{4+}$ | BDC | 极高稳定性 |

---

### 5.2 block表格

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
|结构| 比表面积 (m²/g)|
| --- | --- |
|MOF-5|3800|
|MIL-101|4500|
:::

---

## 6. Cross References（交叉引用）

[Cross Reference Documents](https://mystmd.org/guide/cross-references)

你可以为任意 block 添加 :name: 并引用。

```
在Section2里面，引用图片为：

:::{figure} ../images/Figure-1.png
:name: MOF-structure
:width: 70%
:align: center
MOF 结构示意图。
:::
```

`参见 [](#MOF-structure)。`

参见 [](#MOF-structure)。

`[第一章的1.2 典型结构示意与晶胞](./ch1-mof-basics#target-struct).`

[第一章的1.2 典型结构示意与晶胞](./ch1-mof-basics#target-struct).

---

## 7. External References（外部引用）

wiki与github等网站可以有特殊直接引用:

```<wiki:Metal–organic_framework>```

<wiki:Metal–organic_framework>

其余外部引用：

```[External Reference Documents](https://mystmd.org/guide/external-references)```

[External Reference Documents](https://mystmd.org/guide/external-references)

---

## 8. Embedding（嵌入）

[Embedding Documents]

可嵌入本文档或其他文档使用的内容。例如嵌入MOF-book chapter1的Figure1：

```
:::{embed} ch1-mof-basics.md/#fig-mof-schematic
:::
```

:::{embed} ch1-mof-basics.md/#fig-mof-schematic
:::


---

## 9. Citations（文献引用）

[Citation Documents](https://mystmd.org/guide/citations)

利用DOI引用：

文献引用：
[MOF paper](doi.org/10.1038/s41578-025-00772-8)

重复引用：
[MOF paper](doi.org/10.1038/s41578-025-00772-8)

```如文献 [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8) 所示。```
如文献 [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8) 所示。

（最下方Reference部分不会有重复引用，如果使用相同doi引用）

---

## 10. Proofs and Theorems（定理、证明）

[Theorems Documents](https://mystmd.org/guide/proofs-and-theorems)

可以添加定理，定义，证明等，利用`{prf:关键词}`添加，其中关键词可以为theorem，lemma，definition等。

```
:::{prf:theorem} MOF 稳定性判据
:label: theorem-1
若金属节点配位数足够大，则 MOF 一般更稳定。
:::

:::{prf:proof} 证明
:label: proof-theorem-1
高配位数限制了框架结构的变形自由度，从而提升稳定性。
:::
```

:::{prf:theorem} MOF 稳定性判据
:label: theorem-1
若金属节点配位数足够大，则 MOF 一般更稳定。
:::

:::{prf:proof} 证明
:label: proof-theorem-1
高配位数限制了框架结构的变形自由度，从而提升稳定性。
:::


---

## 11. Exercises（练习）

[Exercise Documents](https://mystmd.org/guide/exercises)

```
:::{exercise} 
:label: my-exercise
孔隙率练习
计算边长 3 nm、孔隙率 0.5 的简单晶胞体积。
:::
```

:::{exercise} 
:label: my-exercise
孔隙率练习
计算边长 3 nm、孔隙率 0.5 的简单晶胞体积。
:::


```
:::{solution} my-exercise
$V = 27\text{ nm}^3$。
:::
```
:::{solution} my-exercise
$V = 27\text{ nm}^3$。
:::

*注*: exercise要采用label，solution需要写出label。

---

## 12. Blocks and Comments（通用块）

[Blocks and Comments Documents](https://mystmd.org/guide/blocks)

### 12.1 Blocks

Block用于格式分割：

```
+++ {"cell": "one"}
cell 1
```
+++ {"cell": "one"}
cell 1

### 12.2 Comments

Comments用于代码中写评论。

```
This next line won't render, but it is in the HTML and LaTeX!
% Markdown comment line
```

This next line won't render, but it is in the HTML and LaTeX!
% Markdown comment line

---

## 13. Diagrams（图结构）

流程图等结构支持并且推荐使用 Mermaid架构。

[Diagram Documents](https://mystmd.org/guide/diagrams)

[Mermaid Official Documents](https://mermaid.js.org/)

```
:::{mermaid} 
graph TD
    A[金属节点] --> B[配体]
    B --> C[三维网络]
:::
```

:::{mermaid} 
graph TD
    A[金属节点] --> B[配体]
    B --> C[三维网络]
:::

---

## 14. Asides（侧边栏）

[Asides and Margin Documents](https://mystmd.org/guide/asides)

用于放置旁注，会显示在右边栏：
```
:::{aside}
ZIF 系列材料在气体分离上表现突出。
:::
```

:::{aside}
ZIF 系列材料在气体分离上表现突出。
:::


---

## 15. Dropdowns, Cards, Tabs（下拉、卡片、标签）

[Dropdowns, Cards, Tabs Documents](https://mystmd.org/guide/dropdowns-cards-and-tabs)

### 15.1 下拉

```
:::{dropdown} 点击展开 MOF 说明
MOF 是由金属节点与有机配体组成的多孔材料。
:::
```

:::{dropdown} 点击展开 MOF 说明
MOF 是由金属节点与有机配体组成的多孔材料。
:::

---

### 15.2 Tabs

```
::::{tab-set}

:::{tab-item} 结构
MOF 框架依赖金属节点和有机链接体。
:::

:::{tab-item} 孔隙
孔径决定吸附选择性。
:::

::::
```

::::{tab-set}

:::{tab-item} 结构
MOF 框架依赖金属节点和有机链接体。
:::

:::{tab-item} 孔隙
孔径决定吸附选择性。
:::

::::

---

## 16. Glossaries and Terms（术语表）

[Glossaries Documents](https://mystmd.org/guide/glossaries-and-terms)

```
:::{glossary}

MOF
: Metal–Organic Framework（金属有机骨架）

SBU
: Secondary Building Unit，次级构筑单元。

:::
```

:::{glossary}

MOF
: Metal–Organic Framework（金属有机骨架）

SBU
: Secondary Building Unit，次级构筑单元。

:::

---

