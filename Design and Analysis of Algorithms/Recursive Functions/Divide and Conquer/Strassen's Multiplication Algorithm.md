The brute force method for multiplying an `n x n` matrix is $O(n^3)$ which was thought to be the most efficient way for the longest period of time
Strassen found a #divide-and-conquer method of solving this in $O(n^{\log_2{7}}) \approx O(n^{2.81})$ time.
- This works out by performing less multiplication and more addition, since addition is faster. It’s time complexity is 
$$
T(n) = 7*T(n/2) + cn
$$
where $c \in \mathbb{R}$ 

Consider a 2x2 matrix $A$ and $B$
$$
A = \begin{bmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{bmatrix},
B = \begin{bmatrix}
B_{11} & B_{12} \\
B_{21} & B_{22}
\end{bmatrix}
$$
then
$$
\displaylines{
M_1 = A_{11}(B_{12}-B_{22}) \\
M_2 = B_{22}(A_{11}+A_{12}) \\
M_3 = B_{11}(A_{21}+A_{22}) \\
M_4 = A_{22}(B_{21}-B_{11}) \\
\\
M_5 = (A_{11}+A_{22})(B_{11}+B_{22}) \\
\\
M_6 = (A_{21}-A_{11})(B_{12}+B_{11}) \\
M_7 = (A_{22}-A_{12})(B_{21}+B_{22})
}
$$
Form the multiples
Now the product matrix $C$ is 
$$
C = \begin{bmatrix}
-M_2+M_4+M_5+M_7 & M_1+M_2 \\
M_3+M_4 & M_1-M_3+M_5+M_6
\end{bmatrix}
$$

Since the matrix is being cut into submatrices of size `n/2` and there are 7 operations done at each recursive call, the coefficient values arise hence in the complexity equation
