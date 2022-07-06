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
  v = 4 \cdot x^{y} \\
  v_{i} = 4 \cdot x_i^{y_i} \\
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
\begin{array}{c}
v = 4 \cdot x^{y} \\
C(C(4 \cdot x^{y})) \Rightarrow \frac{v_{i}}{4} = x^{y} \\
\end{array}
$$

And it's important to overstate this obvious thing, because it allows the known $1, 2, 4$ loop to exists within the solution space.

- Possible loop on itself, results in $\lim_{i\rightarrow\inf}v_i=0$.
- Possible breaks into cases $01$ and $11$ with $v_{i + 2} = \frac{v_{i}}{4}$.

----

### Case $01_2$

$$\begin{array} 1 & 101 & 1001 & 1101 & 10101 & 11101 & \ldots \end{array}$$

Branches of $n_{i} = v_{i} + 01_2$:

$$
C(n_{i}) = 3 \cdot v + 00_2 \rightarrow C(n_{i+1}) = \frac{3 \cdot v}{2} + 
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

$$\begin{array}{c}\ldots110_2&\ldots010_2\\ \end{array}$$

I feel like I don't have to explain this one... as it's in Case $00_2$ and Case $01_2$.
Either we have Case $01_2$ next or we have Case $11_2$[^1] next.
[^1]: This is the growth loop.

----

### Case $11_2$

$${\text{☣️☣️}}_{2}$$

$$
C(n_{i}) = 3 \cdot v + 10_{2} \rightarrow C(n_{i+1}) = \frac{3 \cdot v}{2} +
  \left\\{
    \begin{array}{l}
      01_{2} \rightarrow v = \frac{9 \cdot v}{8} \\
      11_{2} \rightarrow v = \frac{9 \cdot v}{4} \\
    \end{array}
  \right\.
$$

Now, both of these introduced a $v > 1$.
Fortunately, the first one is handled the same way as cases $00_{2}, 01_{2}, 10_{2}$, it's $b$ value, the least significant bits, needs to be expanded a 'bit' further.
It did not make sense to do this for the other cases above.

____
### Expanding $v = \frac{9 \cdot v_i}{8}$

$$
\begin{array}{l}
  n_{i} = 2^{a} \cdot {x_{i}}^{y_{i}} + a_2 \\
  u = 2^{a} \cdot x^{y} \\
\end{array}
$$
