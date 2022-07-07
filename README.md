[^top]
[^top]: top
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

<!-- TODO @dfisheritp -->

## Loop requirements

$$C(n) = C(n_{i+cx})$$

## A substitution of $n$

$$
\begin{array}{l}
  n = x^{y} \cdot 4 + b_{2} \Leftrightarrow x_2^{y} \cdot 4 + b; 0 \leq b \leq 3 \\
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
<br>
Either we have Case $01_2$ next or we have Case $11_2$[^1] next.
[^1]: This is the growth loop.

----

### Case $11_2$

$$3_{2}$$

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
It did not make sense to do this for the other cases above since the value of $v$ was already less than $1$

### Expanding Case $11_2$ s to  $\frac{9 \cdot v}{8}$ branch <!-- FIXME @dfisheritp -->

$$
\begin{array}{l}
  n_{i} = 2^{4} \cdot {x_{i}}^{y_{i}} + a_2; 0 \leq a \leq 15 \\
  u = 2^{4} \cdot x^{y} \\
\end{array}
$$

$$
\begin{array}{lc}
  \text{subcase } n_{i} = u_{i} + 0011_{2} & 3   \\
  \text{subcase } n_{i} = u_{i} + 0111_{2} & 7   \\
  \text{subcase } n_{i} = u_{i} + 1011_{2} & 11  \\
  \text{subcase } n_{i} = u_{i} + 1111_{2} & 15  \\
\end{array}
$$

$$
C(u_{i} + 3) = 3 \cdot u_{i} + 1010_2 \Rightarrow C(3 \cdot u_{i} + 1010_2) = \frac{3 \cdot u_{i}}{2} + 
  \left\\{
    \begin{array}{l}
      0101_2 \Rightarrow C(\frac{3 \cdot u_{i}}{2} + 0101_2) = \frac{9 \cdot u_{i}}{2} + 0000_2 \Rightarrow C(C(C(C(\frac{9 \cdot u_{i}}{2} + 0000_2)))) = \frac{9 \cdot u_{i}}{32} + a \\
      1101_2 \Rightarrow C(\frac{3 \cdot u_{i}}{2} + 1101_2) = \frac{9 \cdot u_{i}}{2} + 1000_2 \Rightarrow C(C(C(\frac{9 \cdot u_{i}}{2} + a))) = \frac{9 \cdot u_{i}}{16} + a \\
    \end{array}
  \right\.
$$
