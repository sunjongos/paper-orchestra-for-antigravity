# PaperOrchestra for Antigravity 🎻

**PaperOrchestra** is an autonomous, native Tool-Using Multi-Agent Teams skill designed exclusively for the **Antigravity AI Environment**. It transforms loose research topics into submission-ready academic manuscripts through a rigorous 5-Phase autonomous pipeline.

Unlike traditional CLI architectures that force users to run Python scripts manually, this repository operates 100% natively as an Antigravity SKILL. The Antigravity AI dynamically spawns sub-personas, takes control of your local workspace, executes code, critiques its own writing, and renders formatted documents—all without requiring you to leave the chat.

## 🚀 Key Features

- **Native Tool Integration**: Utilizes Antigravity's internal tools (`run_command`, `write_to_file`, `search_web`) to orchestrate the entire process natively.
- **Multi-Persona Architecture**:
  - 🕵️‍♂️ **RESEARCHER**: Extracts hypotheses, outlines papers, and performs semantic web searches for real citations (Zero-Hallucination).
  - ✍️ **ACADEMIC WRITER**: Drafts high-quality markdown texts in formal SCI-level tone.
  - 📊 **DATA CODER**: Writes and executes Python visualization scripts (`matplotlib`/`seaborn`) locally to render and embed data graphics (e.g., ROC Curves).
  - 🧐 **PEER REVIEWER**: Harsh Self-Critique loop (Reviewer 2 Mode) that checks logical flow and rewrites markdown if weak.
  - 🖨️ **COMPILER**: Generates fully formatted final files in priority sequence: **HTML** -> **DOCX** -> **PDF**.

## 🛠️ How to Use

1. Ensure the `SKILL.md` is loaded into your Antigravity skills directory (`~/.gemini/antigravity/skills/paper-orchestra/`).
2. Open your Antigravity chat UI.
3. Simply command:
   > *"paper-orchestra 구동시켜. 주제는 [Your Topic]이야."*

### ⏳ Human-In-The-Loop (HITL) Gate
After Phase 1 (Research), the engine will intentionally PAUSE. 
It will present the Outline, Hypothesis, and Citations. It will wait for your explicit **Approval ("진행해")** before committing to the heavy drafting and coding phases.

## 📝 Output Pipeline
By user preference, the system sequentially compiles and delivers:
1. `manuscript.html` (Primary, responsive web visualization)
2. `manuscript.docx` (For traditional editing)
3. `manuscript.pdf` (Requires `weasyprint` or `wkhtmltopdf` on the host OS)

---
*Built autonomously by Antigravity AI Assistant.*
