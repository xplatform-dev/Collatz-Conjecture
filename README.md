<!-- TODO @dfisheritp update all formula's to follow defined variables -->
<!-- TODO @dfisheritp remove repetitive references to $n$ -->
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

The other part of this problem is the looping. For the loop to be true, the solution $C(n) = C(n_{i+cx})$ must exists.

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

- Possible loop on itself, results in $\lim_{i\rightarrow\inf}v_i=0$.
- Possible breaks into cases $01$ and $11$ with $v_{i + 2} = \frac{v_{i}}{4}$.

## Important notes

This might be overstating the obvious, but I don't want things to be unclear.

$$
\begin{array}{l}
	b = 2 \\
	\lambda = 2^{b} \cdot \gamma \\
	C(C(\lambda_{i} + 00_{2})) = \gamma \\
\end{array}
$$

This is important because it allows the known $1, 2, 4$ loop to exists within the solution space.

# The basic $b = 1$

$$C(n) = C(2^{b} \cdot \gamma + \beta) = C(\lambda + \beta) = \lambda_{i+1} + \beta_{i+1}$$

| $\beta_{i}$ | $\lambda_{i+1}$ | $\beta_{i+1}$ | $\lambda_{i+1} < \lambda_{i}$ | Basic Idea |
| ----------- | --------------- | -------------- | ---------------------------- | ---------- |
| $0_{2}$ | $\lambda_{i+1} = \frac{\lambda_{i}}{2}$ | $\beta$ | TRUE | TRUE |
| $1_{2}$ | $\lambda_{i+1} = 3\cdot\lambda$ | $0_{2}$ | FALSE | FALSE |

Explore $\left\\{01_{2}, 11_{2} \right\\}$ further.

----

### Case $\beta_{i} = 01_{2}$

$$
\begin{array}{l}
	C(\lambda_{i} + 01_{2}) = 3\cdot\lambda_{i} + 00_{2} \\
	C^{3}(\lambda_{i} + 01_{2}) = C^{2}(3\cdot\lambda_{i} + 00_{2}) = C^{2}(\lambda_{i+1} + 00_{2}) \\
	C^{3}(\lambda_{i}) = \frac{3\cdot\lambda_{i}}{4} + \beta \\
	\\
	\lambda_{i+3x} < \lambda_{i} \\
\\end{array}
$$

### Case $\beta_{i} = 11_2$

$$
C(n) = C(\lambda + 11_{2}) = 3\cdot\lambda_{i} + 10_{2} \rightarrow C(n_{i+1}) = \frac{3\cdot\lambda_{i}}{2} +
	\left\\{
		\begin{array}{l}
			01_{2} \Rightarrow C^{3}(C^{2}(n)) = C^{5}(n_{i}) = \lambda_{i+5} + \beta \rightarrow \lambda_{i+5} = \frac{9\cdot\lambda}{8} \\
			11_{2} \rightarrow \lambda = \frac{9\cdot\lambda}{4} \\
		\end{array}
	\right\.
$$

<!-- STARTHERE @dfisheritp -->

----
Expanding $11_{2} = \left\\{\begin{array}{l} 0011_{2}, \\ 0111_{2}, \\ 1011_{2}, \\ 1111_{2} \\ \end{array}\right\\}$

### Case $\beta_{i} = 0011_2$

$$
\begin{array}{l}
	C(n) = C(\lambda + 0011_{2}) = \lambda_{i + 1} + 1010_{2} \\
	\lambda_{i + 1} = 3\cdot\lambda_{i} \\
	C(n_{i + 1}) = 
		\left\\{
			\begin{array}{l}
				\lambda_{i + 2} + 0101_{2} = \frac{3\cdot\lambda}{2} + 0101_{2} \\
				\lambda_{i + 2} + 1101_{2} = \frac{3\cdot\lambda}{2} + 1101_{2} \\
			\end{array}
		\right\.
	\\
	0101_{2} \rightarrow C(\lambda_{i + 2}) = \lambda_{i + 3} + 0000_{2} = \frac{9\cdot\lambda_{i}}{2} + 0000_{2} \rightarrow C^{4}(\lambda_{i + 3}) = \frac{9\cdot\lambda}{32} + \beta \\
	1101_{2} \rightarrow C(n_{i + 2}) = \lambda_{i + 3} + 1000_{2} = \frac{9\cdot\lambda_{i}}{4} + 1000_{2} \rightarrow C^{3}(\lambda_{i + 4}) = \frac{9\cdot\lambda}{16} + \beta \\
\end{array}
$$

### Case $\beta_{i} = 0111_2$

$$
\begin{array}{l}
	C(n) = C(\lambda + 0111_{2}) = \lambda_{i + 1} + 0110_{2} \\
	C(n_{i+1}) = 
		\left\\{
			\begin{array}{l}
				C(\lambda_{i + 1} + 0011_{2}) \\
				C(\lambda_{i + 1} + 1011_{2}) \\
			\end{array}
		\right\\}
	\\
	0011_{2} \rightarrow 3 \cdot\text{ Case } 0011_{2} =
		\left\\{
			\begin{array}{l}
				\frac{27\cdot\lambda_{i}}{16} \\
				\frac{27\cdot\lambda_{i}}{32} \\
			\end{array}
		\right\\}
	\\
\end{array}
$$

<!-- TODO @dfisheritp explore the MOD 16, {3, 10, 13, 8, 12, 14, 7, 4, 10} -->

