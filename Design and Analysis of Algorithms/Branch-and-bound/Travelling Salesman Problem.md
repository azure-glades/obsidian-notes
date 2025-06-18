#exhaustive-search #NP-hard
***To find the shortest tour through a given set of `n` cities that visits each city exactly once before returning to the city where it started.***
- Such a path is called a *Hamiltonian Circuit*

Steps:
1. Calculate lower bound $$\text{LB} = \lceil \frac{S}{2} \rceil$$
	- Where S is the sum of 2 shortest roads from each city
2. Branch to all other cities, and calculate lower bound again, now including the path/branch used (so, if AB is a branch, then the distance AB has to be included when making lower bound (done by replacing A and B distances with an AB distance))
3. Choose the lowest bound and continue until that path is exhausted
4. Next, discard all lower bounds that are higher than the exhausted path.
5. If any lower bounds exist that are lower than the exhausted path, back-track to them and then branch from those cities again
6. Continue this until the route with the lowest distance is found
[Girish Rao Salanke Travelling Salesman](https://www.youtube.com/watch?v=d1N6-15a_j4&list=PLtg1mdkLERgnS8XNGU4irXk7dRuji61ZX&index=56)

Time complexity : O(n!)
