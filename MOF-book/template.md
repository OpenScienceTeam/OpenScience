---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
---

# MOF Book 写作者模板（包含所有 MyST 语法示例）

本文件示例展示 MyST Markdown（MyST v2）的全部主要语法，  
所有示例都使用 MOF（金属有机骨架）主题进行改写，  
并全部采用最新推荐的 `:::` 块指令语法（fenced directives）。

写作者可直接复制这些模板并改写内容。

---

# 1. Typography（排版示例）

## 1.1 强调与行内格式

普通文本  
**加粗文本**  
*斜体文本*  
***粗斜体***  
`行内代码`

MOF 示例：

> MOF-5 由 **Zn₄O** 次级构筑单元（SBU）与 *对苯二甲酸配体（BDC）* 组成。  

---

## 1.2 引用块（Block Quote）

> MOF 材料因其可设计性而被称为 “纳米魔方”。

---

## 1.3 水平线

---

---

# 2. Admonitions（提示、警告等）

最新 MyST 推荐使用：

:::{}
内容
:::

可用类型：  
- note  
- tip  
- important  
- warning  
- admonition  

---

## 2.1 tip

:::{tip} 什么是配位聚合？
MOF 本质上是由金属离子与多齿有机配体通过配位键形成的晶体骨架。
:::

---

## 2.2 note

:::{note}
UiO-66 是 Zr 基 MOF 中最稳定、使用最广的结构之一。
:::

---

## 2.3 warning

:::{warning}
HKUST-1 在潮湿环境下容易发生水分解反应，导致结构崩塌。
:::

---

## 2.4 通用 admonition

:::{admonition} 自定义块标题
内容……
:::

:::{admonition} MOF 建模注意事项
在进行 MOF 分子模拟前，应检查晶体结构是否存在缺陷、配位不全或溶剂残留。
:::

---

# 3. Figures（图像）

MyST 推荐使用 fence directive：

:::{figure} path/to/image
:width: 70%
:align: center
图片说明
:::

## 3.1 本地图片

:::{figure} images/mof-structure.png
:width: 70%
:align: center
MOF 结构示意图：金属节点（蓝色）连接有机配体（灰色）。
:::

---

## 3.2 网络图片

:::{figure} https://upload.wikimedia.org/wikipedia/commons/1/1d/MIL101_synthesis.png
:width: 60%
:align: center
MIL-101 的结构示意图（Wikimedia）。
:::

---

# 4. Math（数学公式）

MyST 支持全部 LaTeX 数学语法。

## 4.1 行内公式

MOF 孔隙率可写为 $\phi = V_\text{void} / V_\text{cell}$。

---

## 4.2 块级公式

$$
V_\text{cell} = abc\sqrt{
1 + 2\cos\alpha\cos\beta\cos\gamma -
\cos^2\alpha - \cos^2\beta - \cos^2\gamma
}
$$

---

## 4.3 对齐数组

$$
\begin{aligned}
q(P) &= q_\max \frac{bP}{1 + bP} \\
\phi &= \frac{V_\text{void}}{V_\text{cell}}
\end{aligned}
$$

---

# 5. Tables（表格）

## 5.1 常规 Markdown 表格

名称	金属中心	配体	特点
MOF-5	Zn²⁺	BDC	经典 MOF
UiO-66	Zr⁴⁺	BDC	极高稳定性

---

## 5.2 对齐表格

:align: center

结构	比表面积 (m²/g)
MOF-5	3800
MIL-101	4500


---

# 6. Code（代码）

## 6.1 普通代码

:::{code} python
def mof_density(M, V):
return M / V

print(mof_density(1000, 500))
:::

---

## 6.2 可执行 code-cell

（需要 kernelspec + myst start –execute）

:::{code-cell} python
import numpy as np
print(“示例：生成随机孔隙率：”, np.random.rand())
:::

---

# 7. Cross References（交叉引用）

你可以为任意 block 添加 :name: 并引用。

:::{figure} images/mof-structure.png
:name: fig-mof
MOF 结构图
:::

例如：参见 {ref}fig-mof。

⸻

# 8. External References（外部引用）

使用 MyST 的 {external:...}：

例如：

{external:github}`mystmd/mystmd`

将在渲染后指向 GitHub。

⸻

# 9. Embedding（嵌入）

可嵌入文件、视频、HTML。

## 9.1 插入 YouTube

:::{embed} https://www.youtube.com/watch?v=dQw4w9WgXcQ
:aspect: 16:9
:width: 70%
:::

---

## 9.2 嵌入 HTML

:::{embed}
<iframe src="https://wikipedia.org"></iframe>
:::

---

# 10. Citations（文献引用）

引用格式通常通过 .bib 文件管理。

:::{cite} yaghi2003reticular
:::

引用示例：MOF 的提出来自 Yaghi 等人的开创性工作 {cite}yaghi2003reticular。

---

# 11. Proofs and Theorems（定理、证明）

:::{theorem} MOF 稳定性判据
若框架的节点配位数足够大，则 MOF 更可能具备优异稳定性。
:::

:::{proof}
直观上，高配位可增强金属簇的刚性，减少结构变形的自由度。
:::

---

# 12. Exercises（练习）

:::{exercise} MOF 孔隙率练习
计算边长为 3 nm、孔隙率为 0.5 的简单立方型 MOF 的体积与孔隙率。
:::

:::{solution} 
$V = 27 \text{ nm}^3$，孔隙率 $0.5$。
:::

---

# 13. Blocks（通用块）

:::{block} MOF 设计流程（三步）
	1.	选择金属中心
	2.	选择有机配体
	3.	优化孔隙结构
:::

---

# 14. Diagrams（图结构）

例如使用 Mermaid：

:::{diagram} mermaid
graph TD
A[金属节点] –> B[有机配体]
B –> C[三维骨架]
:::

⸻

# 15. Asides（侧边栏）

:::{aside}
MOF-74 是一类开放金属位点（OMS）丰富的 MOF，常用于 CO₂ 捕获。
:::

⸻

# 16. Dropdowns, Cards, Tabs（下拉、卡片、标签）

## 16.1 下拉

:::{dropdown} 点击展开 MOF 说明
MOF 是由金属节点与有机配体组成的多孔材料。
:::

---

## 16.2 Tabs

::::{tab-set}

:::{tab-item} 结构
MOF 框架依赖金属节点和有机链接体。
:::

:::{tab-item} 孔隙
孔径决定吸附选择性。
:::

::::

---

# 17. Glossaries and Terms（术语表）

:::{glossary}

MOF
: Metal–Organic Framework（金属有机骨架）

SBU
: Secondary Building Unit，次级构筑单元。

:::

---

（结束）

所有 MyST 功能示例到此结束。写作者可自由复制、删除、替换具体内容。

---
