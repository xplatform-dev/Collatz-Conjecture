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

## Defining variables


## Loop requirements

$$C(n) = C(n_{i+cx})$$

## A substitution of $n$

$$
\begin{array}{l}
  n = x^{y} \cdot 4 + b_{2} \Leftrightarrow x_2^{y} \cdot 4 + b \\
  n_{i} = x_i^{y_i} \cdot 4 + b \\
  v = x^{y} \\
  v_{i} = x_i^{y_i} \\
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

$$1\ldots00_2$$

Branches of $n_{i} = v_{i} + 00_2$: 

$$
C(n_{i}) = \frac{v}{2} + 
  \left\\{
    \begin{array}{l}
      00_2 \\
      10_2 
        \left\\{
          \begin{array}{l}
            C(n_{i + 1}) = \frac{v_{i}}{4} + 01_2 \\
            C(n_{i + 1}) = \frac{v_{i}}{4} + 11_2 \\
          \end{array}
        \right\.
      \\
    \end{array}
  \right\.
$$

Overstating the obvious here, but

$$
C(C(x^{y} \cdot 4)) \Rightarrow \frac{v_{i}}{4} = x^{y}
$$

- Possible loop on itself, results in $\lim_{i\rightarrow\inf}v_i=0$.
- Possible breaks into cases $01$ and $11$ with $v_{i + 2} = \frac{v_{i}}{4}$.

----

### Case $01_2$

$$\begin{array} 1 & 101 & 1001 & 1101 & 10101 & 11101 & \ldots \end{array}$$

Branches of $n_{i} = v_{i} + 01_2$:

$$
C(n_{i} = 3 \cdot v + 00_2 \rightarrow C(n_{i+1}) = \frac{3 \cdot v}{2} + 
  \left\\{
    \begin{array}{l}
      00_{2} \rightarrow C(n_{i+3}) = \frac{3 \cdot v}{8} + b \\
      10_{2} \rightarrow C(n_{i+2}) = \frac{3 \cdot v}{4} + 
        \left\\{
          \begin{array}{1}
            01_{2} \\
            11_{2} \\
          \end{array}
        \right\. 
      \\
    \end{array}
  \right\.
$$

- Possible loop on case $01_2 \rightarrow$ case $00_2 \rightarrow$ case $10_2 \rightarrow$ case $01_2$. Resulting in $v \rightarrow {(\frac{3 \cdot v}{4})}^{j}$
- Resulting $v \rightarrow \frac{3 \cdot v}{4}$ on the outbound breaks.

Results for case $01_2$
$v_{i+3} < v_{i}$

----

### Case $10_2$
