To solve the **N-Queens problem**, we aim to place N queens on an N×N chessboard such that no two queens threaten each other (i.e., no two share the same row, column, or diagonal).
- It is a classical algorithm solved using *backtracking*

> Backtracking is a technique of solving problems one step at a time. if no solution is present for a given situation, we go to the previous/precursor of the situation and try out all the solutions there. We either find solutions or we find no solution]
> It is a type of exhaustive search/brute force

## Steps
1. **Row-wise Placement**: Start from the first row and place one queen per row.
2. **Conflict Check**: For each position in the current row, verify if placing a queen is safe:
    - **Column Check**: No queen in the same column.
    - **Diagonal Check**: No queen in the upper-left or upper-right diagonals.
3. **Recursion**: If safe, place the queen and recursively attempt to place queens in subsequent rows.
4. **Backtrack**: If no valid position exists in a row, backtrack to the previous row and adjust the queen’s position.

```al
pos[n]

FUNC nQueens(row, n)
//INPUT: row is row of current queen, and n is no of rows/cols
//OUTPUT: all possible configs
	IF (k == n)
		PRINT solution
		RETURN
	FOR (col<n; col: 0->n)
		IF (isSafe(row, col))
			pos[row] = col
			nqueen(row+1)
		END-IF
	END-FOR
RETURN

FUNC isSafe(row, col)
//INPUT: checking for queen at row,col
//OUTPUT: whether it is safe or not
	FOR(r<row; r:0->row)
		c = pos[r]
		IF (c == col OR abs(col - c) == abs(row - r))
			RETURN 0
		END-IF
	END-FOR
RETURN 1

>> Call nQueens(row:0 -> n, n)
```
## Time complexity
Worst case : $O(n!)$
- Can be optimised with pruning techniques to avoid repeated checks, but it does not get better than exponential growth

## Algorithm
- The loop goes through all previously placed queens (`i = 1` to `p - 1`).
- For each previous queen:
    1. **Same column check:**  
        `x[i] == x[p]`  
        If any previous queen is in the same column as the current queen, it's not safe.
    2. **Same diagonal check:**  
        `abs(x[i] - x[p]) == abs(i - p)` If the difference in columns is equal to the difference in rows, they're on the same diagonal (either `/` or `\` direction), which is not allowed.
- If either situation is true, the function returns `0` (**not safe to place**).
- If the loop finishes without finding a conflict, it returns `1` (**safe to place**).

---
```c
#include <stdio.h>
#include <math.h>
#include <stdlib.h>

#define MAX_N 20

int n, solution_count = 0;
int pos[MAX_N]; // pos[i] = stores col no of queen in ith row

// Check if it's safe to place a queen at (row, col)
int isSafe(int row, int col) {
    for (int r = 0; r < row; i++) {
        int c = pos[r];
        if (c == col || abs(col - c) == abs(row - r))
            return 0;
    }
    return 1;
}

void printSoln(){
	 // Found a solution, print it
        printf("Solution %d:\n", ++solution_count);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (pos[i] == j)
                    printf("Q ");
                else
                    printf("* ");
            }
            printf("\n");
        }
        printf("\n");
        
}

// Recursive function to solve N-Queens
void nqueen(int row) {
    if (row == n) {
       printSoln();
       return;
    }
    // Try placing queen in each column
    for (int c = 0; c < n; c++) {
        if (isSafe(row, c)) {
            pos[row] = c; // Place queen
            nqueen(row + 1); // Recurse to next row
            // No need to 'remove' queen, as col[row] will be overwritten
        }
    }
}

int main() {
    printf("Enter the number of queens: ");
    scanf("%d", &n);
    if (n < 1 || n > MAX_N) {
        printf("Please enter n between 1 and %d\n", MAX_N);
        return 1;
    }
    solve(0);
    if (solution_count == 0)
        printf("No solution!\n");
    else
        printf("Total solutions: %d\n", solution_count);
    return 0;
}
```