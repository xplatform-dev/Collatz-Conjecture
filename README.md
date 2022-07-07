<!-- TODO @dfisheritp update all formula's to follow defined variables -->
<!-- TODO @dfisheritp remove repetitive references to $n$ -->

[^top]
[^top]: top
# Collatz Conjecture

"Simple" math problem that hasn't been proven to be true. The conjecture states that for any positive integer, $n$, the branching function 

$$
C(n) = 
	\left\\{ 
		\begin{array}{lr}
			3 \cdot n + 1; & n \mod 2 = 1 \\
			\frac{n}{2}; & n \mod 2 = 0\\ 
		\end{array}
	\right\.
$$

will converge at the a repeating series of $1, 2, 4$. Such that no other repeating series exists and the function does not escape off to infinity.

## Defining variables

| variable | description | value range |
| -------- | ----------- | ----------- |
| C | Collatz function | N/A |
| n | value fed into C | $\mathbb{Z}^{+}$ |
| $\gamma$ | most significant bits | $\mathbb{Z}^{+}$ |
| $\alpha$ | buffer to allow known ranges of $\beta \text{, } 2^{b}$ | $\mathbb{Z}^{+}$ |
| $b$ | the number of bits of least significance | $\mathbb{Z}^{+}$ |
| $\beta$ | least significant bits | $0 \leq \beta < 2^{b}$ |
| $\lambda$ | the function to represent $\gamma$ | $\alpha \cdot \gamma \text{ or } 2^{b} \cdot \gamma$ |

### The substitution of $n$

$$
\begin{array}{l}
	n = \gamma \cdot 2^{b} + \beta \\
	n = \gamma \cdot \alpha + \beta \\
	n = \lambda + \beta
\end{array}
$$

### Restated problem

$$
C(n) = C(\lambda + \beta) = 
	\left\\{
		\begin{array}{lr}
			3 \cdot (\lambda + \beta) + 1 & n \mod 1 \equiv 1 \\
			\frac{\lambda + \beta}{2} & n \mod 1 \equiv 0 \\
		\end{array}
	\right\.
$$

### Basic idea

Show that $\lambda$ 
approaches 0 after an infinite number of runs through the function $C$, 
and to solve for all other cases of $\beta$

$$\lim_{i\rightarrow\inf}{C(\lambda_{i} + \beta)} = 0$$

<!-- TODO dfisheritp show loop condition goals -->

The other part of this problem is the looping. For the loop to be true, 

$$C(n) = C(n_{i+cx})$$

must exists.

Any reference to the function of $C$ 
with anything that is not the true and current value of $n$,
such as $C(\beta)$ is me being lazy. It all means the same thing.


# The First Truth

I'm lazy.
To reduce the amount of repeated work that would cause this document to become muddied with noise,
any work that has an established pattern to it will be left alone and a reference will be made to it.
If a case loops on itself, the work will also stop. There will be many of these.

## Completed work

A branch is complete if it can be shown for all that 
- has a $\lambda$ that statisies the [basic idea](#basic-idea).
- has all $\beta$ paths explored.

If the $\lambda$ does not meet the basic idea,
then the branch paths in a future section will be explored

## Looping on itself

There is one unique case that will be explored fully throughout this document that a loop will continuously grow.
That continuous loop is debunked [here](#<!-- TODO dfisher add #header-name-here -->). 

The first loop on itself is $\beta_{i} = 0_{2} \rightarrow \beta_{i+1} = 0_{2}$.
This meets the first bullet of the completed work. The branching paths from $\beta_{i+1} = 1_{2}$ needs to be explored

## Repeated or Established Patterns

When $\beta = 10_{2}$ there's a unique repeat where the next bit of significance can either be a 1 or a 0.
In the case of a 1, what we actually see is $\beta_{i+1} = 11_{2}$.
Thus, rather than looking at the case of $\beta = 10_{2}$, 
we could instead just look at the case of $11_{2}$

Similarly, if we see a case of $\beta = 0110_{2}$, this can either be 
$\beta_{i+1} = \left\\{3, 11\right\\}$. And by this point 3 will have already been explored, and 11 is coming up.

# The basic $b = 1$

<!-- STARTHERE @dfisheritp -->

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

### Expanding Case $11_2 \text{'s } \frac{9 \cdot v}{8}$ branch <!-- FIXME @dfisheritp -->

$$
\begin{array}{lrr}
	n_{i} = 2^{a} \cdot {x_{i}}^{y_{i}} + b_2; & a = 4; & 0 \leq b < 2^{a} \\
	u = 2^{4} \cdot x^{y} \\
\end{array}
$$

$$
\begin{array}{lc}
	\text{case } n_{i} = u_{i} + 0011_{2} & 3   \\
	\text{case } n_{i} = u_{i} + 0111_{2} & 7   \\
	\text{case } n_{i} = u_{i} + 1011_{2} & 11  \\
	\text{case } n_{i} = u_{i} + 1111_{2} & 15  \\
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
