---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
title: 开放知识库编写指南
---

> 这份文档是写给**课程编写者 / 任课老师 / 助教**看的，帮助你快速上手本项目的写作与预览流程。

目前本项目是一个面向物理、化学、计算机等多学科的**开源课程知识库**，每一门课都是一个独立的 Jupyter Book，采用MyST markdown语法，最终会汇总到一个总门户网站中（通过 MkDocs 展示）。

你不需要懂太多前端或部署，只要会基本的 Markdown / Jupyter Notebook 即可参与。

---

## 1. 整体架构概览

整体开源项目的大致结构如下（简化版）：

```text
knowledge-base/
│
├── mkdocs.yml               # 顶层门户（主页）的配置文件（一般由维护者负责）
├── docs/                    # 顶层网站内容（构建后自动填充）
│   ├── index.md             # 知识库首页
│   ├── physics.md           # 物理学科介绍页
│   ├── chemistry.md         # 化学学科介绍页
│   └── ...
│
└── courses/                 # ⭐ 各门课程的源码目录（你主要在这里工作）
    ├── quantum-mechanics-book/
    │   ├── myst.yml
    │   ├── intro/
    │   ├── chapters/
    │   ├── notebooks/
    │   ├── images/
    │   ├── data/
    │   └── references/
    ├── structural-chemistry-book/
    └── ...
```

* **你作为课程编者，主要只需要关心：`courses/某门课/` 下面的内容。**
* 顶层的 MkDocs、部署到 GitHub Pages 等工作，一般由统一维护者来处理。

---

## 2. 单门课程的目录结构说明

以一门课程 `quantum-mechanics-book` 为例：

```text
courses/quantum-mechanics-book/
│               
├── myst.yml             # 文档配置（一般由项目维护人初始化，你只需小改）
│                        # 以及本课程的目录结构toc（⭐重点，需要你维护）
│
├── intro/               # 导论/前言模块
│   ├── welcome.md       # 课程欢迎页 / 简介
│   └── structure.md     # 课程结构说明（推荐写）
│
├── chapters/            # 正文章节
│   ├── ch1-wavefunction.md
│   ├── ch2-operators.md
│   ├── ch3-schrodinger.md
│   └── ...
│
├── notebooks/           # Jupyter Notebook 示例，code交互文件
│   ├── example.ipynb
│   └── ...
│
├── data/                # 本地调用文件
│   ├── structure.cif
│   └── ...
│
├── images/              # 图片资源（插图）
│   └── wavefunction.png
│
└── references/          # 附录、术语表、参考文献等
    ├── glossary.md
    └── references.md
```

> **简单结构：**
>
> * `myst.yml`：整本书设置，包括目录结构
> * `intro/`：课程导论
> * `chapters/`：课程正文
> * `notebooks/`：配套 Notebook
> * `data/`：配套本地文件
> * `images/`：图片
> * `references/`：术语和参考文献

---

## 3. 写作格式与规范

本项目推荐使用 **MyST Markdown** （MyST v2），即在普通 Markdown 的基础上，多了标准块扩展，语法上全部推荐采用最新的 `:::` 块指令语法（fenced directives）。

> Markdown的` ``` `写作格式也可以采用，这样方便在本地渲染；但 `:::` 更适合带有代码块的新格式。在本文件中，采用` ``` `写作格式，在下述示例中全部采用 `:::` 新格式。

**具体写作格式与规范在页面**：
- [写作者模板 - 1. 基础](writing-template-basic-zh.md)  （基础语法），与
- [写作者模板 - 2. 代码](writing-template-code-zh.md) （交互代码块）中；

**写作的内容呈现在页面**：
- [MOF书籍示例第一章（基础）](ch1-mof-basics-zh.md) ，与
- [MOF书籍示例第二章（进阶）](ch2-mof-advanced-zh.md) 为参考。

写作者可直接复制这些模板并改写内容，每个部分后面配有官方格式教程链接，包含更多可扩展的功能。

---

## 4. 如何添加新章节 / 修改目录

### 4.1 添加新章节的步骤

以本课程为例：

1. 在 `chapters/` 目录下新建一个文件，例如：

   ```text
   chapters/ch5-spin-and-statistics.md
   ```

2. 在文件中写内容：

   ```md
   # 第 5 章：自旋与统计

   这里是正文……
   ```

3. 打开 `myst.yml`，将在project section下面的toc列表中，将新章节加入目录，例如：

   ```yaml
   project:
   toc:
      - file: intro.md
      - title: Quantum Materials Book 1
      children:
         - file: chapters/ch1-wavefunction
         - file: chapters/ch2-operators
         - file: chapters/ch3-schrodinger
         - file: chapters/ch4-angular-momentum
         - file: chapters/ch5-spin-and-statistics   # ← 新增
   ```

4. 保存后，刷新即可，或可以重新构建本课程（见下一节）。

---

### 4.2 修改章节顺序

直接在 `myst.yml` 中调整章节的顺序即可，例如把第 5 章提前到第 3 章的位置，只要改顺序即可。

---

## 5. 本地预览：如何查看效果？

### 5.0 编写流程

如果交互流程偏多推荐使用Jupyter Lab，或者VS Code配合myst插件进行编写；如果code不多，推荐使用Obsidian等markdown编写器进行写作。如果没有交互性的code，那么直接提交markdown文档即可。

**Myst markdown v2**推荐的fence block `:::`在上述编辑器中不容易渲染，所以最好能够自己搭建本地环境来获得更好的编写体验，如下所示。

---
### 5.1 环境准备

[mystmd install document](https://mystmd.org/guide/installing)

建议使用 Conda 或 venv 创建独立环境，并安装 mystmd，JupyterLab + ipykernel：

```bash
pip install mystmd jupyterlab ipykernel
```

同时注册一个kernel，名字自定义，这里使用jupyterbook（这一步是让文件中的interactive code能在kernelspec中寻找到这个kernel环境）

```bash
python -m ipykernel install --user --name jupyterbook --display-name "jupyterbook"
```

- --name jupyterbook → kernel 内部唯一名字（写在 kernelspec 中用）
- --display-name → 在 JupyterLab 里显示的友好名称

如果你只负责单个课程，只需要这一个工具即可。构建后期Jupyter Book可由维护者进行。

（顶层 MkDocs 一般由统一维护者安装和构建）

---

### 5.2 构建单门课程

[mystmd build document](https://mystmd.org/guide/quickstart)

在某门课程的根目录下，例如：

```bash
cd courses/quantum-mechanics-book
myst init
```

构建成功后，会在该目录下生成：

```text
quantum-mechanics-book/_build/    #本地格式文件，可以忽略
quantum-mechanics-book/myst.yml   #书本的格式文件，需要添加书本名称以及toc等
```

---

### 5.3 本地浏览课程

[mystmd start document](https://mystmd.org/guide/quickstart-myst-documents)

[mystmd start executable document](https://mystmd.org/guide/quickstart-executable-documents)

在某门课程的根目录下，例如：

```bash
cd courses/quantum-mechanics-book
myst start --execute
```

你会看到

```text
📖 Built README.md in 33 ms.
📖 Built 01-paper.md in 30 ms.
📖 Built 02-notebook.ipynb in 6.94 ms.
📚 Built 3 pages for myst in 76 ms.

      ✨✨✨  Starting Book Theme  ✨✨✨

⚡️ Compiled in 510ms.

🔌 Server started on port 3000!  🥳 🎉

      👉  http://localhost:3000  👈
```

然后在浏览器中打开`http://localhost:3000`，你就可以像在线网站一样浏览整门课程。

---

## 6. 提交流程：如何上传内容？

### 6.1 普通上传文件

若是对GitHub流程不熟练，或者不使用Git功能，那么可以直接通过邮件或其他文件传输方式，将课程文件发送至项目维护者，进行双向审核与编辑沟通，然后上线。

---
### 6.2 通过统一GitHub community上传

以 GitHub 仓库为例，一般流程是：

1. **更新 / 新建文件**

   * 在 `courses/某门课/` 下编辑/新增 `.md` / `.ipynb`
   * （可选）本地运行 `myst init` 确认无明显报错，可以顺利渲染

2. **提交代码**

   ```bash
   git status          # 查看修改过的文件
   git add .
   git commit -m "添加第 3 章薛定谔方程内容"
   ```

3. **推送到远程仓库**

   ```bash
   git push origin 分支名
   ```

4. **（如采用 PR 流程）提交 Pull Request**

   * 在 GitHub 上发起 PR，请项目维护者审核合并
   * 合并后，维护者会触发构建和部署（一般是自动的 Github Actions）

> 🚨 一般建议：**编者不要直接修改 `docs/` 下的构建产物**，那是生成的静态网站。
> 你只需要维护 `courses/` 里的源文件。

---

## 7. 编写建议与最佳实践

- 建议新开启一门课编写前与编辑和项目维护者沟通目前的开源整体内容，以及其他编写者正在构思内容，方便进行知识架构补充。
* 一个文件只讲一个主要知识点或一个章节，避免单页面过长。
* 章节开头建议有一个简短的“本章目标 / 学习要点”列表，或最后有一个知识总结。
* 尽量深入浅出，难度到达能理解目前的论文水准，可以将内容分为不带细节高屋建瓴的版本，和带推导或代码细节的实践进阶版本。

---

## 8. 常见问题（FAQ）

**Q0：我不用英语，用其他语言写作可以吗**
A：可以，请写作前与项目维护人进行沟通。我们推荐使用各种语言写作，也就是英语外，可以使用中文等语言；编写过程或结束后我们推荐将内容并行翻译为英文标准版，例如示例中的`MOF Learning Handbook`；同时注意每个block的label都需要在后面区分不同语言：例如在中文内容里，将所有label加上`-zh`后缀，防止编译时出现重复错误。

---

**Q1：我只会写普通 Markdown，可以不学 MyST 吗？**
A：可以，大部分 MyST 语法与 Markdown 一致，你可以从基本 Markdown 开始，逐步添加公式和代码块。

---

**Q2：我需要自己写 `myst.yml` 吗？**
A：通常由项目维护人提供初始模板。你主要需要维护 `myst.yml` 文件内，`project`下的`toc`章节列表，以及小范围调整其他信息（如标题、作者）。

---

**Q3：为什么我在本地看不到顶层门户（首页）？**
A：顶层门户（MkDocs 部分）通常由统一维护者构建。
作为课程编者，你只需关注单课程的 MyST-Jupyter Book 预览即可。

---

**Q4：跨课程引用的链接 URL 要我自己写吗？**
A：目前阶段，一般采用**固定的 URL 规则**（例如 `https://opensciencedomain/subject/course/...`）。
维护者会给出约定好的路径示例，你可以按该规则填写链接。如果路径将来变动，会统一替换。

---

**Q5：AI 助教（LLM）相关的前端/后端我需要参与吗？**
A：这是未来的feature，目前暂时在开发中。一般不需要编写者参与这部分。
网站中用于给学生提问的“AI 助教”是由统一的前端组件 + 后端 API 提供的，你只需要保证内容结构合理，AI 才能更好地回答问题。

---

## 9. 如果你还不确定从哪里开始……

1. 先联系项目维护者，共同商量能够贡献的题目与内容，然后进行开发沟通，同时看网站示例内容

2. 决定内容后，在 `courses/` 下找到你负责的课程目录，例如 `quantum-mechanics-book/`，或者本地下载`MOF learning handbook`写作模板

3. 打开 `intro.md`，写好课程简介，构建课程大致框架

4. 将 `myst.yml`中的`toc`构建为大致构想的章节结构

5. 在 `chapters/` 下新建一个章节文件，或者直接在写作模板上进行修改，用简短的正文试写

6. 在本地运行：

   ```bash
   cd courses/quantum-mechanics-book
   myst init
   myst start --execute
   ```

7. 用浏览器打开 `http://localhost:3000`，查看效果

8. 如果一切正常，再考虑增加更多内容，最后按照提交流程上传文件即可。

---

如有任何疑问，可以联系项目维护者，或在仓库中开 Issue 讨论。
欢迎你把自己的课程内容沉淀到这个开放知识库中，让更多学生受益 🙌