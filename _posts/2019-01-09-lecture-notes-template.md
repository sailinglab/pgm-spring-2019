# Undirected Graphical Models
### High-Level Properties
* There can only be symmetric relationships between a pair of nodes (random variables). In other words, there is no causal effect from one random variable to another.
* The model can represent properties and configurations of a distribution, but it cannot generate samples explicitly.
* Each node has strong correlations with its neighbors.
##### Example
Img1

Let each node represents an image patch. It is impossible to tell what is inside this image patch by isolating it from others. However, when we look at its neighboring image patches, we can see that it’s an image patch of water. Due to the fact that the relationships between neighboring image patches should be symmetric, an image is best represented by an undirected graphical model. This particular undirected graphical model is also known as the grid model.

### Quantitative Specification
#### Cliques
* Cliques are subgraphs that are fully connected.
* A maximal clique is a clique such that any superset (any bigger subgraph that contains this subgraph) is not complete.
* A sub-clique is a not-necessarily-maximal clique.
##### Example
Img2.1
Img2.2
Img2.3

#### Potential Functions
Each clique can be associated with a potential function. The potential function can be understood as a provisional function of its arguments by assigning a pre-probabilistic score of their joint distribution. This potential function can be somewhat arbitrary.

Why cliques? Each component of the clique contributes to the overall potential function.
##### Example
Img3.1
For $$\psi_c(X_1, X_2)$$
Img3.2

In general, potential functions have to be positive non-zero.

Potential functions are not necessarily probabilistic:
Img4
This model implies that '$X \perp Y | Z$' So this graph factorizes as:
<d-math block>
\begin{aligned}
    p(x,y,z)&=p(y)p(x|y)p(z|y) \\
    &=p(x,y)p(z|y) \\
    &=p(x|y)p(y,z)
\end{aligned}
</d-math>

