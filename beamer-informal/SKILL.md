---
name: beamer-informal
description: Create informal, visually engaging LaTeX Beamer slides for educational math explainer videos, using intuitive explanations, mathematical diagrams, worked examples, and custom playful styling.
workflow_stage: communication
compatibility:
  - claude-code
  - cursor
  - codex
  - gemini-cli
author: MinhTa
version: 1.0.0
tags:
  - LaTeX
  - Beamer
  - mathematics
  - education
  - explainer-videos
---

# Informal Beamer Math Explainer

## Purpose

Create visually engaging, mathematically rigorous Beamer presentations for recorded math explainer videos.

Target style: informal educational videos, not academic lectures. Slides should help viewers understand mathematical ideas through intuition, examples, diagrams, visual transformations, and storytelling. Encourage the use of emoji.

The result must compile into a 16:9 PDF suitable for screen recording or video editing.

## When to Use

- Explaining mathematical concepts, theorems, proofs, or formulas
- Creating educational YouTube videos
- Visualizing algebra, geometry, calculus, probability, statistics, and discrete mathematics
- Explaining scientific ideas using mathematics
- Turning a script or outline into visual teaching slides

## Core Principles

### 1. Teach through visual storytelling

Build an explanation as a sequence of discoveries:

1. **Hook:** Start with a surprising question, puzzle, paradox, or concrete problem.
2. **Intuition:** Establish an intuitive understanding before introducing formal notation.
3. **Discovery:** Show how the mathematical idea emerges.
4. **Formalization:** Introduce definitions, equations, or proofs when viewers have sufficient context.
5. **Application:** Solve a concrete problem or reveal an unexpected consequence.
6. **Payoff:** Resolve opening question and summarize central insight.

Adapt this sequence to topic. Do not force every presentation into a fixed structure.

Avoid academic conventions such as literature reviews, research questions, methodology sections, and conference roadmaps unless topic genuinely requires them.

### 2. One visual idea per slide

- Each slide should communicate one primary idea.
- Prefer one equation, diagram, graph, construction, or worked step over several competing elements.
- Split complicated derivations into multiple slides.
- Use short conversational phrases instead of paragraph-length explanations.
- Use whitespace intentionally.
- Do not compress too much content onto one slide merely to reduce slide count.

### 3. Design for video, not live presentations

Slides appear inside a video player and may be viewed on small screens.

- Use 16:9 aspect ratio.
- Prefer large equations, labels, and diagrams.
- Use approximately 28–36 pt for ordinary text and 36–48 pt for major equations when practical.
- Keep essential labels readable at reduced video resolution.
- Maintain strong contrast between foreground and background.
- Avoid tiny footnotes, dense tables, and unnecessarily decorative elements.
- Do not rely on viewers reading lengthy text while narration continues.
- Keep titles short; omit titles when the visual itself establishes context.

These font sizes are starting points, not rigid constraints. Adjust based on visual density and output resolution.

### 4. Informal but mathematically precise

- Explain concepts in natural spoken language.
- Use familiar objects, concrete numbers, thought experiments, and relatable examples.
- Allow restrained humor, visual jokes, and playful annotations when they reinforce understanding.
- Introduce technical vocabulary only when useful, and explain it clearly.
- Never sacrifice mathematical correctness for entertainment.
- Distinguish intuition, conjecture, and rigorous proof.
- Verify algebra, arithmetic, notation, units, and logical implications.
- Avoid patronizing viewers or adding jokes to every slide.

### 5. Reveal mathematical ideas progressively

Treat each slide as a meaningful stage in an explanation.

Use overlays or successive frames when they help viewers follow a transformation:

- Introduce an expression before manipulating it.
- Highlight the term currently being discussed.
- Show intermediate steps in derivations.
- Reveal graph features alongside the relevant explanation.
- Compare before-and-after states.
- Remove obsolete elements when they distract from the current step.

Use `\pause`, Beamer overlays, or TikZ visibility controls selectively.

Do not animate every bullet by default. Every reveal should serve a teaching purpose.

## Workflow

### Step 1: Understand the material

Inspect any supplied script, outline, source document, or existing slides before asking questions.

If essential information is missing, ask concise questions about:

1. Topic and intended learning outcome.
2. Target audience and prerequisite knowledge.
3. Desired duration or supplied narration script.
4. Preferred language and visual style, if not established.

Do not ask questions already answered by supplied material. Use reasonable defaults for nonessential choices.

If the user supplies a complete script, proceed directly to slide planning.

### Step 2: Plan narrative and pacing

Determine the main idea, prerequisites, likely misconceptions, and desired final takeaway.

Create a slide outline containing:

- Slide number and purpose.
- Main visual or equation.
- Key teaching point.
- Narration or script segment, when provided.
- Any required reveal or transition.

Allocate time according to conceptual difficulty, not a fixed slides-per-minute rule.

Use fewer slides for sustained geometric constructions or difficult derivations, and more slides for short, contrasting visual steps.

Do not produce an academic table of contents unless it helps the audience.

### Step 3: Choose Visual Representations

Prioritize visual representations that reveal mathematical structure and support narration.

#### 3.1 Handle user-supplied images

If the user provides a script containing image files, image paths, or explicit image references:

- Insert each referenced image into an appropriate slide using `\includegraphics`.
- Do not inspect, analyze, reinterpret, or recreate the image unless the user explicitly requests it.
- Preserve the original image file and content.
- Use the surrounding script and any accompanying image description to determine placement, size, cropping, and relationship to nearby mathematical content.
- If the user describes an image's content or intended role, use that information to plan its placement and any relevant reveal or transition.
- If no image description is provided, treat the image as an opaque visual asset. Do not invent claims about its contents.
- Preserve supplied filenames and paths unless changes are necessary. If an asset is missing or its path is ambiguous, report the issue instead of inventing a replacement.

Example:

```latex
\begin{frame}[plain]
  \centering
  \includegraphics[width=0.85\textwidth]{figures/example.png}
\end{frame}
```

#### 3.2 Create mathematical visuals

Prefer representations that expose mathematical relationships rather than merely decorate slides.

Recommended tools:

- **TikZ:** Diagrams, geometric constructions, arrows, annotations, number lines, trees, and mathematical illustrations.
- **PGFPlots:** Functions, coordinate systems, curves, probability distributions, and data plots.
- **amsmath / amssymb:** Mathematical notation and aligned derivations.
- **Beamer overlays:** Progressive explanations and visual comparisons.
- **graphicx:** Display user-supplied or other appropriate external images.

Examples of effective visual teaching:

- Completing the square: show a square's area being rearranged.
- Quadratic equations: connect roots, intersections, and discriminant.
- Derivatives: compare secant and tangent slopes.
- Probability: visualize sample spaces, events, and distributions.
- Linear algebra: show transformations of vectors and geometric objects.

Prefer diagrams that explain relationships over decorative illustrations.

#### 3.3 Use simple reveals and transitions

Use Beamer's built-in overlay mechanisms to reveal information progressively when doing so improves comprehension.

Examples:

- Reveal derivation steps one at a time.
- Introduce equation terms in sequence.
- Highlight the part of a diagram currently being discussed.
- Show intermediate stages of a geometric construction.
- Reveal a final result only after establishing its motivation.
- Compare two expressions or configurations by changing which elements are visible.

Useful mechanisms include `\pause`, overlay specifications such as `<2->`, `\only`, `\uncover`, and `\visible`.

Choose the simplest mechanism that achieves the intended effect. Prefer stable layouts in which elements appear or disappear without unrelated content jumping around.

Do not add reveals to every slide by default. Each reveal must serve a clear teaching or narration purpose.

Distinguish between:
- **Progressive reveals:** Content appears in stages within one frame.
- **Slide transitions:** The presentation moves from one frame to another.
- **Continuous animation:** Objects move or transform smoothly over time.

Beamer overlays primarily support progressive reveals, not continuous animation. Do not simulate elaborate continuous motion with excessive overlays.

#### 3.4 Use external visuals selectively

Use external images only when they materially improve the explanation or when the user supplies them. But User-supplied images in the script are mandatory. Never replace them with emoji/TikZ. 

Do not assume external assets are available. Do not invent file paths, create placeholder figures in a purportedly finished presentation, or claim to have generated assets that do not exist.

Prefer TikZ and PGFPlots for mathematical diagrams that benefit from precise, scalable rendering.

### Step 4: Build a Consistent Informal Theme

Use a custom, minimalistic Beamer theme designed for educational videos, not conventional academic presentations.

#### Visual defaults

- **Background:** Pure white (`RGB 255,255,255`).
- **Text:** Near-black for strong contrast.
- **Accent colors:** One primary accent and one secondary accent; add other colors only when they encode meaningful distinctions.
- **Typography:** Large, readable text with clear hierarchy between headings, equations, labels, and annotations.
- **Layout:** Generous whitespace, simple alignment, and uncluttered compositions.
- **Visual language:** Simple geometric shapes, clear arrows, restrained playful annotations, and occasional visual jokes.
- **Consistency:** Reuse colors, line widths, notation styles, and recurring visual elements throughout presentation.

Use color purposefully. For example, use one accent color to highlight a particular variable or mathematical object, and preserve that meaning across subsequent slides.

Keep decorative elements subordinate to mathematical content. Avoid excessive borders, shadows, gradients, emojis, and unrelated illustrations.

Use vector graphics whenever practical so diagrams remain crisp in video.

Do not default to Metropolis, Madrid, or standard academic title and footer layouts. Build on Beamer's default facilities with a lightweight custom style unless another theme better fits user's explicit requirements.

### Step 5: Write Narration-Friendly Slides

Slides support narration; they do not replace it.

- Display the mathematical object being discussed.
- Use short labels and annotations to direct attention.
- Align visual changes with meaningful moments in narration.
- Keep equations and diagrams synchronized with the explanation.
- Avoid long paragraphs that force viewers to read while listening to unrelated narration.
- Do not duplicate narration verbatim on slides unless wording itself is important.

If the user supplies a script:

1. Preserve its intended meaning, logical sequence, and mathematical claims.
2. Divide it into coherent narration segments.
3. Map each segment to an appropriate slide or overlay sequence.
4. Use supplied images at the positions indicated by the script or supported by accompanying descriptions.
5. Avoid unnecessary rewriting, added claims, or invented narration.
6. If a script segment has no obvious visual representation, use a concise textual slide rather than forcing an irrelevant diagram.

If the user does not supply narration, create slides around a clear teaching sequence. Add explanatory cues or a separate narration script only when requested or useful.

When generating both narration and slides, keep their content aligned. Each reveal should correspond to a meaningful point in the spoken explanation.

### Step 6: Generate Complete, Compilable LaTeX

Produce a self-contained `.tex` file unless the user requests another structure.

Include:

- Document class with 16:9 aspect ratio.
- Custom white-background theme and accent colors.
- Required packages and TikZ libraries.
- Reusable macros for notation and recurring visual elements.
- Complete slide content.
- TikZ or PGFPlots definitions where needed.
- References to actual supplied or generated assets.
- Progressive overlays where pedagogically useful.
- A title slide only when appropriate.
- An ending slide that resolves the opening question or reinforces the central insight.

#### Asset handling

- Keep user-supplied images unchanged.
- Reference assets using paths that match the actual project structure.
- Do not fabricate filenames or assume missing files exist.
- Document required external assets and dependencies.
- If the presentation depends on supplied assets, deliver them alongside the `.tex` file or preserve their existing project locations.
- Use relative paths where practical to keep the project portable.

#### Code quality

- Avoid unnecessary packages and external dependencies.
- Avoid undefined commands, conflicting package options, and invalid overlay specifications.
- Use consistent mathematical notation.
- Verify that equations and visual annotations match the intended explanation.
- Avoid placeholder content in final deliverables.
- Compile and inspect the PDF when tools are available. Fix errors and obvious layout problems before delivery.
- If compilation cannot be verified, state this explicitly.

## Default Technical Template

Use this as a starting point, not a mandatory visual design.

The default background is pure white. Select accent colors according to the subject and maintain consistent semantic use throughout the presentation.

```latex
\documentclass[aspectratio=169,11pt]{beamer}

\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage{xcolor}
\usepackage{tikz}
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}

\usetikzlibrary{
  arrows.meta,
  calc,
  positioning,
  intersections,
  angles,
  quotes,
  decorations.pathreplacing
}

% Minimal white-background palette
\definecolor{Paper}{RGB}{255,255,255}
\definecolor{Ink}{RGB}{35,38,48}
\definecolor{Blue}{RGB}{50,105,190}
\definecolor{Orange}{RGB}{230,125,55}

\setbeamercolor{background canvas}{bg=Paper}
\setbeamercolor{normal text}{fg=Ink}
\setbeamercolor{structure}{fg=Blue}
\setbeamercolor{frametitle}{fg=Ink,bg=Paper}

\setbeamertemplate{navigation symbols}{}
\setbeamertemplate{footline}{}

\setbeamerfont{frametitle}{size=\Large,series=\bfseries}
\setbeamerfont{normal text}{size=\large}

\newcommand{\highlight}[1]{\textcolor{Blue}{\mathbf{#1}}}
\newcommand{\surprise}[1]{\textcolor{Orange}{\mathbf{#1}}}

\begin{document}

\begin{frame}[plain]
  \centering
  {\Huge\bfseries Why does this work?}

  \vspace{1em}
  {\Large Start with a concrete puzzle.}
\end{frame}

\begin{frame}[plain]
  \centering
  \[
    x^2+6x+9=(x+3)^2
  \]

  \vspace{0.5em}
  {\Large One expression, two ways to see it.}
\end{frame}

\begin{frame}[plain]
  \centering
  \[
    \only<1>{x^2+6x+9}
    \only<2->{(x+3)^2}
  \]

  \vspace{1em}
  \uncover<2->{\Large Same expression, rewritten.}
\end{frame}

\end{document}
```

Customize palette, fonts, macros, layout, and overlays to fit topic. The example demonstrates basic overlay syntax; use more deliberate layouts for real presentations. Do not reuse example slide content unless relevant.

## Mathematical and Visual Quality Checks

Before delivery, verify:

1. **Correctness:** Equations, derivations, examples, and mathematical claims are correct.
2. **Progression:** Each slide follows logically from preceding explanation.
3. **Readability:** Text, equations, axes, and labels remain legible at video size.
4. **Visual clarity:** Main idea stands out without competing decoration.
5. **Consistency:** Colors, notation, spacing, and visual conventions remain coherent.
6. **Asset integrity:** Supplied images remain unchanged and referenced paths are valid.
7. **Overlay behavior:** Reveals show intended elements in correct sequence without accidental layout shifts.
8. **Compilation:** Compile with available LaTeX tools when possible and resolve errors.
9. **Dependencies:** Required packages and external assets are documented.
10. **Narration alignment:** Slide changes support explanation rather than interrupt it.
11. **Pacing:** Complex steps have enough time and space to be understood.
12. **Accessibility:** Do not rely on color alone to distinguish mathematical categories.


## Mathematical and Visual Quality Checks

Before delivering slides, check:

1. **Correctness:** Verify every equation, derivation, example, and mathematical claim.
2. **Progression:** Each slide follows logically from preceding explanation.
3. **Readability:** Text, equations, axes, and labels remain legible at video size.
4. **Visual clarity:** Main idea stands out without competing decoration.
5. **Consistency:** Colors, notation, spacing, and visual conventions remain coherent.
6. **Compilation:** Compile with available LaTeX tools when possible and resolve errors.
7. **Dependencies:** Ensure required packages and external assets are documented.
8. **Narration alignment:** Slide changes support the explanation rather than interrupt it.
9. **Pacing:** Complex steps have enough time and space to be understood.
10. **Accessibility:** Do not rely on color alone to distinguish mathematical categories.

If compilation tools are unavailable, state that compilation was not verified. Never claim that untested LaTeX compiles successfully.

## Output Format

Adapt output to the user's request.

- **Outline request:** Return slide-by-slide plan with teaching objective and visual concept.
- **Script-to-slides request:** Return complete LaTeX and preserve alignment with narration.
- **New presentation request:** Plan narrative, then generate complete LaTeX.
- **Existing presentation modification:** Preserve correct material and modify only necessary parts.
- **Code-only request:** Return LaTeX without lengthy explanations.

When creating files, use a clear project structure if multiple assets are needed:

```text
presentation/
├── main.tex
├── figures/
└── README.md
```

Include a concise description of compilation requirements and commands when useful.

## Common Pitfalls

Avoid:

- Academic conference layouts for informal educational videos.
- Dense bullet lists and paragraph-heavy slides.
- Introducing formal definitions before giving viewers intuition.
- Showing an entire proof before explaining its motivation.
- Using tiny mathematical annotations.
- Unnecessary overlays that slow down explanation.
- Decorative graphics unrelated to mathematical content.
- Overusing color, emojis, jokes, or visual effects.
- Inconsistent notation between slides.
- Unverified external images or citations.
- Placeholder content in final deliverables.
- Treating every slide as a static poster rather than one moment in a larger explanation.


