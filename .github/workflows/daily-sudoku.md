---
name: Daily Sudoku Puzzle
description: Generates a new sudoku puzzle every day and posts it as a GitHub issue labeled "sudoku"
on:
  schedule: daily
  workflow_dispatch:
permissions:
  issues: read
timeout-minutes: 10
checkout: false
safe-outputs:
  create-issue:
    labels: [sudoku]
    close-older-issues: false
    max: 1
tools:
  bash: true
---

Generate a unique sudoku puzzle for today and create a GitHub issue with it.

## Instructions

1. Generate a valid, fully solvable 9×9 sudoku puzzle using bash. Use a bash script to:
   - Create a solved sudoku grid using a backtracking algorithm
   - Remove approximately 45–51 cells to create a puzzle with a unique solution
   - Format the puzzle as a readable grid using Unicode box-drawing characters

2. Create a GitHub issue with:
   - **Title**: `🧩 Daily Sudoku – <weekday>, <Month> <Day>, <Year>` (e.g. `🧩 Daily Sudoku – Monday, March 24, 2025`)
   - **Body**: A nicely formatted sudoku grid where empty cells are shown as `·`, with instructions, and a spoiler-tagged solution at the bottom using a `<details>` block

### Issue body format

```
## Today's Sudoku Puzzle

Difficulty: Medium

Fill in the grid so every row, column, and 3×3 box contains the digits 1–9.

╔═══╤═══╤═══╦═══╤═══╤═══╦═══╤═══╤═══╗
║ 5 │ 3 │ · ║ · │ 7 │ · ║ · │ · │ · ║
║ 6 │ · │ · ║ 1 │ 9 │ 5 ║ · │ · │ · ║
║ · │ 9 │ 8 ║ · │ · │ · ║ · │ 6 │ · ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║ 8 │ · │ · ║ · │ 6 │ · ║ · │ · │ 3 ║
║ 4 │ · │ · ║ 8 │ · │ 3 ║ · │ · │ 1 ║
║ 7 │ · │ · ║ · │ 2 │ · ║ · │ · │ 6 ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║ · │ 6 │ · ║ · │ · │ · ║ 2 │ 8 │ · ║
║ · │ · │ · ║ 4 │ 1 │ 9 ║ · │ · │ 5 ║
║ · │ · │ · ║ · │ 8 │ · ║ · │ 7 │ 9 ║
╚═══╧═══╧═══╩═══╧═══╧═══╩═══╧═══╧═══╝

<details>
<summary>🔍 Reveal Solution</summary>

╔═══╤═══╤═══╦═══╤═══╤═══╦═══╤═══╤═══╗
║ 5 │ 3 │ 4 ║ 6 │ 7 │ 8 ║ 9 │ 1 │ 2 ║
...
╚═══╧═══╧═══╩═══╧═══╧═══╩═══╧═══╧═══╝

</details>
```

3. Output the issue using the safe output format.
