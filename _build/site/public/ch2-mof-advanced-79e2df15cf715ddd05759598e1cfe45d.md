---
kernelspec:
  name: python3
  display_name: 'Python 3'
  title: "第二章：MOF 吸附与模拟（进阶)!!"
---

# 第二章：MOF 吸附与模拟（进阶）

## 2.1 吸附等温线基础

MOF 在气体储存、分离等应用中，**吸附等温线**是非常重要的表征手段。

典型的 Langmuir 等温线可写为：

$$
q(P) = q_{\max} \frac{b P}{1 + b P}
$$

其中：

- $ q(P) $：在压力 $P$ 下的吸附量
- $ q_{\max} $：饱和吸附量
- $ b $：平衡常数（与温度有关）

:::{warning}
公式本身是简化模型，真实 MOF 吸附行为可能更复杂，如多位点吸附、微孔填充等。
:::

## 2.2 交互式曲线（使用 ipywidgets）

下面示例展示如何在书中嵌入交互式控件（在支持的小环境中会成为交互式图像）。

:::{code-cell} python
---
tags: [interactive]
---
import numpy as np
import matplotlib.pyplot as plt

try:
    from ipywidgets import interact, FloatSlider
except ImportError:
    interact = None

def langmuir_isotherm(P, qmax, b):
    return qmax * b * P / (1 + b * P)

def plot_langmuir(qmax=5.0, b=1.0):
    P = np.linspace(0, 10, 200)
    q = langmuir_isotherm(P, qmax, b)
    plt.figure()
    plt.plot(P, q)
    plt.xlabel("压力 P (bar)")
    plt.ylabel("吸附量 q (mmol/g)")
    plt.title(f"Langmuir 等温线 (qmax={qmax:.1f}, b={b:.2f})")
    plt.grid(True)
    plt.show()

if interact is not None:
    interact(
        plot_langmuir,
        qmax=FloatSlider(min=1, max=10, step=0.5, value=5),
        b=FloatSlider(min=0.1, max=5, step=0.1, value=1),
    )
else:
    # 如果没有 ipywidgets，就画一张默认图
    plot_langmuir()
:::

:::{note}
要真正看到交互效果，需要在支持小部件渲染的环境中（例如 JupyterLab 或某些在线部署）。
:::

## 2.3 动画示例（matplotlib animation）

下面是一个简单动画例子，模拟「气体分子进出 MOF 孔道」的示意（非常简化）。

:::{code-cell} python
---
tags: [animation]
---
import numpy as np
import matplotlib.pyplot as plt

from matplotlib import animation

# 创建一个简单的 2D 孔道示意 (正方形区域)
fig, ax = plt.subplots()
ax.set_xlim(0, 1)
ax.set_ylim(0, 1)
ax.set_title("气体分子在 MOF 孔道中的随机运动（示意）")
ax.set_xticks([])
ax.set_yticks([])

n_particles = 10
positions = np.random.rand(n_particles, 2)
scat = ax.scatter(positions[:, 0], positions[:, 1])

def update(frame):
    global positions
    # 随机移动
    step = 0.05 * (np.random.rand(n_particles, 2) - 0.5)
    positions = positions + step
    # 简单碰壁反射
    positions = np.mod(positions, 1.0)
    scat.set_offsets(positions)
    return scat,

ani = animation.FuncAnimation(
    fig, update, frames=100, interval=100, blit=True
)

plt.close(fig)  # 避免重复静态图

from IPython.display import HTML
HTML(ani.to_jshtml())
:::

:::{tip}
在 HTML 输出中，这段代码将生成一个嵌入的 JS 动画。
若构建时出错，检查你的环境是否安装了 matplotlib、ffmpeg 等依赖。
:::

## 2.4 Tabs 与折叠内容（MyST 扩展）

### 2.4.1 Tabs 示例

::::{tab-set}
:::{tab-item} 吸附
吸附（adsorption）是气体或液体分子被「吸附到」固体表面或孔道中的过程。
:::
:::{tab-item} 解吸
解吸（desorption）是已经被吸附的分子从表面或孔道中离开的过程。
:::
:::{tab-item} 扩散
扩散（diffusion）描述了分子在 MOF 孔道中的迁移行为。
:::
::::


### 2.4.2 折叠/下拉内容

GCMC 是模拟吸附过程的常用方法之一。  
在给定温度 T、化学势 μ（或压力 P）条件下，体系粒子数 N 可以波动。
通常用于模拟 MOF 对气体的吸附等温线。

## 2.5 高级代码示例：简单 GCMC 风格的伪代码

:::{code-cell} python
---
tags: [gcmc-pseudo]
---
import random
import math

def gcmc_step(N, mu, beta):
    """
    非常简化的单步 GCMC 伪代码示意：
    - 以概率 0.5 尝试插入粒子
    - 否则尝试删除粒子
    """
    if random.random() < 0.5:
        # 尝试插入
        dE = random.uniform(-1, 1)  # 假设的能量变化
        acc = min(1, math.exp(-beta * dE + beta * mu))
        move = "insert"
    else:
        # 尝试删除
        if N == 0:
            return N, "skip"
        dE = random.uniform(-1, 1)
        acc = min(1, math.exp(-beta * (-dE) - beta * mu))
        move = "delete"

    if random.random() < acc:
        if move == "insert":
            N += 1
        elif move == "delete":
            N -= 1
        accepted = True
    else:
        accepted = False

    return N, f"{move}, accepted={accepted}"

N = 0
mu = -2.0   # 化学势（示意）
beta = 1.0  # 1/(k_B T)（简化）

for step in range(10):
    N, info = gcmc_step(N, mu, beta)
    print(f"Step {step:2d}: N={N}, {info}")
:::

## 2.6 内联公式、交叉引用与参考文献

内联公式示例：Langmuir 模型中的平衡常数 (b) 与温度呈指数关系。

可引用上一章的图：见 {ref}fig-mof-schematic。
也可以引用表格：见 {ref}tab-common-mofs。

（如果你要加入真正的参考文献，可以再补充一个 references.bib，并在这儿使用 []{cite} 语法等。）

⸻

## 2.7 小结

本章通过 交互式曲线、动画、Tabs、下拉内容、进阶代码示例 等，展示了如何在 Jupyter Book 中构建一个较为丰富的 MOF 进阶章节。

:::{admonition} 练习
尝试：
1. 将本章中的 Langmuir 等温线换成 Freundlich 或 Sips 模型；
2. 将动画改为 3D 轨迹；
3. 将 GCMC 伪代码替换为真正的能量评价（如 Lennard-Jones 势）。
:::
