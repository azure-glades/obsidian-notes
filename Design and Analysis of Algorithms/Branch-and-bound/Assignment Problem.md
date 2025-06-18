#exhaustive-search #NP-hard 
***To assign `n` jobs to `n` people such that the total cost of assignment is as low as possible***

Steps:
1. Calculate lower bound : Sum of lowest cost values of each job
2. Take person 1, successively assign each job and calculate possible lower bound (remember that the assigned job cannot be given to others, but when calculating unassigned lower bounds its fine)
3. Choose the best solution and then assign remaining jobs successively

[Girish Rao Salanke - Assignment Problem](https://www.youtube.com/watch?v=ptwqAyvf63Q&list=PLtg1mdkLERgnS8XNGU4irXk7dRuji61ZX&index=54)

*Hungarian Method* is a solution to the assignment problem
