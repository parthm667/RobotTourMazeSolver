# Robout Tour Maze Solver

This is a pathfinding simulation I developed **for fun** during the 2024 Science Olympiad season while preparing for the **Robot Tour** event. Although I never used this in actual competition, it started as a side experiment to see how far I could push **A\*** search with direction tracking, gate sequencing, and wall collisions — kind of like turning a maze into a logic-based strategy game.

---

## What It Does

Given a maze with walls and labeled **gates** (A–F), the algorithm finds the **optimal path** that:

- Starts at a defined cell with a heading (north, east, south, west)
- Visits **all gates in any order**, except one gate which must be visited **last**
- Avoids walls and maze boundaries
- Accounts for **turning costs** and **movement costs**
- Disallows backward movement
- Ends at a specific destination

The movement is encoded as a series of actions:  
**S** = Start, **L**/**R** = Turn, **F** = Forward, **U** = U-turn, **E** = Final move into goal

---

## Gameplay Feel

The algorithm feels a bit like a puzzle game where:
- You control a robot that can only go forward, left, right, or U-turn
- Every action has a cost (e.g., turning slows you down)
- You need to **strategically plan** how to hit all gates with the shortest total time
- It keeps track of your **heading** at each step
- **Gates only count as visited when you *leave* them**, not just land on them

---

## Sample Output

```
Actions:
S L F R F F L F F R F F R F R F E

Total forward movements: 12
Total turns (incl. U-turns): 6
Total moves (movements + turns): 19
Order of gates visited: ('F', 'A', 'C', 'B', 'E', 'D')
Path verification: Valid
Total time needed: 18.56 seconds
```

---

## Maze Design

The maze is a 6×7 grid (modifiable) with:
- Walls placed on edges (bi-directional)
- Labeled gates like this:  
  - `'A': (3, 1)`  
  - `'D': (1, 2)`  
  - `'F': (4, 3)`  
  *(see code for full list)*

You can change the maze in `create_maze()`:
- Update gate positions
- Add/remove wall barriers
- Set a new start, end, or last gate
- Even randomize if you want to gamify it

---

## Running the Code

### Requirements
- Python 3.9+
- No external libraries — just `heapq` and `typing`

### It will:
- Print the maze layout as an ASCII grid
- Print each move, direction, and gate interaction
- Show the full path and actions
- Verify that the path is valid
- Show total time and gate visit order

---

## How It Works

- Uses A\* search with custom `State` objects that track position, heading, gate status, and path
- Each action (turn, move) has a time cost
- Wall collisions are bidirectional and checked before each forward step
- A `verify_path()` function replays the path to make sure it actually works

---

## Why I Made This

While training for Robot Tour in SciOly 2024, I wanted to experiment with:
- Heuristic search
- Modeling direction and movement costs
- Logic for gates and conditional traversal
- Real-world robot constraints (no backward movement, discrete turns)

I never ended up using this in a real competition as it was against the rules.

---

## Ideas for Extensions

- Add a GUI to visualize pathfinding
- Make gates have colors, weights, or timed opening rules
- Turn into a turn-based game or maze challenge
- Add battery limits or randomized obstacles
- Train a model to learn the best gate orders

---

Enjoy!
