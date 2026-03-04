# Excalidraw Diagram Skill

A coding agent skill that generates Excalidraw diagrams from natural language descriptions. Not just boxes-and-arrows — diagrams that **argue visually**. Works natively with **Obsidian** (outputs `.md` files the Excalidraw plugin reads directly) and with standard `.excalidraw` files for sharing.

Compatible with any coding agent that supports skills. For agents that read from `.claude/skills/` (like [Claude Code](https://docs.anthropic.com/en/docs/claude-code) and [OpenCode](https://github.com/nicepkg/OpenCode)), just drop it in and go.

## What Makes This Different

- **Diagrams that argue, not display.** Every shape mirrors the concept it represents — fan-outs for one-to-many, timelines for sequences, convergence for aggregation. No uniform card grids.
- **Obsidian-native output.** Generates `.md` files with Excalidraw frontmatter that open directly in Obsidian with zero extra steps. Standard `.excalidraw` files also supported for sharing.
- **Evidence artifacts.** Technical diagrams include real code snippets and actual JSON payloads — not generic placeholder labels.
- **Built-in visual validation.** A Playwright-based render pipeline lets the agent see its own output, catch issues (overlapping text, misaligned arrows), and fix them in a loop before delivering.
- **Brand-customizable.** All colors and brand styles live in a single file (`references/color-palette.md`). Swap it out and every diagram follows your palette.

## Installation

Clone or download this repo, then copy it into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/alialfredji/excalidraw-diagram-skill.git
cp -r excalidraw-diagram-skill .claude/skills/excalidraw-diagram
```

**Prerequisites for Obsidian output:** [Obsidian](https://obsidian.md/) with the [Excalidraw plugin](https://github.com/zsviczian/obsidian-excalidraw-plugin) installed.

Clone or download this repo, then copy it into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/coleam00/excalidraw-diagram-skill.git
cp -r excalidraw-diagram-skill .claude/skills/excalidraw-diagram
```

## Setup

The skill includes a render pipeline that lets the agent visually validate its diagrams. There are two ways to set it up:

**Option A: Ask your coding agent (easiest)**

Just tell your agent: *"Set up the Excalidraw diagram skill renderer by following the instructions in SKILL.md."* It will run the commands for you.

**Option B: Manual**

```bash
cd .claude/skills/excalidraw-diagram/references
uv sync
uv run playwright install chromium
```

## Usage

Ask your coding agent to create a diagram:

> "Create an Excalidraw diagram of our authentication flow"
> *→ saves as `auth-flow.flowchart.md` — open directly in Obsidian*

> "Draw a system architecture diagram for the data pipeline"
> *→ saves as `data-pipeline.hierarchy.md`*

> "Create a standard excalidraw of the AG-UI protocol streaming events"
> *→ saves as `.excalidraw` for sharing on excalidraw.com*

The skill handles the rest — concept mapping, layout, JSON generation, rendering, and visual validation.
For Obsidian files, open them in Obsidian and switch to Excalidraw view via MORE OPTIONS (⋮) → "Switch to Excalidraw view".

## Customize Colors

Edit `references/color-palette.md` to match your brand. Everything else in the skill is universal design methodology.

## File Structure

```
excalidraw-diagram/
  SKILL.md                          # Design methodology + workflow
  references/
    color-palette.md                # Brand colors (edit this to customize)
    element-templates.md            # JSON templates for each element type
    json-schema.md                  # Excalidraw JSON format reference
    render_excalidraw.py            # Render .excalidraw or Obsidian .md to PNG
    render_template.html            # Browser template for rendering
    pyproject.toml                  # Python dependencies (playwright)
```
