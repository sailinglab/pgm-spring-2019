---
layout: distill
title: Lecture Notes Template
description: An example of a distill-style lecture notes that showcases the main elements.
date: 2019-01-09

lecturers:
  - name: Eric Xing
    url: "https://www.cs.cmu.edu/~epxing/"

authors:
  - name: Author 1  # author's full name
    url: "#"  # optional URL to the author's homepage
  - name: Author 2
    url: "#"
  - name: Author 3
    url: "#"

editors:
  - name: Editor 1  # editor's full name
    url: "#"  # optional URL to the editor's homepage

abstract: >
  An example abstract block.
---

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

