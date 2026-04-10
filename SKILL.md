---
name: paper-orchestra
description: Autonomous, multi-agent AI research paper writing skill. Features a Human-in-the-Loop (HITL) brainstorming gate, semantic literature review, zero-hallucination markdown drafting, data visualization, and sequential multi-format compilation (HTML -> DOCX -> PDF).
---

# PaperOrchestra Skill

This skill transforms loose research topics and ideas into fully fleshed-out, submission-ready academic manuscripts via a rigorous 5-Phase Gated Workflow. You act as an ensemble of specialized writing agents (Outline, Plotting, Literature Review, Writer, Refinement).

## 🎯 When to Use
Trigger this skill when the user asks you to write a paper given a topic or data, or explicitly invokes the "paper-orchestra" skill.

## 🛑 5-Phase Gated Workflow

You MUST execute these phases strictly in order. Always declare your current "Phase" to the user. **Do not skip phases or generate the full paper immediately.** Stop and wait for the user at the designated `[USER REVIEW GATE]` markers.

### Phase 1: Human-in-the-Loop (HITL) Brainstorming
* **Action**: When given a topic, do NOT start writing the paper. Instead, engage the user in a targeted brainstorming session. Ask focused questions to establish:
  1. The core Research Hypothesis / Problem Statement (연구 가설).
  2. The primary Novel Contributions (주요 기여점).
  3. The Baseline Models/Methods for comparison (비교군).
* **[USER REVIEW GATE]**: Stop generating and wait for the user to answer and agree on the direction.

### Phase 2: Outline & Hybrid Literature Review 
* **Action**: Using the agreed-upon direction from Phase 1, generate a structured JSON/Markdown Outline (Sparse Idea). Then, use the `search_web` tool to discover actual, verified research papers relevant to the topic. Formulate a BibTeX list. Only use verified real papers—Zero Hallucination.
* **[USER REVIEW GATE]**: Present the Outline and the BibTeX references to the user for approval.

### Phase 3: Markdown Drafting (PaperOrchestra Engine) & Peer-Review
* **Action**: Act as the Section Writing Agent and the Content Refinement Agent. Draft the full paper accurately in Markdown format, pulling facts exclusively from user data and verified literature. After drafting, run a self-peer-review pass to refine clarity, logic, and scientific tone.
* **[USER REVIEW GATE]**: Save the Markdown draft (`manuscript.md`) to the user's workspace and present it. Do not proceed to formatting until the user reviews and is satisfied with the content.

### Phase 4: Data Visualization attached to Draft
* **Action**: Write and execute Python scripts (e.g., using `matplotlib` or `seaborn`) via `run_command` to generate visually appealing academic plots (e.g., ROC curves, Bar charts, Architecture diagrams) related to the paper's experiments.
* **Rule**: Save the images locally and embed them into the `manuscript.md` draft using Markdown image syntax (`![Caption](path)`).
* **[USER REVIEW GATE]**: Present the generated plots for approval.

### Phase 5: Multi-Format Compilation (HTML, DOCX, PDF)
* **Action**: Once the user approves the Markdown draft and plots, you must systematically convert the manuscript into three formats natively onto the disk:
  1. **HTML File**: Use `write_to_file` to create a beautiful, standalone academic HTML document. Use Google Fonts, embed simple CSS for styling, and include MathJax scripts for LaTeX equation rendering.
  2. **DOCX File**: Write and execute a Python script using libraries like `python-docx` or `markdown2` to convert the markdown/HTML into a Word document (`.docx`). If libraries are missing, install them dynamically (`pip install python-docx`) via `run_command` or recommend `pandoc`.
  3. **PDF File**: Write and execute a Python script using `pdfkit`, `weasyprint`, or headless Playwright to generate a pristine PDF. If you cannot generate it computationally, guide the user to print the generated HTML file to PDF via their browser.
* **Output**: Return the exact local paths of the 3 final compiled documents to the user.
