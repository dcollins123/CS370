# CS 370 — Treasure Hunt
 
**Category:** Algorithms and Data Structures
**Original course:** CS 370 — Current and Emerging Trends in Computer Science

## What the original artifact is

A Jupyter notebook that trains a reinforcement learning agent to navigate an 8×8 maze and find treasure. Uses deep Q-learning built on Keras with experience replay. Starter code provided the environment (`TreasureMaze.py`) and the replay buffer (`GameExperience.py`); I wrote the Q-training loop.

## Why I chose it

Deep Q-learning is a cool hammer, but it's not always the right tool. For a deterministic shortest-path problem on a small grid, a classical search algorithm will crush it on every metric that matters. I wanted the artifact to actually make that comparison instead of just showing off one technique.

## What I enhanced

Added **A\*** and **breadth-first search** alongside the existing Q-learning agent, then benchmarked all three on the same maze.

- Implemented A\* with a Manhattan distance heuristic and a priority queue
- Implemented BFS for comparison (optimal for unweighted grids, no heuristic)
- Both algorithms work directly on the existing numpy maze — kept it simple, no graph classes, no adjacency lists
- Added benchmarking cells that measure path length, nodes explored, and wall-clock time
- Fixed several bugs in the original notebook along the way: `model.evaluate()` → `model.fit()` (the model wasn't actually learning), `while True` loops replaced with bounded `for _ in range(max_steps)` (prevented hangs), loop detection added so the agent doesn't bounce between two cells, and deprecated `keras` imports updated to `tensorflow.keras`

## What the comparison actually showed

| Algorithm | Path length | Nodes explored | Wall-clock |
|---|---|---|---|
| A\* | 24 steps (optimal) | ~50 | ~0.06 ms |
| BFS | 24 steps (optimal) | ~60 | ~0.05 ms |
| Deep Q-learning | inconsistent (~40% win rate) | — | ~1.4 hours to train |

A\* and BFS both hit the optimal path in under a millisecond. Q-learning needed over an hour of training to reach a ~40% win rate on the same maze. That's the whole point of the enhancement — showing that for a deterministic, fully-observable problem with a small state space, reinforcement learning is massive overkill. The interesting question isn't "which one wins," it's "which one is the right tool when the problem changes" (stochastic environments, unknown dynamics, huge state spaces — that's where RL earns its keep).

## Course outcomes this hits

- **Outcome 3 (algorithmic principles, trade-offs):** three algorithms, one problem, measured comparison — the whole artifact is about trade-offs
- **Outcome 4 (well-founded, innovative techniques):** combining classical search with modern reinforcement learning in one notebook, with real benchmarks

## Files

- `README.md` — this narrative
- `Collins_Daniel_ProjectTwo.ipynb` — original notebook
- `CS499_Milestone_Three_Daniel_Collins.zip` — full milestone submission with enhanced notebook + `TreasureMaze.py` + `GameExperience.py`, plus an `original/` folder

## How to run it

Open the enhanced notebook in Jupyter. A\* and BFS cells run instantly. The Q-learning training cell takes a while (hours) — if you just want to see results, the training output and benchmark tables are saved in the notebook.

---

Part of my CS 499 ePortfolio — [dcollins123.github.io](https://dcollins123.github.io)
