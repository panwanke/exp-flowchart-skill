---
name: psych-exp-flowchart
description: Use when generating APA-style trial sequence diagrams for cognitive psychology experiments. Applies when given jsPsych, PsychoPy, MATLAB, or Python experiment scripts, or natural language descriptions of trial timelines (e.g., "Fixation 500ms → Stimulus 1000ms → Response 2000ms"). Covers fixation/stimulus/response/ITI sequences, multi-layout stimuli, and publication-ready single-trial flowchart figures.
---

# Psychology Experiment Flowchart Generator

Generates single-trial flowcharts for cognitive psychology experiments that conform to academic journal standards (e.g., APA formatting).

## Core Capabilities

1. **Deep Code Parsing:** Extracts experimental flow from `jsPsych` timeline code (JS/HTML), or from MATLAB/Python experimental scripts.
2. **Natural Language Understanding:** Converts text descriptions (e.g., "Fixation 500ms -> Two Chinese characters presented left and right for 500ms -> Blank screen response 2000ms") into a precise visual flowchart.
3. **Academic Standard Output:** Produces a pure black-and-white minimalist style with sans-serif fonts and an adjustable parameter panel.

## Workflow

### Step 1: Information Extraction

Before generating the code, clearly extract data across the following three dimensions:

1. **Temporal Sequence:**
   - Identify standard nodes: Fixation, Stimulus, Mask, Response, ITI (Inter-Trial Interval).
   - Extract the duration (ms) for each node.
2. **Spatial & Stimulus Layout:**
   - Analyze the stimulus rendering code/description to determine the number of elements simultaneously present on the screen.
   - Identify the layout structure: Left-Right, Top-Bottom, or Grid.
   - Identify special placeholders: e.g., whether a central fixation cross (`+`) remains on screen between stimulus groups.
3. **Action & Response:**
   - Extract key mappings (e.g., `F = Same, J = Different`).
   - Extract response time limits.

### Step 2: Dynamic Decision Confirmation

Do not use fixed questions. Instead, analyze the provided code or text description for ambiguities and generate 1-3 targeted questions to clarify the visualization requirements before generating the final HTML. Wait for the user's response before proceeding. 

*Examples of contexts that trigger dynamic questions:*
- **Spatial Layout Ambiguity:** If the script supports multiple layouts, ask the user which specific layout they want to visualize.
- **Stimulus Representation:** If the stimuli are complex images, ask how they should be represented in the diagram (e.g., abstract shapes like ○/■, CSS-rendered specific symbols, or simple text labels).
- **Flowchart Granularity:** Ask whether to map out a standard main trial, or if they need the practice trial included (showing correctness feedback loops).

### Step 3: Parameterized Generation

The generated HTML must include the following structure, utilizing CSS variables for easy adjustment:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  /* ===== User-defined Parameter Panel ===== */
  :root {
    /* Screen frame dimensions */
    --frame-width: 160px;
    --frame-height: 120px;
    --frame-border-width: 3px;
    
    /* Stimulus dimensions */
    --stim-size: 32px;
    --text-size: 28px;
    --fixation-size: 24px;
    
    /* Spacing and arrows */
    --arrow-length: 40px;
    --arrow-thickness: 2px;
    --layout-gap: 30px;
    
    /* Colors (Grayscale only) */
    --border-color: #000000;
    --bg-color: #ffffff;
    --text-color: #333333;
  }
  
  /* Base styles */
  body { 
    font-family: Arial, Helvetica, sans-serif;
    background: var(--bg-color);
  }
  
  .screen-box {
    width: var(--frame-width);
    height: var(--frame-height);
    border: var(--frame-border-width) solid var(--border-color);
    background: var(--bg-color);
  }
  
  .arrow {
    width: var(--arrow-length);
    height: var(--arrow-thickness);
    background: var(--border-color);
  }
</style>
</head>
<body>
  </body>
</html>

```

### Step 4: Figure Caption Generation

Automatically add an academic-style Figure Caption at the bottom of the flowchart:

```html
<div class="figure-caption">
  <strong>Figure 1.</strong> Single-trial timeline flowchart (Example: Abstract homogeneous condition). 
  A fixation cross is presented for 300-1000 ms, followed by the stimulus for 500 ms. Participants must make a judgment within 2000 ms (press 'F' for "Same", press 'J' for "Different"). The inter-trial interval is 300 ms.
</div>

```

## Visual Specifications (Academic Journal Standards)

1. **Color:** Pure white background, solid black borders.
2. **Font:** Arial or Helvetica (sans-serif).
3. **Time Parameters:** Italicized (`font-style: italic`).
4. **Action Descriptions:** Bolded (`font-weight: bold`).
5. **Flow Direction:** Left-to-Right layout.
6. **Borders:**
* Solid lines = Formal/Main trials.
* Dashed lines = Practice trials.



## Quick Reference

| Step | Action | Key rule |
|------|--------|----------|
| 1 | Parse code / description | Extract timing, layout, keys |
| 2 | Ask 1–3 targeted questions | Only about real ambiguities |
| 3 | Generate parameterized HTML | CSS variables at top, no external libs |
| 4 | Append Figure Caption | APA format, italic timing, bold keys |

| Visual token | Rule |
|---|---|
| Solid border | Formal trial |
| Dashed border | Practice trial |
| Italic text | Timing values |
| **Bold text** | Action labels / key prompts |

## Output Requirements

* Generate a standalone `.html` file.
* Absolutely no dependencies on external libraries (e.g., no Bootstrap, no React).
* Must be viewable simply by double-clicking the file in a browser, ready for clean screenshots.
* Adaptable to double-column academic formatting (compact layout).

## Example Reference

Reference file: `example_psych_experiment_flowchart.html` in the `references` folder.

This file demonstrates:

* Practice phase flow (dashed borders).
* Formal experiment flow (solid borders).
* Parameterized CSS variable panel.
* Bottom information box (experiment design parameters).

