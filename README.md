# VisualizeNavigationAlgorithms

*A real-time maze visualiser that races **BFS**, **DFS** and **A\*** side-by-side, complete with procedural audio feedback.  
Generated in twelve AI-driven commits and archived read-only on **2025-06-28**.*  

---

<details>
<summary>Table of Contents</summary>

1. [Introduction](#introduction)  
2. [Key Features](#key-features)  
3. [Quick Start](#quick-start)  
4. [Controls & CLI Options](#controls--cli-options)  
5. [Project Structure](#project-structure)  
6. [AI Generation Process](#ai-generation-process)  
7. [Customisation Guide](#customisation-guide)  
8. [License](#license)  
9. [Appendix A – AI Prompt Templates](#appendix-a--ai-prompt-templates)  

</details>

---

## 1. Introduction <a id="introduction"></a>

**VisualizeNavigationAlgorithms** is a single-file Python program that

* generates a random perfect maze (with adjustable “complexity” openings),  
* launches three panes showing **BFS**, **DFS** and **A\*** path-finding in parallel,  
* renders coloured frontiers, explored nodes and final paths in real time, and  
* plays sine-wave tones whose pitch tracks each algorithm’s progress, finishing with a victory chord.  

Everything lives in one script, making it ideal for teaching search algorithms,  
visualisation techniques and basic audio synthesis with **Pygame**.

---

## 2. Key Features <a id="key-features"></a>

- **Minimal dependencies**  
  - Python ≥ 3.8  
  - Pygame 2.x → `pip install pygame`
- **Three algorithms in parallel** — BFS, DFS and A\* share the same maze seed.  
- **Fully interactive** — resizable window, zoom-to-fit, **M** to mute, ESC to quit.  
- **Procedural audio** — continuous tones + success jingles, no external sound files.  
- **Command-line tweaks** — grid size, speed, complexity, auto-test mode and more.

---

## 3. Quick Start <a id="quick-start"></a>

```bash
# 1 – Install dependency
python -m pip install -U pygame

# 2 – Clone repository
git clone https://github.com/OperaAIBot/VisualizeNavigationAlgorithms.git
cd VisualizeNavigationAlgorithms

# 3 – Run (defaults to a 61×61 maze)
python maze_pathfinding_simulation.py
```

> **Tip** Use a virtual environment:  
> `python -m venv venv && source venv/bin/activate`

---

## 4. Controls & CLI Options <a id="controls--cli-options"></a>

| Key / Option            | Effect |
| ----------------------- | ------ |
| **M**                   | Mute / un-mute audio |
| **ESC**                 | Quit simulation |
| `--grid-size N`         | Maze size (odd 50-100, default 61) |
| `--speed-index 0-4`     | 0 = fastest, 4 = slowest |
| `--complexity 0-1`      | Extra wall openings (default 0.75) |
| `--auto-test`           | Headless run, exits on success |
| `--strict-completion`   | Fail if *all* algorithms don’t finish |

---

## 5. Project Structure <a id="project-structure"></a>

```text
VisualizeNavigationAlgorithms/
 ├─ maze_pathfinding_simulation.py   # full simulation logic
 └─ LICENSE                          # GNU GPL v3.0
```

All visuals and sounds are generated at runtime; no external assets required.

---

## 6. AI Generation Process <a id="ai-generation-process"></a>

The program was produced in **12 AI-assisted commits** with an iterative
“generate-test-fix” loop powered by the autonomous agent in `SimuationAgent.py`.
The repo was **archived read-only on 2025-06-28** after the final green run.  

---

## 7. Customisation Guide <a id="customisation-guide"></a>

| What to tweak            | Variable / flag | Notes |
| ------------------------ | -------------- | ----- |
| Maze size & complexity   | `--grid-size`, `--complexity` | Larger → slower |
| Visual speed             | `--speed-index` | Lower index = more updates / frame |
| Colour palette & fonts   | Edit constants near the top of the script |
| Audio behaviour          | Press **M** or set `audio.muted = True` in code |
| Algorithms               | Drop-in any class with `.step()`/`.progress()` |

---

## 8. License <a id="license"></a>

Released under the **GNU General Public License v3.0**.  
Any derivative must remain GPL-3.0; see `LICENSE` for details.

---

## Appendix A – AI Prompt Templates <a id="appendix-a--ai-prompt-templates"></a>

> The agent (`SimuationAgent.py`) relies on a library of reusable message
> templates. Below are the **raw prompt texts** it sends to the OpenAI API.  

### A.1 Partial-Fix **System** Prompt

```text
You are an expert Python and Pygame developer.
Fix the specific error in the provided code with minimal changes.

CRITICAL RULES:
- Provide ONLY the complete corrected Python code
- Use a single ```python code block
- No explanations or text outside the code block
- Fix only what's necessary to resolve the reported error
- Maintain the project goal: {self.project_goal}
```

### A.2 Partial-Fix **User** Prompt Template

```text
PROJECT GOAL: {self.project_goal}

Fix ONLY the specific error in the Python code for '{filename}'.
Do NOT rewrite the entire code. Only modify the minimal parts necessary.

ERROR TO FIX:
{error_message}

{error_line_info}

CURRENT CODE:
```python
{code}
```

INSTRUCTIONS:
You must respond with ONLY the corrected code in a single code block.
Fix only what is necessary to resolve the error.
Do not include explanations, markdown formatting outside the code block, or any other text.

Provide the complete corrected code:
```

### A.3 Full-Rewrite **System** Prompt

```text
You are an expert Python developer. 
Fix the provided code to achieve: {self.project_goal}

REQUIREMENTS:
- Provide complete, working Python code
- Use a single ```python code block
- No explanations or text outside the code block
- Fix all errors and ensure the code runs properly

CRITICAL RULES FOR SIMULATION DESIGN:
- Design a NEW, DIFFERENT maze layout for this iteration (iteration {self.iteration_count})
- Ensure the simulation has clear completion conditions
- Implement proper algorithm visualisation that works reliably
- Avoid infinite loops, deadlocks, or unescapable situations
- Include automatic testing support with the '--auto-test' flag
```

### A.4 Full-Rewrite **User** Prompt Template

```text
PROJECT GOAL: {self.project_goal}

Fix the Python code for '{filename}' to resolve the error and achieve the project goal.

The simulation has the following error:
----------------
{error_message}
----------------

Current code:
```python
{code}
```

Provide ONLY the complete corrected Python code in a single code block. No explanations.
```

### A.5 New-Code **System** Prompt

```text
You are an expert Python developer specialised in creating stable, reliable code.
Create code to achieve: {self.project_goal}

REQUIREMENTS:
- Start with: # filename: chosen_filename.py
- Provide complete Python code in ```python code blocks
- No explanations outside the code block
- Ensure the code achieves the project goal
- Include automatic testing capability with '--auto-test'
```

### A.6 New-Code **User** Prompt Template

```text
PROJECT GOAL: {self.project_goal}

Current project state:
Files: {files}
Directory structure: {structure}

Create complete Python code from scratch to achieve the project goal.

At the VERY BEGINNING of your response, include: # filename: chosen_filename.py
Then provide ONLY Python code in a code block, no explanations.
```

### A.7 Simplified-Version **System** Prompt

```text
You are an expert Python developer.
Create a simplified version of the pathfinding visualisation that focuses on core functionality.

REQUIREMENTS:
- Provide ONLY the complete Python code
- Implement a smaller 20×20 maze
- Simplify visual effects
- Maintain automatic testing with '--auto-test'
```

### A.8 Alternative-Approach **System** Prompt

```text
You are an expert Python developer.
Create an alternative implementation of the pathfinding visualisation using a different approach.

REQUIREMENTS:
- Provide ONLY the complete Python code
- You may switch to tkinter or simplify pygame radically
- Focus on algorithm correctness and stability
- Keep '--auto-test' functional
```

### A.9 Incremental-Implementation **System** Prompt

```text
You are an expert Python developer.
Create an incremental implementation of the pathfinding visualisation, starting with just one algorithm.

REQUIREMENTS:
- Provide ONLY the complete Python code
- Implement BFS first with perfect visualisation
- Add clear completion conditions
- Ensure maze generation works correctly
```

### A.10 Fix-CLI-Args **System** Prompt

```text
You are an expert Python developer.
Fix the command-line argument handling in the pathfinding visualisation.

REQUIREMENTS:
- Provide ONLY the complete Python code
- Make all arguments optional with sensible defaults
- Ensure '--auto-test' runs without extra flags
- Maintain full functionality
```
---
