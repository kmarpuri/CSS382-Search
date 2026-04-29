# Pacman Search

Implementation of classic search algorithms for UC Berkeley's Pacman AI project, completed for **CSS 382 – Artificial Intelligence** at the University of Washington Bothell.

## Overview

This project applies graph-search algorithms to navigate Pacman through various maze environments. The work spans eight questions covering uninformed search, informed search, problem modeling, and heuristic design.

## Algorithms Implemented

| # | Question | Algorithm / Topic | File |
|---|----------|-------------------|------|
| 1 | Depth First Search | Stack-based graph-search DFS | `search.py` |
| 2 | Breadth First Search | Queue-based graph-search BFS | `search.py` |
| 3 | Uniform Cost Search | Priority-queue search by path cost | `search.py` |
| 4 | A\* Search | Priority-queue search with `f(n) = g(n) + h(n)` | `search.py` |
| 5 | Corners Problem | State-space modeling for visiting all four corners | `searchAgents.py` |
| 6 | Corners Heuristic | Admissible greedy nearest-corner heuristic | `searchAgents.py` |
| 7 | Food Search Heuristic | Max maze-distance heuristic with caching | `searchAgents.py` |
| 8 | Suboptimal Search | BFS-based closest-dot search | `searchAgents.py` |

## Project Structure

```
CSS382-Search/
├── search.py              # Search algorithm implementations (DFS, BFS, UCS, A*)
├── searchAgents.py        # Search problem definitions and heuristics
├── pacman.py              # Main Pacman game engine
├── game.py                # Game state and supporting types
├── util.py                # Data structures (Stack, Queue, PriorityQueue, etc.)
├── autograder.py          # Project autograder
├── autograde.txt          # Autograder output (26/25)
├── commands.txt           # Example Pacman commands
├── Answers.md             # Detailed written answers for each question
├── eightpuzzle.py         # Eight-puzzle demo for UCS
├── graphicsDisplay.py     # Pacman graphics renderer
├── graphicsUtils.py       # Graphics utility functions
├── textDisplay.py         # Text-based display
├── ghostAgents.py         # Ghost behavior agents
├── keyboardAgents.py      # Human-controlled Pacman agent
├── pacmanAgents.py        # Simple Pacman agents
├── layout.py              # Maze layout parser
├── layouts/               # Maze layout files
├── test_cases/            # Autograder test cases
└── VERSION                # Project version file
```

## Getting Started

### Prerequisites

- Python 3.x

### Running Pacman

```bash
# Default game
python pacman.py

# DFS on medium maze
python pacman.py -l mediumMaze -p SearchAgent

# BFS on big maze
python pacman.py -l bigMaze -p SearchAgent -a fn=bfs -z .5

# UCS with cost functions
python pacman.py -l mediumDottedMaze -p StayEastSearchAgent
python pacman.py -l mediumScaryMaze -p StayWestSearchAgent

# A* with Manhattan heuristic
python pacman.py -l bigMaze -z .5 -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic

# Corners problem with BFS
python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs,prob=CornersProblem

# Corners problem with A* and custom heuristic
python pacman.py -l mediumCorners -p AStarCornersAgent -z 0.5

# Food search with A* and custom heuristic
python pacman.py -l trickySearch -p AStarFoodSearchAgent

# Closest dot search
python pacman.py -l bigSearch -p ClosestDotSearchAgent -z .5
```

### Running the Autograder

```bash
python autograder.py
```

## Results

All eight questions pass with **26/25** (extra credit on Q7):

| Question | Score | Notes |
|----------|-------|-------|
| Q1 – DFS | 3/3 | |
| Q2 – BFS | 3/3 | |
| Q3 – UCS | 3/3 | |
| Q4 – A\* | 3/3 | 221 nodes expanded on `mediumMaze` |
| Q5 – Corners Problem | 3/3 | |
| Q6 – Corners Heuristic | 3/3 | 901 nodes expanded (threshold: 1200) |
| Q7 – Food Heuristic | **5/4** | 4137 nodes expanded (extra credit threshold: 7000) |
| Q8 – Closest Dot | 3/3 | |
| **Total** | **26/25** | |

## Acknowledgments

The Pacman AI projects were developed at [UC Berkeley](http://ai.berkeley.edu). The core projects and autograders were primarily created by John DeNero and Dan Klein. Student-side autograding was added by Brad Miller, Nick Hay, and Pieter Abbeel.