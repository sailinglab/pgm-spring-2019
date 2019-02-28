---
layout: distill
title: Lecture 10
description: Kalman Filtering and Topic Models
date: 2019-02-20

lecturers:
  - name: Eric Xing
    url: "https://www.cs.cmu.edu/~epxing/"

authors:
  - name: Aakanksha Naik
    url: "#"  # optional URL to the author's homepage
  - name: Author 2
    url: "#"
  - name: Bingqing Chen
    url: "#"

editors:
  - name: Editor 1  # editor's full name
    url: "#"  # optional URL to the editor's homepage

abstract: >
  An example abstract block.
---
## Kalman Filtering 
Kalman filtering is a technique to perform efficient inference in the forward algorithm for state-space models. Consider the following state-space model:
<figure id="ssm-figure" class="l-body-outset">
  <div class="row">
    <div class="col one">
      <img src="{{ 'assets/img/lecture-11/ssm.png' | relative_url }}" />
    </div>
  </div>
  <figcaption>
    <strong>Figure 1: State Space Model</strong>
  </figcaption>
</figure>
As we can see, this model consists of a sequence of hidden states, with each hidden state emitting an observation. To perform inference efficiently on this model, we can define a recursive algorithm as follows:
1. Compute $ P(X_t \vert Y_{1...t}) $
2. Compute $ P(X_t+1 \vert Y_{1...t+1}) $ from the previous probability after adding the observation $ Y_{t+1} $

Kalman filtering provides a way of performing this recursion. It breaks the computation into two steps:
1. Predict Step: Compute $P(X_{t+1} \vert Y_{1...t})$ (prediction) from $ P(X_t \vert Y_{1...t}) $ (prior belief) and $P(X_{t+1} \vert X_t)$ (dynamical model)
2. Update Step: Compute $P(X_{t+1} \vert Y_{1...t+1})$ from $P(X_{t+1} \vert Y_{1...t})$ (prediction), $Y_{t+1}$ (observation) and $P(Y_{t+1} \vert X_{t+1})$ (observation model)

The predict and update steps are also called the time update and measurement update steps respectively.
We will now derive equations for both steps for our state-space model. Remember that all hidden states and observations in the model are drawn from Gaussian distributions since they are computed via linear transformations. This means that all conditional and marginal probabilites in the model are also Gaussian distributions.

### Predict Step Derivation
Remember that the dynamical model is defined as $X_{t+1} = AX_t + GW_t$, where $W_t \sim \mathcal{N}(0,Q)$
We can compute the mean and variance for this Gaussian distribution as follows:
<d-math block>
\begin{aligned}
\hat X_{t+1 \vert t} &= E(X_{t+1} \vert Y_1...Y_t) = E(AX_t + GW_t) = A\hat X_{t|t} \\
P_{t+1 \vert t} &= E((X_{t+1} - \hat X_{t+1 \vert t})(X_{t+1} - \hat X_{t+1 \vert t})^T \vert Y_1...Y_t) \\
&= E((AX_t + GW_t - \hat X_{t+1 \vert t})(AX_t + GW_t - \hat X_{t+1 \vert t})^T \vert Y_1...Y_t) \\
&= AP_{t \vert t}A + GQG^T
\end{aligned}
</d-math>

For the observation model, which is defined as $Y_{t} = CX_t + \nu_t$, where $\nu \sim \mathcal{N}(0,R)$, we can compute the mean and variance as follows:
<d-math block>
\begin{aligned}
E(Y_{t+1} \vert Y_1...Y_t ) &= E(CX_{t+1} + \nu_{t+1} \vert Y_1...Y_t ) = C\hat X_{t+1|t} \\
E((Y_{t+1} - \hat Y_{t+1 \vert t})(Y_{t+1} - \hat Y_{t+1 \vert t})^T \vert Y_1...Y_t) &= CP_{t+1|t}C^T + R\\
\end{aligned}
</d-math>

Finally, we can also derive the following:
$$ E((Y_{t+1} - \hat Y_{t+1 \vert t})(X_{t+1} - \hat X_{t+1 \vert t})^T \vert Y_1...Y_t) = CP_{t+1|t} $$

### Update Step Derivation
Recall that for two gaussian distributions $X_1, X_2$, their joint distribution is a Gaussian with the following mean and variance:
<d-math block>
\begin{aligned}
\mu &=
  \begin{bmatrix}
    \mu_1 \\
    \mu_2
  \end{bmatrix} \\
\sum &=
  \begin{bmatrix}
    \sum_{11} & \sum_{12} \\
    \sum_{21} & \sum_{22}
  \end{bmatrix}
\end{aligned}
</d-math>
Using this result in combination with the derivations from the predict step, we can deduce that $P(X_{t+1}, Y_{t+1} \vert Y_1...Y_t) \sim \mathcal{N}(M_{t+1}, V_{t+1})$, where
<d-math block>
\begin{aligned}
M_{t+1} &=
  \begin{bmatrix}
    \hat X_{t+1|t} \\
    C\hat X_{t+1|t}
  \end{bmatrix} \\
V_{t+1} &=
  \begin{bmatrix}
    P_{t+1|t} & P_{t+1|t}C^T \\
    CP_{t+1|t} & CP_{t+1|t}C^T + R
  \end{bmatrix}
\end{aligned}
</d-math>

Given a joint distribution of two Gaussian random variables $X_1, X_2$, recall that their conditional and marginal probability distributions are defined as follows:\\
$$ P(X_2) = \mathcal{N}(M_2^m, V_2^m) $$ \\
$$ M_2^m = \mu_2 $$ \\
$$ V_2^m = \sum_{22} $$

$$ P(X_{1 \vert 2}) = \mathcal{N}(M_{1 \vert 2}^m, V_{1 \vert 2}^m) $$ \\
$$ M_{1 \vert 2}^m = \mu_1 + \sum_{12} \sum_{22}^{-1} (X_2 - \mu_2) $$ \\
$$ V_{1 \vert 2}^m = \sum_{11} - \sum_{12} \sum_{22}^{-1} \sum_{21} $$

Using this information, we can compute the measurement update (update step) as:
<d-math block>
\begin{aligned}
\hat X_{t+1 \vert t+1} &= \hat X_{t+1 \vert t} + K_{t+1} (Y_{t+1} - C \hat X_{t+1 \vert t}) \\
P_{t+1 \vert t+1} &= P_{t+1 \vert t} - KCP_{t+1 \vert t}\\
\end{aligned}
</d-math>
Here $K_{t+1} = P_{t+1 \vert t} C^T (C P_{t+1 \vert t} C^T + R)^{-1}$ and is known as the Kalman gain matrix. An interesting point to note is that $K_t$ is independent of $Y_t$ (i.e. the data), so it can be precomputed to improve efficiency.

### Example of Kalman Filtering in 1-D
Suppose we have some noisy observations of a particle performing a random walk in 1-D. Assume our states and observations are defined as follows: \\
$ X_{t \vert t-1} = X_{t-1} + W $ where $W \sim \mathcal{N}(0,\sigma_x)$ \\
$ Z_{t} = X_{t} + V $ where $V \sim \mathcal{N}(0,\sigma_z)$ \\
We can compute KF updates for this model as follows:\\
$P_{t+1 \vert t} = AP_{t \vert t}A + GQG^T = \sigma_t + \sigma_z$\\
$\hat X_{t+1 \vert t} = A\hat X_{t|t} = \hat X_{t|t}$\\
$K_{t+1} = P_{t+1 \vert t} C^T (C P_{t+1 \vert t} C^T + R)^{-1} = (\sigma_t + \sigma_x)(\sigma_t + \sigma_x + \sigma_z)$\\
$\hat X_{t+1 \vert t+1} &= \hat X_{t+1 \vert t} + K_{t+1} (Z_{t+1} - C \hat X_{t+1 \vert t}) = \frac{(\sigma_t + \sigma_x)Z_t + \sigma_z \hat X_{t|t}}{\sigma_t + \sigma_x + \sigma_z}$
$P_{t+1 \vert t+1} = \frac{(\sigma_t + \sigma_x) \sigma_z}{\sigma_t + \sigma_x + \sigma_z}$

### Understanding the intuition behind Kalman Filtering
In the KF update equation for the mean, $\hat X_{t+1 \vert t+1} &= \hat X_{t+1 \vert t} + K_{t+1} (Z_{t+1} - C \hat X_{t+1 \vert t})$, the term $(Z_{t+1} - C \hat X_{t+1 \vert t})$ is called the **innovation** term. We can see that the update equation for new belief is a convex weighted combination of updates from prior and observation, with the Kalman Gain matrix acting as the weight. From the equation for the Kalman Gain matrix, we can see that if observations are noisy ($\sigma_z$ or $R$ is large), then the KG matrix is small and updates rely more on prior. On the other hand if the process is unpredictable (large $\sigma_x$) or prior is unreliable (large $\sigma_t$), the KG matrix is higher and we rely more on the observation. 

## Motivating Example: Probabilistic Topic Model
Probabilistic topic model is used here to demonstrate the challenge with inference on graphic models and the necessity of approximate inference. 

### Problem Motivation: 
It is difficult for human to handle a large number of textual documents. It would be helpful to automate some of such processes, such as search, browse or measure similarity.

A specific task is **document embedding**, i.e. finding low-dimensional representation of documents. Furthermore, it is desirable that the latent representation corresponds to semantic meaning, such as topics. One approach to such a representation is to look at frequent words that corresponds to a topic. 

Using the embedding, one application is to study the evolution of documents over time. Another application is to track user interest based on his/her posts on social media.

### Representation:
**Bag of words** representation is the starting point of topic modeling. Specifically, each document is represented as a vector in word space, i.e. count of each word in the dictionary. 

The main advantage of this method is simplicity. The limitation is that the ordering of words is neglected. To give an example: two documents of different length is not comparable under a representation based on word ordering. The longer document has smaller likelihood by taking the product of a longer sequence. Under the **bag of words** representation, any two documents would be vectors of same length and thus comparable.

Documents are usually represented as very long vectors under **bag of words**, due to the large size of the dictionary. The representation can be more compact with topic modeling. 

To model semantic meaning in a document, one look at keywords that correspond to a specific topic. Figure 1 provides a concrete example. Keywords such as "source", "target" and "BLEU" show that the document is about machine translation. The document also contains vocabulary associated with topic such as syntax and learning.
 
Furthermore, one can assign probability to each topic. In this example, keywords on machine translation are most frequent, so we assign a larger probability. There is some mention related to syntax and learning, so we assign some probability based on word frequency.

<figure id="example-figure" class="l-body-outset">
  <div class="row">
    <div class="col one">
      <img src="{{ 'assets/img/lecture-11/example.png' | relative_url }}" />
    </div>
  </div>
  <figcaption>
    <strong>Figure 1 Example of Topic Model Architecture</strong>
  </figcaption>
</figure>


To sum up, a document is first represented with bag of words. Then, the bag of words representation is transformed into strength on topics, which is a very compact representation.  
 
### Topic Models:
The probability of each word in a document, $P(w)$, can be decomposed into the distribution of topics in a document, $P(z)$, and the probability of a word given the topic, $P(w|z)$.

$$P(w) = P(w|z)P(z)$$

A related concept is **latent semantic indexing (LSI)**. LSI decomposes matrix with linear algebra-based method. However, the drawback of LSI, which involves matrix inversion, is high computational cost.  


The architecture of topic model is shown in Figure 2. To sample from a document, one first draw a topic distribution $\theta$ based on the prior. For a document with $N_d$ words, one first draw topic indicators, z, from topic distribution, $\theta$. Then one draws words, w, from word-frequency distribution, K, conditioning on the topic indicator, z. 

<figure id="example-figure" class="l-body-outset">
  <div class="row">
    <div class="col one">
      <img src="{{ 'assets/img/lecture-11/Architecture.png' | relative_url }}" />
    </div>
  </div>
  <figcaption>
    <strong>Figure 2 Architecture of Topic Model Architecture</strong>
  </figcaption>
</figure>


## Equations

This theme supports rendering beautiful math in inline and display modes using [KaTeX](https://khan.github.io/KaTeX/) engine.
You just need to surround your math expression with `$`, like `$ E = mc^2 $`.
If you leave it inside a paragraph, it will produce an inline expression, just like $E = mc^2$.

To use display mode, again surround your expression with `$$` and place it as a separate paragraph.
Here is an example:

$$
\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
$$

Alternatively and for more complex math environments, use `<d-math block>...</d-math>` tags.
Here is an example:

<d-math block>
\begin{aligned}
\left( \sum_{i=1}^n u_i v_i \right)^2 & \leq \left( \sum_{i=1}^n u_i^2 \right) \left( \sum_{i=1}^n v_i^2 \right) \\
\left| \int f(x) \overline{g(x)} dx \right|^2 & \leq  \int |f(x)|^2 dx \int |g(x)|^2 dx
\end{aligned}
</d-math>

Note that [KaTeX](https://khan.github.io/KaTeX/) is work in progress, so it does not support the full range of math expressions as, say, [MathJax](https://www.mathjax.org/).
Yet, it is [blazing fast](http://www.intmath.com/cg5/katex-mathjax-comparison.php).

***

## Figures

To add figures, use `<figure>...</figure>` tags.
Within the tags, define multiple rows of images using `<div class="row">...</div>`.
To add captions, use `<figcaption>...</figcaption>` tags.

Here is an example usage of a figure that consists of a row of images with a caption:

<figure id="example-figure" class="l-body-outset">
  <div class="row">
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/1.jpg' | relative_url }}" />
    </div>
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/2.jpg' | relative_url }}" />
    </div>
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/3.jpg' | relative_url }}" />
    </div>
  </div>
  <figcaption>
    <strong>Figure caption title in bold.</strong>
    An example figure caption.
  </figcaption>
</figure>

Note that the figure uses `class="l-body-outset"` which lets it take more horizontal space.
For more on this, see layouts section below.
Also, the size of the images themselves is controlled by `class="one"`, `class="two"`, or `class="three"` which corresponds to 1/3, 2/3, 3/3 of the full horizontal space, respectively.

Here is the same example, but each image is captioned separately:
<figure id="example-figure" class="l-body-outset">
  <div class="row">
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/1.jpg' | relative_url }}" />
      <figcaption>
        <strong>Figure caption title 1.</strong>
        Caption text for figure 1.
      </figcaption>
    </div>
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/2.jpg' | relative_url }}" />
      <figcaption>
        <strong>Figure caption title 2.</strong>
        A very very very long caption text for figure 2 so that it is longer than the image itself.
      </figcaption>
    </div>
  </div>
</figure>

Here is an example that shows how the figures of different sizes are aligned:

<figure>
  <div class="row">
    <div class="col two">
      <img src="{{ 'assets/img/notes/template/4.jpg' | relative_url }}" />
    </div>
    <div class="col one">
      <img src="{{ 'assets/img/notes/template/2.jpg' | relative_url }}" />
      <figcaption>
        <strong>Subcaption.</strong>
        The content of the subcaption.
      </figcaption>
    </div>
  </div>
  <figcaption>
    <strong>The second row figure caption title.</strong>
    An example of a sencond row figure caption.
  </figcaption>
</figure>

***

## Citations

Citations are then used in the article body with the `<d-cite>` tag.
The key attribute is a reference to the id provided in the bibliography.
The key attribute can take multiple ids, separated by commas.

The citation is presented inline like this: <d-cite key="gregor2015draw"></d-cite> (a number that displays more information on hover).
If you have an appendix, a bibliography is automatically created and populated in it.

Distill chose a numerical inline citation style to improve readability of citation dense articles and because many of the benefits of longer citations are obviated by displaying more information on hover.
However, we consider it good style to mention author last names if you discuss something at length and it fits into the flow well — the authors are human and it’s nice for them to have the community associate them with their work.

***

## Footnotes

Just wrap the text you would like to show up in a footnote in a `<d-footnote>` tag.
The number of the footnote will be automatically generated.<d-footnote>This will become a hoverable footnote.</d-footnote>

***

## Code Blocks

Syntax highlighting is provided within `<d-code>` tags.
An example of inline code snippets: `<d-code language="html">let x = 10;</d-code>`.
For larger blocks of code, add a `block` attribute:

<d-code block language="javascript">
  var x = 25;
  function(x) {
    return x * x;
  }
</d-code>

***

## Layouts

The main text column is referred to as the body.
It is the assumed layout of any direct descendants of the `d-article` element.

<div class="fake-img l-body">
  <p>.l-body</p>
</div>

For images you want to display a little larger, try `.l-page`:

<div class="fake-img l-page">
  <p>.l-page</p>
</div>

All of these have an outset variant if you want to poke out from the body text a little bit.
For instance:

<div class="fake-img l-body-outset">
  <p>.l-body-outset</p>
</div>

<div class="fake-img l-page-outset">
  <p>.l-page-outset</p>
</div>

Occasionally you’ll want to use the full browser width.
For this, use `.l-screen`.
You can also inset the element a little from the edge of the browser by using the inset variant.

<div class="fake-img l-screen">
  <p>.l-screen</p>
</div>
<div class="fake-img l-screen-inset">
  <p>.l-screen-inset</p>
</div>

The final layout is for marginalia, asides, and footnotes.
It does not interrupt the normal flow of `.l-body` sized text except on mobile screen sizes.

<div class="fake-img l-gutter">
  <p>.l-gutter</p>
</div>

***

## Arbitrary $$\LaTeX$$ (experimental)

In fact, you can write entire blocks of LaTeX using `<latex-js>...</latex-js>` tags.
Below is an example:<d-footnote>If you don't see anything, it means that your browser does not support Shadow DOM.</d-footnote>

<latex-js style="border: 1px dashed #aaa;">
This document will show most of the supported features of \LaTeX.js.

\section{Characters}

It is possible to input any UTF-8 character either directly or by character code
using one of the following:

\begin{itemize}
    \item \texttt{\textbackslash symbol\{"00A9\}}: \symbol{"00A9}
    \item \verb|\char"A9|: \char"A9
    \item \verb|^^A9 or ^^^^00A9|: ^^A9 or ^^^^00A9
\end{itemize}

\bigskip

\noindent
Special characters, like those:
\begin{center}
\$ \& \% \# \_ \{ \} \~{} \^{} \textbackslash % \< \>  \"   % TODO cannot be typeset
\end{center}
%
have to be escaped.

More than 200 symbols are accessible through macros. For instance: 30\,\textcelsius{} is
86\,\textdegree{}F.
</latex-js>

Note that you can easily interleave latex blocks with the standard markdown.

<latex-js style="border: 1px dashed #aaa;">
\section{Environments}

\subsection{Lists: Itemize, Enumerate, and Description}

The \texttt{itemize} environment is suitable for simple lists, the \texttt{enumerate} environment for
enumerated lists, and the \texttt{description} environment for descriptions.

\begin{enumerate}
    \item You can nest the list environments to your taste:
        \begin{itemize}
            \item But it might start to look silly.
            \item[-] With a dash.
        \end{itemize}
    \item Therefore remember: \label{remember}
        \begin{description}
            \item[Stupid] things will not become smart because they are in a list.
            \item[Smart] things, though, can be presented beautifully in a list.
        \end{description}
    \item Technical note: Viewing this in Chrome, however, will show too much vertical space
        at the end of a nested environment (see above). On top of that, margin collapsing for inline-block
        boxes is not allowed. Maybe using \texttt{dl} elements is too complicated for this and a simple nested
        \texttt{div} should be used instead.
\end{enumerate}
%
Lists can be deeply nested:
%
\begin{itemize}
  \item list text, level one
    \begin{itemize}
      \item list text, level two
        \begin{itemize}
          \item list text, level three

            And a new paragraph can be started, too.
            \begin{itemize}
              \item list text, level four

                And a new paragraph can be started, too.
                This is the maximum level.

              \item list text, level four
            \end{itemize}

          \item list text, level three
        \end{itemize}
      \item list text, level two
    \end{itemize}
  \item list text, level one
  \item list text, level one
\end{itemize}

\section{Mathematical Formulae}

Math is typeset using KaTeX. Inline math:
$
f(x) = \int_{-\infty}^\infty \hat f(\xi)\,e^{2 \pi i \xi x} \, d\xi
$
as well as display math is supported:
$$
f(n) = \begin{cases} \frac{n}{2}, & \text{if } n\text{ is even} \\ 3n+1, & \text{if } n\text{ is odd} \end{cases}
$$

</latex-js>

Full $$\LaTeX$$ blocks are supported through [LaTeX JS](https://latex.js.org/){:target="\_blank"} library, which is still under development and supports only limited functionality (which is still pretty cool!) and does not allow fine-grained control of the layout, fonts, etc.

*Note: We do not recommend using using LaTeX JS for writing lecture notes at this stage.*

***

## Print

Finally, you can easily get a PDF or printed version of the notes by simply hitting `ctrl+P` (or `⌘+P` on macOS).
