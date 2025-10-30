# Implement a Sudoku Solver From Scratch
## Steps to solve the Sudoku Puzzle in Python
<ol>
  <li>In this method for solving the sudoku puzzle, first, we assign the size of the 2D matrix to a variable M (M*M).</li>
 <li>Then we assign the utility function (puzzle) to print the grid.</li>
<li>Later it will assign num to the row and col.</li>
<li>If we find the same num in the same row or same column or in the specific 3*3 matrix, ‘false’ will be returned.</li>
<li>Then we will check if we have reached the 8th row and 9th column and return true for stopping further backtracking.</li>
<li>Next, we will check if the column value becomes 9 then we move to the next row and column.</li>
<li>Further now we see if the current position of the grid has a value greater than 0, then we iterate for the next column.</li>
<li>After checking if it is a safe place, we move to the next column and then assign the num in the current (row, col) position of the grid. Later we check for the next possibility with the next column.</li>
<li>As our assumption was wrong, we discard the assigned num and then we go for the next assumption with a different num value</li>
</ol>

## PROGRAM

```

Name : CHANDRAPRIYADHARSHINI C
Register number : 212223240019


# Size of the grid
M = 9

# Utility function to print the Sudoku grid
def print_grid(grid):
    for row in grid:
        print(row)

# Function to check whether it's safe to place a number
def is_safe(grid, row, col, num):
    # Check row
    for x in range(9):
        if grid[row][x] == num:
            return False

    # Check column
    for x in range(9):
        if grid[x][col] == num:
            return False

    # Check 3x3 subgrid
    start_row = row - row % 3
    start_col = col - col % 3
    for i in range(3):
        for j in range(3):
            if grid[i + start_row][j + start_col] == num:
                return False

    return True

# Main function to solve the Sudoku using backtracking
def solve_sudoku(grid, row=0, col=0):
    # If we reach the end, return True
    if row == M - 1 and col == M:
        return True

    # Move to the next row if column is 9
    if col == M:
        row += 1
        col = 0

    # Skip cells that already have a number
    if grid[row][col] > 0:
        return solve_sudoku(grid, row, col + 1)

    # Try placing numbers 1–9
    for num in range(1, 10):
        if is_safe(grid, row, col, num):
            grid[row][col] = num

            # Recurse to next cell
            if solve_sudoku(grid, row, col + 1):
                return True

        # Undo assignment (backtrack)
        grid[row][col] = 0

    return False

# Sudoku grid (0 = empty)
grid = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]

if solve_sudoku(grid):
    print("Sudoku grid solved successfully!!!")
    print_grid(grid)
else:
    print("No solution exists")

```

## Output :

<img width="401" height="231" alt="image" src="https://github.com/user-attachments/assets/b690606d-2697-481a-a98f-568e8c39dbbb" />


## Result:
Thus the python program to implement a sudoko solver from scratch is executed sucessfully.



