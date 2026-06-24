


<div align="center">

#  Micro-State-Space

<img width="728" height="416" alt="image" src="https://github.com/user-attachments/assets/cbc8c39c-06ff-443e-af5e-80b9881b7580" />


</div>


A compact research and experimentation repository for **micro-scale adversarial game environments** built with **Streamlit**, **Matplotlib**, and lightweight **search + learning agents**.

This repository contains three standalone strategy arenas:

- **Hex-Line Arena** — a 7-hex connection game with dual win conditions.
- **Quantum Match Arena** — a 2×2 token-control game with placement and flip actions.
- **Shift-3 Arena** — a 5-square sliding-piece game with repetition-aware tactical play.

Each module is designed as a self-contained environment with:

- explicit game-state logic,
- legal move generation,
- terminal-state detection,
- heuristic evaluation,
- MCTS-based search,
- alpha-beta negamax support,
- tabular reinforcement-style updates,
- self-play training,
- visual analytics,
- agent save/load packaging.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Highlights](#repository-highlights)
- [Included Arenas](#included-arenas)
  - [Hex-Line Arena](#hex-line-arena)
  - [Quantum Match Arena](#quantum-match-arena)
  - [Shift-3 Arena](#shift-3-arena)
- [AI and Search Architecture](#ai-and-search-architecture)
- [Installation](#installation)
- [Running the Apps](#running-the-apps)
- [Training Workflow](#training-workflow)
- [Saving and Loading Agents](#saving-and-loading-agents)
- [Repository Structure](#repository-structure)
- [Dependencies](#dependencies)
- [Design Notes](#design-notes)
- [Research Use Cases](#research-use-cases)
- [Future Extensions](#future-extensions)
- [License](#license)

---

## Project Overview

`Micro-State-Space` explores how much strategic depth can be extracted from very small, fully specified game worlds.

The project is intentionally focused on **micro state spaces** rather than large-scale gameplay. That design choice makes the environments ideal for:

- rapid search experiments,
- self-play comparisons,
- heuristic tuning,
- policy/value approximation,
- explanation-friendly AI behavior,
- reproducible game-theoretic analysis.

Although the boards are compact, the decision spaces are non-trivial. Each arena combines:
- tactical forcing moves,
- board geometry constraints,
- tempo and mobility management,
- threat detection,
- and multiple layers of evaluation.

---

## Repository Highlights

### 1. Three independent game environments
Each game can be run separately as its own Streamlit application.

### 2. Compact but expressive AI pipelines
The agents combine:
- **MCTS + PUCT** for guided exploration,
- **Negamax + Alpha-Beta pruning** for tactical lookahead,
- **heuristic evaluation** for policy/value estimates,
- **Q-learning style tables** for tabular reinforcement updates,
- **self-play training** for iterative improvement.

### 3. Interactive visualization
Each module includes visual tools such as:
- board renderers,
- move-history plots,
- training curves,
- state summaries,
- winner indicators,
- and compact diagnostics for tactical patterns.

### 4. Portable agent checkpoints
Trained agents can be:
- serialized,
- bundled into a ZIP archive,
- downloaded,
- restored later,
- and reused across sessions.

---

## Included Arenas

---

## Hex-Line Arena

### Core idea

Hex-Line is a minimalist connection game played on a **7-hex cluster**:

- 1 center hex
- 6 surrounding outer hexes

The game is deliberately small, but the geometry creates meaningful tactical tension.

### Win conditions

A player wins by either:

1. forming a line through the center:
   - `[1, 0, 4]`
   - `[2, 0, 5]`
   - `[3, 0, 6]`

2. controlling **4 or more outer hexes**

This dual-win structure makes the game fast, decisive, and tie-free in spirit.

### Key characteristics

- **Board size:** 7 cells
- **Players:** 2
- **Move type:** place one token on an empty hex
- **Termination:** immediate win or exhaustion of legal moves
- **State encoding:** board tuple + current player
- **History tracking:** move list and event log

### Strategic themes

Hex-Line rewards:
- center control,
- outer-ring domination,
- fork creation,
- blocking line completion,
- and tactical tempo efficiency.

### AI components

The Hex-Line agent includes:
- MCTS with PUCT selection,
- negamax with alpha-beta pruning,
- heuristic policy/value estimation,
- self-play reinforcement,
- tabular Q-learning updates,
- epsilon-based exploration,
- temperature-based sampling during training.

### Visual and analytics support

The module includes:
- board rendering,
- training charts,
- move statistics,
- agent serialization,
- and ZIP-based load/save utilities.

---

## Quantum Match Arena

### Core idea

Quantum Match is a **2×2 grid** token-control game with a shared pool of **4 tokens**.

Each turn, a player may:

- **PLACE** a token from the shared pool onto an empty square, or
- **FLIP** an opponent-controlled token to their own color

### Win condition

A player wins when they control **all 4 squares** after a move.

### Key characteristics

- **Board size:** 4 cells
- **Token pool:** 4 total tokens
- **Move types:** place / flip
- **State encoding:** board tuple + current player + remaining pool
- **Termination:** all squares controlled by one player
- **History tracking:** structured action log

### Strategic themes

Quantum Match emphasizes:
- material conversion,
- tempo,
- board saturation,
- flip pressure,
- and short-horizon tactical dominance.

Because every move can either expand presence or reverse control, the game has a compact but highly dynamic decision surface.

### AI components

The Quantum Match agent includes:
- MCTS + PUCT,
- alpha-beta negamax search,
- heuristic evaluation of ownership and flip pressure,
- self-play learning,
- Q-learning style value tables,
- exploration decay over time,
- policy table updates from game outcomes.

### Visual and analytics support

The module includes:
- board rendering,
- action-history plots,
- training analytics,
- agent serialization,
- and ZIP packaging for portable checkpoints.

---

## Shift-3 Arena

### Core idea

Shift-3 is a **5-square linear sliding game** where pieces do not merely get placed once; they can also be shifted left or right, which makes the board dynamic and potentially cyclical.

Each player can:
- **PLACE** a piece,
- or **SLIDE** an existing piece by one square left or right

### Win condition

The primary winning pattern is:

- **Surround pattern:** `[You, Opponent, You]`

This gives the game a positional, pattern-based identity rather than a pure occupancy identity.

### Key characteristics

- **Board size:** 5 cells
- **Move types:** place / slide
- **Repetition awareness:** position cycling is tracked
- **Termination safeguards:** max move limit and repeated-state logic
- **History tracking:** full move record and event log

### Strategic themes

Shift-3 is particularly useful for studying:
- mobility constraints,
- positional loops,
- repetition handling,
- threat distance,
- sliding piece geometry,
- and constrained search in a small state space.

### AI components

The Shift-3 agent includes:
- MCTS with PUCT,
- negamax + alpha-beta pruning,
- evaluation focused on surround threats and mobility,
- loop-aware tactical reasoning,
- self-play reinforcement,
- Q-learning style table updates,
- exploration and temperature control.

### Visual and analytics support

The module includes:
- board rendering,
- heatmap visualization,
- move-history analysis,
- training charts,
- agent save/load support,
- and ZIP packaging.

---

## AI and Search Architecture

The repository uses a layered decision stack that is intentionally lightweight, inspectable, and appropriate for tiny game spaces.

### 1. Monte Carlo Tree Search (MCTS)
Used to explore candidate actions by simulating outcomes and accumulating visit/value statistics.

### 2. PUCT selection
The tree policy uses a PUCT-style formulation to balance:
- prior preference,
- visit counts,
- exploitation,
- exploration.

### 3. Negamax with Alpha-Beta pruning
Used as a tactical search baseline to:
- evaluate forcing sequences,
- prune low-value branches,
- and provide deeper local reasoning than shallow heuristics alone.

### 4. Heuristic evaluation
Each game includes game-specific evaluation terms, such as:
- center control,
- outer-ring pressure,
- flip pressure,
- surround distance,
- mobility advantage,
- blocking potential,
- repetition risk.

### 5. Tabular reinforcement
Agents maintain compact state-action or state-value tables, making the system:
- easy to inspect,
- easy to serialize,
- and easy to experiment with.

### 6. Self-play learning
The repository includes self-play training loops that can:
- generate episodes,
- collect outcome statistics,
- update tables,
- decay exploration,
- and visualize learning progress.

---

## Installation

### Recommended environment

- Python 3.10 or later
- Streamlit
- Matplotlib
- Pandas
- NumPy

### Install dependencies

```bash
pip install streamlit matplotlib pandas numpy
```

If you are using a virtual environment:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install streamlit matplotlib pandas numpy
```

---

## Running the Apps

Each file is a standalone Streamlit app.

### Hex-Line Arena

```bash
streamlit run hex_line.py
```

### Quantum Match Arena

```bash
streamlit run quantum_match.py
```

### Shift-3 Arena

```bash
streamlit run shift3.py
```

---

## Training Workflow

Each arena includes a self-play workflow in the sidebar.

Typical training flow:

1. open the app,
2. choose the number of training episodes,
3. configure search depth / simulations / learning rate settings,
4. start self-play training,
5. review the chart outputs,
6. save the resulting agents as a ZIP archive.

### Training behavior

During training, the agents may:
- choose exploratory actions,
- decay epsilon over time,
- decay temperature over time,
- update Q-style tables,
- collect win/loss statistics,
- and store episode-level metrics.

### Training analytics

The repository surfaces trends such as:
- win rates,
- draw rates,
- epsilon decay,
- temperature decay,
- average game length,
- move distributions,
- and training progress over episodes.

---

## Saving and Loading Agents

The repository supports portable agent bundles.

### Save format

Each ZIP archive contains:

- `agent1.json`
- `agent2.json`
- `config.json`

### What is stored

The saved data typically includes:
- learning rate,
- gamma,
- epsilon,
- temperature,
- search depth,
- MCTS simulations,
- Q-tables or state tables,
- and configuration metadata.

### Why this is useful

This makes it easy to:
- preserve trained agents,
- compare checkpoints,
- share experiment snapshots,
- and reload models for later analysis.

### Practical workflow

- train agents,
- download the ZIP,
- upload the ZIP later,
- resume evaluation or comparison.

---

## Repository Structure

The repository currently centers on three Python modules:

```text
Micro-State-Space/
├── hex_line.py
├── quantum_match.py
└── shift3.py
```

### File responsibilities

- **`hex_line.py`**  
  Implements the Hex-Line board, AI agent, visualizations, training loop, and save/load workflow.

- **`quantum_match.py`**  
  Implements the Quantum Match board, structured actions, AI agent, visualizations, training loop, and save/load workflow.

- **`shift3.py`**  
  Implements the Shift-3 board, sliding mechanics, repetition-aware logic, AI agent, visualizations, training loop, and save/load workflow.

---

## Dependencies

The code base uses the following Python libraries:

- **streamlit** — web UI and app framework
- **matplotlib** — board rendering and analytics
- **pandas** — tabular history analysis
- **numpy** — numerical helpers, especially in Shift-3
- **random**, **math**, **time**, **json**, **zipfile**, **io**, **copy**, **dataclasses**, **typing** — standard library support for game logic, serialization, and training

---

## Design Notes

### Small state spaces, rich behavior
The project intentionally uses compact boards to keep the state space small enough for:
- deep inspection,
- fast testing,
- and readable AI behavior.

### Deterministic game logic
The rules are encoded directly in Python, making the environments:
- reproducible,
- transparent,
- and easy to debug.

### Research-friendly implementation
The code is suitable for examining:
- search-vs-heuristic tradeoffs,
- self-play dynamics,
- reinforcement from compact state spaces,
- and game-specific evaluation functions.

### Explainability first
Rather than hiding logic inside a large neural network, the repository uses explicit, inspectable scoring terms and search procedures. That makes it especially valuable for educational and experimental use.

---

## Research Use Cases

This repository can be used for:

- adversarial search demonstrations,
- AI agent benchmarking,
- heuristic evaluation experiments,
- tabular reinforcement learning tests,
- self-play comparisons,
- compact state-space analysis,
- teaching MCTS and alpha-beta pruning,
- studying repetition handling in board games,
- studying board geometry and tactical forcing patterns.

---

## Future Extensions

Possible directions for further development include:

- adding a unified launcher page for all three games,
- introducing stronger evaluation functions,
- recording and replaying complete game transcripts,
- exporting training logs to CSV or Parquet,
- adding head-to-head tournament modes,
- implementing deeper search variants,
- integrating visualization dashboards for agent comparisons,
- and building a shared configuration layer for all modules.

---

## License

MIT License

Copyright (c) 2026 Devanik

---

## Closing Summary

`Micro-State-Space` is a technically focused collection of tiny adversarial environments built for clarity, experimentation, and controlled AI evaluation.

Its core value lies in the combination of:

- small boards,
- complete rule definitions,
- search-based decision making,
- self-play learning,
- rich visual analytics,
- and portable agent checkpoints.

Even though the environments are minimal, the design space is not. Each arena is compact enough to inspect, yet rich enough to study meaningful tactical and algorithmic behavior.
