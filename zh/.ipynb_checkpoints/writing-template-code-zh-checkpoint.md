---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
title: MOF Book 写作者模板
abstract:
  包含所有 _MyST markdown_ 语法示例

jupyter: false

---

# 代码部分

本章展示所有 `{code-cell}` 的进阶用法。  
所有示例均以 **MOF 结构建模 / 吸附模拟 / 材料性质计算** 为主题。

:::{warning}
所有的代码部分请全部用英文，为保证运行和渲染效果。
:::

## 1. 静态代码（不执行）

```
block内容：

:::{code} python
def mof_density(M, V):
return M / V
print(mof_density(1000, 500))
:::
```

:::{code} python
def mof_density(M, V):
return M / V
print(mof_density(1000, 500))
:::

适用于：
解释概念 / 示例代码片段

---

## 2 可执行 code-cell

（需要文件开头写 `kernelspec`，并且运行 `myst start –execute`）

```
:::{code-cell} python
import numpy as np
print("Example: generate random porosity:", np.random.rand())
:::
```

:::{code-cell} python
import numpy as np
print("Example: generate random porosity:", np.random.rand())
:::

---

## 3 添加元数据

元数据可以控制代码执行方式与显示方式。

### 3.1 隐藏输入（只显示输出）

```
block内容：

:::{code-cell} python
:tags: hide-input
print('MOF is great')
:::
```

:::{code-cell} python
:tags: hide-input
print('MOF is great')
:::

---

### 3.2 隐藏输出（只显示代码）

```
block内容：

:::{code-cell} python
:tags: hide-output

x = 42
x
:::
```

:::{code-cell} python
:tags: hide-output

x = 42
x
:::

---

### 3.3 完全移除输入（最终网页中看不到代码）
```
block内容：
:::{code-cell} python
:tags: remove-input

print("This code is not visible in the final webpage, but still executed")
:::
```

:::{code-cell} python
:tags: remove-input

print("This code is not visible in the final webpage, but still executed")
:::

---

### 3.4 完全移除输出（网页不可见）

```
block内容：

:::{code-cell} python
:tags: remove-output

print("This code is not visible in the final webpage, but still executed")
```

:::{code-cell} python
:tags: remove-output

print("This code is not visible in the final webpage, but still executed")
:::

---

### 常用 tags 

:::{table}
| tag | 含义 |
|-----|------|
| hide-input | 隐藏代码，只显示输出 |
| hide-output | 隐藏输出 |
| remove-input | 最终页面完全移除输入 |
| remove-output | 完全移除输出 |
| raises | 指定必须抛出的异常 |
| cache | 允许执行缓存 |
:::

---

## 4. 图形绘制（Plotting）

以下示例展示 MOF 孔隙率与比表面积的关系图。

:::{code-cell} python

import numpy as np
import matplotlib.pyplot as plt

phi = np.linspace(0.1, 0.9, 9)
sa = 1500 * phi * 2

plt.figure(figsize=(6,4))
plt.plot(phi, sa, marker="o")
plt.xlabel("Porosity φ")
plt.ylabel("Surface Area (m²/g)")
plt.title("MOF Porosity vs Surface Area (illustration)")
plt.grid(True)
plt.show()
:::

---

## 5. 多图展示（Subplots）

:::{code-cell} python

fig, axs = plt.subplots(1, 2, figsize=(10,4))

axs[0].plot(phi, sa, 'o-')
axs[0].set_title("Surface Area")

axs[1].plot(phi, np.sqrt(sa), 's-')
axs[1].set_title("sqrt(Surface Area)")

fig.suptitle("MOF Plot Example")
plt.show()
:::

---

## 6. Pandas 表格


:::{code-cell} python
import pandas as pd

df = pd.DataFrame({
    "MOF": ["MOF-5", "UiO-66", "HKUST-1"],
    "Metal": ["Zn²⁺", "Zr⁴⁺", "Cu²⁺"],
    "Surface Area (m²/g)": [3800, 1200, 1500]
})
df
:::

---

## 7. 结构可视化（ASE）

（如果你的 kernel 安装了 ase）

### 7.1 ASE构造分子并交互显示

:::{code-cell} python
from ase.build import molecule
from ase.visualize import view

try:
    #Build a simple molecule with ASE
    water = molecule('H2O')
    
    #Visualize the molecule
    
    disp_water = view(water, viewer='x3d')
    display(disp_water)

except:
    print('ASE is not installed, so the example is skipped')
:::

---

### 7.2 从本地文件读取结构并展示（CIF / POSCAR 等）


:::{code-cell} python
from ase.io import read

#Read structure from a local file, e.g. CIF\PDB
mof_from_file = read("../data/MOF-5.pdb")

#View the periodic structure
disp_mof=view(mof_from_file, viewer='x3d')
display(disp_mof)

:::

