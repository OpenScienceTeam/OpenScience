---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'

title: MOF书籍示例第一章（基础）
---

> 本章为MOF简介基础章节，显示可以使用的基础功能和排版

# 第一章：MOF 基础概念与结构

## 1.1 什么是 MOF？

金属有机骨架（Metal–Organic Framework, MOF）是一类由**金属节点**和**有机配体**组成的多孔晶体材料。

:::{tip} MOF 的历史
MOF 领域的爆炸式增长始于 1990 年代末，Omar Yaghi 教授在这一领域做出了开创性的贡献。
:::

- 金属节点：通常是金属离子或金属簇（如 Zn²⁺, Cu²⁺, Zr⁴⁺ 等）
- 有机配体：含羧酸、吡啶等配位基团的多齿配体
- 特点：比表面积超大、结构可设计、官能化灵活

:::{hint}
可以把 MOF 想象成「金属原子是节点、有机分子是杆件」的三维骨架结构。
:::


> MOF 材料最大的特点是其**超高的比表面积**和**可调控的孔径结构**。你可以把它们想象成纳米级别的乐高积木。


如文献 [Yaghi, 2025](https://doi.org/10.1038/s41578-025-00772-8) 所示[^1]

[^1]: This is a review about AI for MOFs.

---


(target-struct-zh)=
## 1.2 典型结构示意与晶胞

%(target-struct-zh)=   这部分是用来为cross-reference做link

### 1.2.1 结构示意图片

:::{figure} ../images/Figure-1.png
:name: fig-mof-schematic-zh
:width: 60%
:align: center
一个 MOF 结构示意图。
:::

## 1.3 简单晶体学表达

下面使用公式描述简单的 MOF 框架晶胞尺寸及孔隙率。

### 1.3.1 体积与孔隙率

晶胞体积：

$$
V_{\text{cell}} = a \cdot b \cdot c \cdot \sqrt{
1 + 2\cos\alpha\cos\beta\cos\gamma \cos^2\alpha - \cos^2\beta - \cos^2\gamma
}
$$

假设以分子模拟或吸附实验得到 MOF 的空隙体积 $V_{\text{void}}$，则孔隙率 $\phi$ 可写为：

$$
\phi = \frac{V_{\text{void}}}{V_{\text{cell}}}
$$

:::{admonition} 思考题
为什么 MOF 通常具有比传统多孔材料（如活性炭、硅胶）更高的可设计性？
:::

## 1.4 表格：一些常见 MOF

:::{table}
:name: tab-common-mofs-zh
:align: center

| 名称       | 金属中心 | 有机配体                     | 特点                          |
|------------|-----------|------------------------------|-------------------------------|
| MOF-5      | Zn²⁺      | 1,4-苯二甲酸 (BDC)          | 早期经典 MOF, 高比表面积     |
| UiO-66     | Zr⁴⁺      | BDC                          | 热/化学稳定性好              |
| HKUST-1    | Cu²⁺      | 1,3,5-苯三甲酸 (BTC)        | 经典铜基 MOF                  |
| MIL-101(Cr)| Cr³⁺      | BDC                          | 超大孔体积, 良好水稳定性     |
:::

## 1.5 使用python代码描述MOF

% 这是不会显示的comments：以下code block根据设置不会被当成可执行单元。

:::{code} python
def describe_mof(name, metal, linker):
    return f"{name} is a MOF with {metal} as the metal center and {linker} as the organic linker."

print(describe_mof("UiO-66", "Zr⁴⁺", "BDC"))
:::

上面是python coding的MOF描述代码，`describe_mof`。



## 1.6 使用python代码计算孔隙率与孔体积关系

% 以下code block根据设置会被当成可执行单元，并且可以通过修改:tags:来定义不同的输入、输出显示。

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


## 1.7 简单 2D 图示例

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

## 1.8 练习区（task list）

:::{exercise} 1. 计算孔隙率
- 手动计算一个简单 MOF 的孔隙率
:::

:::{exercise} 2. 查找MOF结构
- 查找你感兴趣的一个 MOF 的结构信息
:::

:::{exercise} 3. 载入可视化
- 使用 pymatgen 或 ASE 载入 CIF 文件尝试可视化
:::