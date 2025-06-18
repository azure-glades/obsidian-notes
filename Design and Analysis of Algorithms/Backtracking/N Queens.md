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
FUNC nQueens(k, n)
//INPUT: k is current queen, and n is no of queens
//OUTPUT: all possible configs
	FOR(i<n, i: 0 -> n)
		IF(place(k,i))
			
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
#include <stdlib.h>

int place(int p, int x[]) {
    int i;
    for (i = 1; i <= (p - 1); i++) {
        if ((x[i] == x[p]) || (abs(x[i] - x[p]) == abs(i - p)))
            return 0;
    }
    return 1;
}

int main() {
    int i, j, k, n, count = 1, x[1500], flag = 0;
    printf("Enter the number of queens: ");
    scanf("%d", &n);

    k = 1;
    x[k] = 0;    // x[1] column no, k is row number
    while (k) {
        x[k] = x[k] + 1;
        while (x[k] <= n && !place(k, x))
            x[k] = x[k] + 1;
        if (x[k] <= n) {
            if (k == n) { // nth queen
                printf("Solution %d\n", count++);
                flag = 1;
                for (i = 1; i <= n; i++) {
                    for (j = 1; j < x[i]; j++)
                        printf("* ");
                    printf("Q ");
                    for (j = x[i] + 1; j <= n; j++)
                        printf("* ");
                    printf("\n");
                }
            } else {
                k += 1;
                x[k] = 0;
            }
        } else {
            k = k - 1;
        }
    }
    if (flag == 0)
        printf("No solution!!\n");

    return 0;
}
```