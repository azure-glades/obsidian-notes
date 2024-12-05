For 2,3 and 4 variables
5+ variables : QM method

K maps use Greycodes
### Overview
Karnaugh Maps (K-Maps) are a graphical method for simplifying Boolean expressions. They reduce complex expressions to simpler forms, which can help in digital circuit design. A K-Map is a grid where each cell represents a possible input combination for the Boolean expression, and the cells are arranged so that only one variable changes between adjacent cells.

### Steps to Simplify Using K-Maps

1. **Draw the K-Map Grid**:
   - For 2 variables, use a 2x2 grid.
   - For 3 variables, use a 2x4 grid.
   - For 4 variables, use a 4x4 grid.
   
   The variables are labeled so that only one bit changes between adjacent cells (Gray code).

2. **Fill the K-Map with Values**:
   - Based on the given Boolean function, mark each cell with either a 1 (if the function is true for that input) or a 0 (if false).
   - Alternatively, the problem may provide a truth table that you can use to fill in the values.

3. **Identify and Circle Groups**:
   - Find groups of 1s in the K-Map. Groups should be of sizes that are powers of 2 (1, 2, 4, 8, etc.).
   - Circle the largest possible groups (overlapping is allowed), and make sure each 1 is in at least one group.
   - Group sizes and placements:
     - Each group should be as large as possible.
     - Groups can "wrap" around the edges of the K-Map.

4. **Write the Simplified Expression**:
   - For each group, write down the product term (ANDed term) by identifying the common variables that are constant within the group.
   - Combine all the product terms with OR operators.
   
#### 2-Variable K-Map

| A \ B | 0 B' | 1 B |
| ----- | ---- | --- |
| 0 A'  | 0    | 1   |
| 1 A   | 2    | 3   |
#### 3-Variable K-Map

| A \\ BC | 00 (A'B') | 01 (A'B) | 11 (AB) | 10 (AB') |
| ------- | --------- | -------- | ------- | -------- |
| 0 (A')  | 0         | 1        | 3       | 2        |
| 1 (B)   | 4         | 5        | 7       | 6        |

#### 4-Variable K-Map

| AB \ CD | 00  | 01  | 11  | 10  |
| ------- | --- | --- | --- | --- |
| 00      | 1   | 1   | 1   | 1   |
| 01      | 1   | 1   | 0   | 0   |
| 11      | 0   | 1   | 0   | 0   |
| 10      | 1   | 0   | 0   | 0   |

**Simplification**:
   - Find groups: Circle groups of 1s.
   - Resulting simplified terms combine into a minimal Boolean expression.

> [!tip]
> - Always group the largest possible groups of 1s.
> - Wrap around edges to create larger groups.
> - Don’t include unnecessary variables in the simplified terms.



