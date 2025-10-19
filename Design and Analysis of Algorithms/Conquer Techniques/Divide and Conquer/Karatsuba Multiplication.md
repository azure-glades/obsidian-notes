The commonly used multiplication algorithm for integers is the grade-school multiplication commonly known which is $O(n^2)$ 
Anatoly Karatsuba discovered another algorithm using #divide-and-conquer that takes $\Theta(n^{\log_2 3}) \approx \Theta(n^{1.58})$ which makes it asymptotically faster than the conventional method. However it is only faster for large numbers.
- More algorithms were made as modifications of this, like [Toom-Cook Algorithm](https://en.wikipedia.org/wiki/Toom%E2%80%93Cook_multiplication) and [Schonhage-Strassen Algorithm](https://en.wikipedia.org/wiki/Sch%C3%B6nhage%E2%80%93Strassen_algorithm)
$$T(n) = 3*T(n/2)+cn+d$$
```al
function karatsuba(num1, num2)
    if (num1 < 10 or num2 < 10)
        return num1 × num2 /* fall back to traditional multiplication */
    
    /* Calculates the size of the numbers. */
    m = max(size_base10(num1), size_base10(num2))
    m2 = floor(m / 2) 
    /* m2 = ceil (m / 2) will also work */
    
    /* Split the digit sequences in the middle. */
    high1, low1 = split_at(num1, m2)
    high2, low2 = split_at(num2, m2)
    
    /* 3 recursive calls made to numbers approximately half the size. */
    z0 = karatsuba(low1, low2)
    z1 = karatsuba(low1 + high1, low2 + high2)
    z2 = karatsuba(high1, high2)
    
    return (z2 × 10 ^ (m2 × 2)) + ((z1 - z2 - z0) × 10 ^ m2) + z0
```

