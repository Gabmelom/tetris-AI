# Tetris AI

An autonomous Tetris player built with Python and Pygame. The agent simulates
the available placements for each falling piece, evaluates the resulting
boards with a hand-designed heuristic, and plays the lowest-cost move.

## Academic context

This was developed as a team project for **COMP 3106 — Introduction to
Artificial Intelligence** at **Carleton University** during Winter 2022. The
course project asked teams to choose a problem and solve it using artificial
intelligence methods.

The Tetris game in `tetris.py` is adapted from Laria Carolin Chabowski's
open-source Pygame implementation. Its original copyright and MIT permission
notice are retained at the top of that file. The AI player and related game
changes were developed for the course project.

## How it works

For every falling tetromino, the agent:

1. Enumerates every unique rotation and legal horizontal position.
2. Simulates dropping the piece and clearing any completed rows.
3. Scores each resulting board using a heuristic that heavily penalizes holes
   and cavities, with larger penalties for deeper or taller obstructions.
4. Uses greedy best-first selection to choose the state with the lowest
   heuristic value.
5. Rotates, positions, and instantly drops the live piece before repeating the
   process for the next one.

The Pygame event loop and AI loop run concurrently on separate threads so the
game remains visible and responsive while the agent plays.

Concepts demonstrated include:

- state-space and successor-state generation;
- heuristic evaluation and greedy best-first selection;
- game-state simulation and matrix manipulation;
- collision detection and line-clearing logic;
- real-time event loops and threading.

The agent is intentionally simple: it evaluates only the current piece and
does not perform multi-piece lookahead or learn its heuristic from data.

## Requirements

- Python 3
- Pygame (listed in `requirements.txt`)

## Running the AI

From the repository root, create and activate a virtual environment:

```bash
python -m venv .venv
```

PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS or Linux:

```bash
source .venv/bin/activate
```

Install the single dependency:

```bash
python -m pip install -r requirements.txt
```

Then start the autonomous player:

```bash
python AI.py
```

To play manually instead:

```bash
python tetris.py
```

Manual controls:

| Key | Action |
| --- | --- |
| Left / Right | Move the piece |
| Down | Drop faster |
| Up | Rotate clockwise |
| Enter | Instantly drop |
| P | Pause or resume |
| Space | Start a new game after game over |
| Escape | Quit |

## Project structure

- `AI.py` — board simulation, heuristic evaluation, move selection, and the
  threaded autonomous-player entry point.
- `tetris.py` — Pygame game implementation, rendering, controls, collision
  detection, scoring, and board updates.
- `requirements.txt` — Python dependency list.
