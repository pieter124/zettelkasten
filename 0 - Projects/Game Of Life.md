Tags: [[2 - Tags/project|project]] [[programming]]

# **Game Of Life**

Rules:
The universe of the Game of Life is an infinite, two-
dimensional orthogonal grid of square cells, each of which is in one of two possible states, live or dead. Every cell interacts with its eight neighbours, which are the cells that are horizontally, vertically, or diagonally adjacent. At each step in time, the following transitions occur:

1. Any live cell with fewer than two live neighbours dies, as if by under population.
2. Any live cell with two or three live neighbours lives on to the next generation.
3. Any live cell with two or three live neighbours lives on to the next generation.
4. Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

The initial pattern constitutes the seed of the system. The first generation is created by applying the above rules simultaneously to every cell in the seed, live or dead; births and deaths occur simultaneously, and the discrete moment at which this happens is sometimes called a tick. Each generation is a pure function of the preceding one. The rules continue to be applied repeatedly to create further generations.

# Objective(s):
Successfully create a working implementation of the game of life in C, displayed on the terminal.

# Subtopics / Milestones:
MVP Features:
- Display a grid
- Apply rules to one generation
- Fixed-grid size. 
- No fancy graphics.

Future Milestones:
- Having a working input being read by the user to exit the game and free the memory allocated.
- Use multi-threading to calculate next generation.
- Add colour.

# Resources:
*Wikipedia's*
**Conway's Game of Life:** https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life






