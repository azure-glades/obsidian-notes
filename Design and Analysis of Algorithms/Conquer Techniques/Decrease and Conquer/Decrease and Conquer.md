Similar to [[Divide and Conquer]], but instead of dividing the problem into 2 halves, we decrease the size of the instance (no splitting, there is only 1 instance
$$T(n) = T(n-k) + f(n)$$

> Example
> - [[Binary search]]
> - [[Tower of Hanoi]]
> - [[Insertion sort]]
> - [[Depth First Search]]
> - [[Breadth First Search]]

1. decrease by constant one/value: [[Insertion sort]],[[Depth First Search]],[[Breadth First Search]]
2. decrease by constant factor: [[Josephus Problem]], [[Fake coin problem]]
3. variable size decrease: [[Median of array]], [[LCM and GCD]]

decrease by constant
- calculate 2^n → T(n) = T(n-1) + 1
- insertion sort algorizz

