# psych-exp-flowchart

**English** | [中文](./README.zh.md)

> A Claude Code skill that generates APA-style, publication-ready experiment flowcharts from jsPsych / PsychoPy / MATLAB / Python code or plain-text trial descriptions.

---

![Preview](./figs/example1.png)

> Open [`references/example_psych_experiment_flowchart.html`](./references/example_psych_experiment_flowchart.html) in a browser to see a full interactive example.

---

## Features

- **Code parsing** — reads `config.js`, `factories.js`, `MATLAB.m` or Python `.py` scripts and extracts the trial timeline automatically
- **Natural language input** — works with plain descriptions like `"Fixation 500ms → Two images left/right 1000ms → Blank response screen 2000ms"`
- **Clarifying questions** — asks 1–3 targeted questions before generating, so the output matches your exact design
- **APA-ready styling** — pure black-and-white, Arial font, italic timing labels, bold action text
- **CSS variable panel** — every size, spacing, and color is a variable at the top of the file; adjust without touching layout code
- **Standalone HTML** — double-click to open, no server or internet required; screenshot-ready

## Output Specifications

| Property | Value |
|---|---|
| Format | Standalone `.html` |
| Style | APA-compliant (B&W, sans-serif) |
| Solid border | Formal / main trial |
| Dashed border | Practice trial |
| Italic text | Timing values (ms) |
| **Bold text** | Action labels / key prompts |
| Dependencies | None |

## Installation

**Option A — copy the skill folder**

```bash
# macOS / Linux
cp -r psych-exp-flowchart ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse psych-exp-flowchart "$env:USERPROFILE\.claude\skills\"
```

**Option B — clone into your skills directory**

```bash
cd ~/.claude/skills
git clone https://github.com/<your-repo>/psych-exp-flowchart
```

After installation, the skill is automatically available in every new Claude Code session.

## Usage

Just describe what you want in natural language — Claude picks up the skill automatically.

**From code:**

> "Read `config.js` and `factories.js` in `public/task-two-array-v2/` and generate an experiment flowchart."

**From text:**

> "Generate a flowchart: Fixation 300–1000 ms → Two columns of shapes 500 ms (left-right or top-bottom layout) → Blank response screen 2000 ms → ITI 300 ms. Keys: F = Same, J = Different."

**With options:**

> "Generate a flowchart including both the practice phase (with feedback) and the main trial."

## Workflow (what Claude does)

1. **Extract** — timing sequence, spatial layout, key mappings from code or text  
2. **Clarify** — ask 1–3 questions about ambiguous design choices  
3. **Generate** — parameterized HTML with CSS variable panel  
4. **Caption** — append APA-style Figure caption

## Example Reference

[`references/example_psych_experiment_flowchart.html`](./references/example_psych_experiment_flowchart.html) demonstrates:

- Practice phase (dashed borders) with correctness feedback
- Formal trial (solid borders)
- CSS variable parameter panel
- APA Figure caption

## Supported Experiment Frameworks

| Framework | Input type |
|---|---|
| jsPsych | `config.js`, `index.html`, `factories.js` |
| PsychoPy | `.py` experiment scripts |
| MATLAB | `.m` scripts |
| Custom | Natural language description |

## License

MIT
