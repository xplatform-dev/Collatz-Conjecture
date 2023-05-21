I am accepting contributions in the form of revising and editing and will credit you as such.

# Collatz Conjecture

"Simple" math problem that hasn't been proven to be true. The conjecture states that for any positive integer, $n$, the branching function.

$$
C(n) = 
	\left\\{ 
		\begin{array}{lr}
			3 \cdot n + 1; & n \mod 2 = 1 \\
			\frac{n}{2}; & n \mod 2 = 0\\ 
		\end{array}
	\right\.
$$

This was my initial thought process on solving the problem. I explored other methods that are more commonly accepted for math proofs in the paper. Since losing my point of contact for having this reviewed and edited by math professors to brain cancer, I have put this project on pause until I find the time to work on it.

A lot of these patterns are easier for me to explain or show when using the binary representation of the number.

The first one is repeating $0101...0101$. If we put this number into the Collatz function, *C*, we get a number that is a power of 2 which will very quickly converge to 1. If we look at this pattern, we have a cycle length of 2, and we can use either $10_2$ or $01_2$. Now we can quickly declare that any repeating values that meet this specific cycle will converge to 1.

We dismiss the repeative cycle of $00_2$ as it's trivial. And as for the repeative cycle of $11_2$, we actually have a special formualt for that one. That is 

$$
\frac{2n - 1}{3} \neq 2^{m} - 1; m > 1
$$

The restriction that $m$ must be greater than 1 is because $2^1 - 1$ doesn't produce a pattern of $11$, but instead produces the other 2 introduced.

The next part of this pattern is to show that by combining any of these patterns you can generate any positive integer.

| binary string | hex value |
| ---- | - |
| '00' + '00' | 0 |
| 00 + 01 | 1 |
| 00 + 10 | 2 |
| 00 + 11 | 3 |
| 01 + 00 | 4 |
| 01 + 01 | 5 |
| 01 + 10 | 6 |
| 01 + 11 | 7 |
| 10 + 00 | 8 |
| 00 + 01 | 9 |
| 00 + 10 | A |
| 00 + 11 | B |
| 01 + 00 | C |
| 01 + 01 | D |
| 01 + 10 | E |
| 01 + 11 | F |
| 01 + 00 + 01 | 10 |

The meaning behind this equation $\frac{2n - 1}{3} \neq 2^{m} - 1; m \gt 1$ has meaning because when evaluating *C* with these patterns we find that we only increase our leading coefficent when we have a set of $11_2$

Let us consider a number, *n*, represented as $a + 4 + b$, where *b* represents the 2 least significant binary bits. If we want to represent any possible number as it traverses through *C*, we can introduce another variable *k* to represent the number of multiplication steps we take. Now, *n'* can be written as $k(a + 4) + b$. While *a*, *b*, and *n* are restricted to be integers, k is not, this allows for the overflow from the *plus 1*. 

For any case *b*, we have the following
| case | steps | divide steps | resulting case | resulting coeffient | points to |
| ------ | - | - | ------ | ----------------- | - |
| $00_2$ | 0 | 2 | $xx_2$ | $\frac{k}{4}$     | any |
| $01_2$ | 1 | 2 | $xx_2$ | $\frac{3k}{4}$    | any |
| $10_2$ | 0 | 1 | $x1_2$ | $\frac{k}{2}$     | $01_2$ or $11_2$ |
| $11_2$ | 1 | 1 | $x1_2$ | $\frac{3k}{2}$    | $10_2$ or itself!! |

Since the only resulting coeffient that is greater than 1 is with case $11_2$, we need to show that this cannot loop on itself. Thus the derived equation.

The next step was showing that *C* did not loop elsewhere. However, my initial thought process on this was so embarrassingly wrong, I won't be sharing it. Turns out, this was the easiest thing to prove with two contradictions.
