# Collatz Conjecture

"Simple" math problem that hasn't been proven to be true. The conjecture states that for any positive integer, $n$, the branching function 

$$
C(n) = 
  \left\\{ 
    \begin{array}{lr}
      3 \cdot n + 1; & n \mod 2 = 1 \\
      \frac{n}{2}; & n \mod 2 = 1\\ 
    \end{array}
  \right\.
$$

will converge at the a repeating series of $1, 2, 4$. Such that no other repeating series exists and the function does not escape off to infinity.

## Loop requirements

$$C(n) = C(n_{i+cx})$$

## A substitution of $n$

$$
\begin{array}{l}
  n = x^{y} \cdot 4 + b_{2} \Leftrightarrow x_2^{y + 2} + b_{2} \\
  n_{i} = x_i^{y_i} \cdot 4 + b_{2i} \\
  v = x^{y + 2} \\
  v_{i} = x_i^{y_i + 2} \\
\end{array}
$$

$$
\begin{array}{l}
  n_i = v_i + 00_2 \\
  n_i = v_i + 01_2 \\
  n_i = v_i + 10_2 \\
  n_i = v_i + 11_2 \\
\end{array}
$$

## Pattern Building

### Case $00_2$

Branches of $n_{i} = v_{i} + 00_2$: 

$$
C(n_{i}) = \frac{v}{2} + 
  \left\\{
    \begin{array}{l}
      00_2 \\
      10_2 
        \left\\{
          \begin{array}{l}
            C(n_{i + 1} = \frac{v_{i}}{4} + 01_2 \\
            C(n_{i + 1} = \frac{v_{i}}{4} + 11_2 \\
          \end{array}
        \right\.
      \\
    \end{array}
  \right\.
$$

Overstating the obvious here, but

$$
C(C(x^{y + 2})) \Rightarrow \frac{v_{i}}{4} = x^{y}
$$

- Possible loop on itself, results in $\lim_{i\rightarrow\inf}v_i=0$.
- Possible breaks into cases $01$ and $11$ with $v_{i + 2} = \frac{v_{i}}{4}$.

----

### Case $01_2$

