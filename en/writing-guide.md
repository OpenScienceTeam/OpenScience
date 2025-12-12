---
kernelspec:
  name: jupyterbook
  display_name: 'jupyterbook'
title: Knowledge Base Authoring Guide
---

> This guide is intended for **course authors, instructors, and teaching assistants** to help you quickly get started with writing and previewing content in this project.

This project is an **open-source course knowledge base** spanning multiple disciplines including physics, chemistry, and computer science. Each course is managed as an independent Jupyter Book using MyST Markdown syntax, and all courses are eventually aggregated on a central portal website (displayed with MkDocs).

No extensive knowledge of web frontend or deployment is required; familiarity with basic Markdown and Jupyter Notebook is sufficient to contribute.

---

## 1. Project Structure Overview

The simplified structure of the overall open-source project is as follows:

```text
knowledge-base/
│
├── mkdocs.yml               # Top-level portal (home page) configuration file (maintained by site admin)
├── docs/                    # Top-level site contents (auto-filled after build)
│   ├── index.md             # Knowledge base homepage
│   ├── physics.md           # Physics subject introduction
│   ├── chemistry.md         # Chemistry subject introduction
│   └── ...
│
└── courses/                 # ⭐ Main directory for all course source code (this is your main workspace)
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

* **As a course author, you primarily need to focus on the contents under `courses/<your-course>/`.**
* Top-level configuration (MkDocs) and deployment (e.g., to GitHub Pages) are generally managed by site maintainers.

---

## 2. Single Course Directory Structure

Taking `quantum-mechanics-book` as an example:

```text
courses/quantum-mechanics-book/
│               
├── myst.yml             # Book configuration file (initialized by maintainers, minor edits on your part)
│                        # Also contains the ToC—⭐ you will maintain this
│
├── intro/               # Introductory/Preface module
│   ├── welcome.md       # Welcome/introduction page
│   └── structure.md     # Course structure description (recommended)
│
├── chapters/            # Main content chapters
│   ├── ch1-wavefunction.md
│   ├── ch2-operators.md
│   ├── ch3-schrodinger.md
│   └── ...
│
├── notebooks/           # Jupyter Notebook examples and interactive files
│   ├── example.ipynb
│   └── ...
│
├── data/                # Local data files
│   ├── structure.cif
│   └── ...
│
├── images/              # Image resources/illustrations
│   └── wavefunction.png
│
└── references/          # Appendices, glossaries, references, etc.
    ├── glossary.md
    └── references.md
```

> **To summarize:**
>
> * `myst.yml`: Book-wide settings, including Table of Contents
> * `intro/`: Course introduction
> * `chapters/`: Main course content
> * `notebooks/`: Companion Jupyter Notebooks
> * `data/`: Supplementary local files
> * `images/`: Images
> * `references/`: Glossary and references

---

## 3. Content Standards and Formatting

We recommend using **MyST Markdown** (MyST v2), which extends standard Markdown with additional block and directive features. For block content, always use the latest `:::` fenced directive syntax.

> The traditional Markdown code fences `` ``` `` are also supported, which can be useful for local editing and previewing. However, `:::` blocks are preferred for code-heavy or structured content. This guide uses `` ``` `` for demonstration, while all examples in the links below use the new `:::` syntax.

**For detailed formatting and style guidelines, see:**
- [Authoring Template - 1. Basics](writing-template-basic.md) (basic syntax)
- [Authoring Template - 2. Code](writing-template-code.md) (interactive code blocks)

**For examples of authored content, refer to:**
- [MOF Book Example: Chapter 1 (Basics)](ch1-mof-basics.md)
- [MOF Book Example: Chapter 2 (Advanced)](ch2-mof-advanced.md)

Authors are encouraged to copy and adapt these templates. Each section includes a link to the official style guide for further extensibility.

---

## 4. How to Add Chapters / Edit the Table of Contents

### 4.1 Steps to Add a New Chapter

For example:

1. Create a new file under the `chapters/` directory, such as:

   ```text
   chapters/ch5-spin-and-statistics.md
   ```

2. Draft your content in the new file:

   ```md
   # Chapter 5: Spin and Statistics

   Main content goes here...
   ```

3. Open `myst.yml` and add your new chapter to the ToC list in the `project` section. For example:

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
         - file: chapters/ch5-spin-and-statistics   # ← Newly added
   ```

4. Save and refresh, or rebuild the course as described in the next section.

---

### 4.2 Rearranging Chapter Order

To change the sequence of chapters, simply reorder the entries in the `myst.yml` file. For example, to move Chapter 5 to Chapter 3, just adjust its position in the list.

---

## 5. Local Preview: How to Check Your Work

### 5.0 Writing Workflow

If your course involves substantial interactivity, we recommend authoring with JupyterLab or VS Code with the MyST plugin. For simpler content, editors like Obsidian are suitable. If no interactive code is required, you may submit plain Markdown documents directly.

**Note:** The recommended MyST v2 fenced directive `:::` may not render well in some editors, so setting up a local environment provides the most accurate authoring experience.

---
### 5.1 Environment Setup

See the [MyST installation guide](https://mystmd.org/guide/installing).

We advise creating a dedicated environment with Conda or venv, and installing `mystmd`, `jupyterlab`, and `ipykernel`:

```bash
pip install mystmd jupyterlab ipykernel
```

You should then register a custom kernel, e.g. called "jupyterbook", so that interactive code in your files is associated with the correct environment:

```bash
python -m ipykernel install --user --name jupyterbook --display-name "jupyterbook"
```

- `--name jupyterbook`: the internal kernel name used in kernelspec references
- `--display-name`: the user-friendly name shown in JupyterLab

If you are only responsible for a single course, these tools are all you need. Final Jupyter Book building and deployment can be handled by project maintainers.

(The top-level MkDocs site is generally set up and built by maintainers.)

---

### 5.2 Building a Single Course Book

See the [MyST build guide](https://mystmd.org/guide/quickstart).

From your course root directory, for example:

```bash
cd courses/quantum-mechanics-book
myst init
```

Upon successful build, the following structure is generated:

```text
quantum-mechanics-book/_build/    # Local build outputs (can be ignored)
quantum-mechanics-book/myst.yml   # Book configuration file—set the title and update ToC as needed
```

---

### 5.3 Local Preview of Course

Consult:
- [MyST start document guide](https://mystmd.org/guide/quickstart-myst-documents)
- [MyST start executable document guide](https://mystmd.org/guide/quickstart-executable-documents)

In your course root directory, run:

```bash
cd courses/quantum-mechanics-book
myst start --execute
```

You will see output similar to:

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

Open `http://localhost:3000` in your browser and you can view your course as it will appear online.

---

## 6. Content Submission Workflow

### 6.1 Submitting Files Directly

If you are not familiar with the GitHub workflow, or do not wish to use Git, you may send your course files directly to the project maintainers via email or other file transfer methods for review, editing, and publication.

---
### 6.2 Submitting via the Central GitHub Community

The standard workflow (for contributors comfortable with GitHub) is as follows:

1. **Update or create new files**

   * Edit or create `.md` / `.ipynb` files under `courses/<your-course>/`
   * (Optional) Run `myst init` locally to ensure no errors and preview rendering

2. **Commit your changes**

   ```bash
   git status          # View updated files
   git add .
   git commit -m "Add content for Chapter 3: Schrodinger Equation"
   ```

3. **Push to the remote repository**

   ```bash
   git push origin <branch-name>
   ```

4. **(If using Pull Request workflow) Submit a Pull Request**

   * Open a PR on GitHub and request review/merge by a maintainer
   * Once merged, maintainers will trigger the build and deployment process (typically automated via GitHub Actions)

> 🚨 Recommendation: **Do not directly edit the built artifacts under `docs/`**; those are static site outputs.
> You only need to maintain source files within `courses/`.

---

## 7. Authoring Tips and Best Practices

- Before starting a new course, coordinate with editors and project maintainers to understand the scope and current architecture, and to avoid duplication of efforts.
- Each file should focus on a single main topic or chapter to avoid excessively long documents.
- It is advisable to include a brief "Objectives / Key Points" list at the start of each chapter, or a summary at the end.
- Strive for clarity and accessibility; aim for a level that allows students to understand current literature. Consider providing both a high-level overview version and a more advanced treatment with derivations or code as appropriate.

---

## 8. Frequently Asked Questions (FAQ)

**Q0: Can I write in languages other than English?**  
A: Yes, but please coordinate this with the project maintainers beforehand. We encourage contributions in any language, including Chinese. After drafting, we strongly recommend maintaining a parallel English version (as in the `MOF Learning Handbook` example). Be sure to append language tags (e.g., `-zh` for Chinese content) to all block labels to avoid duplicate label errors during compilation.

---

**Q1: I only know regular Markdown. Do I need to learn MyST?**  
A: Not necessarily. Most MyST syntax is compatible with standard Markdown, so you can start with basic Markdown and incrementally use MyST features for formulas and code blocks as needed.

---

**Q2: Do I need to create my own `myst.yml` file?**  
A: Project maintainers typically provide an initial template. Your main responsibility is to maintain the chapters list under the `toc` section in `myst.yml`, and make minor adjustments such as the title or authors as needed.

---

**Q3: Why can't I see the main portal (homepage) locally?**  
A: The top-level portal (MkDocs component) is constructed and managed by the maintainers. As a course author, focus on previewing your individual course using MyST-Jupyter Book.

---

**Q4: Do I need to manually create inter-course link URLs?**  
A: Currently, a fixed URL scheme is used (e.g., `https://opensciencedomain/subject/course/...`). Maintainers will provide example paths. You may use these, and any future changes to the scheme will be handled globally.

---

**Q5: Do I need to work on the AI assistant (LLM) front-end or back-end?**  
A: No. This is a future feature and is still under development. Authors are not required to work on this aspect. The site’s "AI teaching assistant" is powered by core front-end components and back-end API; your focus should be on clear, well-structured content to maximize the assistant’s effectiveness.

---

## 9. Not Sure Where to Start?

1. First contact a project maintainer to discuss potential contributions and review existing sample content together.
2. Once you’ve decided on the scope, locate your assigned course directory under `courses/` (e.g., `quantum-mechanics-book/`), or download the local `MOF learning handbook` template.
3. Open `intro.md` and draft a course introduction; establish a general structure.
4. Update the `toc` in `myst.yml` to reflect your envisioned chapter structure.
5. Create a new file in `chapters/`, or adapt the template, and try drafting a short sample section.
6. Run locally:
   ```bash
   cd courses/quantum-mechanics-book
   myst init
   myst start --execute
   ```
7. Open your browser to `http://localhost:3000` and view the output.
8. If all looks good, expand the content as needed, and submit your work following the process outlined above.

---

For any questions, please reach out to a project maintainer or open an issue in the repository.
We encourage you to contribute your course content to this open knowledge base to benefit more students 🙌
