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
  - name: D. Bayani
    url: "#"
  - name: Bingqing Chen
    url: "#"

editors:
  - name: Editor 1  # editor's full name
    url: "#"  # optional URL to the editor's homepage

abstract: >
  An example abstract block.
---
## Note on Lecture Content
Due to the previous lecture running over, the actual
material covered in the lecture deviated from what the title of the lecture
on the course homepage suggests. 

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

[comment]: I believe this is  where Aakanksha stopped, roughly 

[comment]:V~V~V~~V~~VV~V~V~V~V~V~VV~V~~V~~VVV~V~V~V~V~V~V~~V~V~VV~VV~VV~VV~VV~V~~V~~V~V~V~V~V
[comment]: dcbayani section. Time in video: start: 27:07  , stop: 
[comment]:-----------------------------------------------------------------------------------

## Dicussion of Where the A, G, and C Matrix Come From 
[comment]: starts around 29 minutes, ends around 31 minutes
Up to this point, we have discussed inference in the Kalmann filter model; given the 
model up-front, tell me something about the data. This leaves open where the matrices A, G, and
C come from, however. This is a similar situation we were in for HMMs: to find the necessary 
matrices, we must do learning. Using approaches like EM we can interleave learning and inference
to come across the parameters of interest.

Furthering this comparison to HMMs, the Rauch-Tung-Strievel algorithm allows us to perform "exact off-line inference in an LDS", and is essentially a "Guassian analog of the forwards-backwards" algorithm.

## Learning SSMs
[comment]: starts around minute 31, ends around 32:52....
In order to learn the necessary parameters for the Kalmann filter, 
we calculate the complete data liklihood:
<d-math block>
\begin{aligned}
$l_t(\theta, D) = \sum_{n}p(x_n, y_n) = (\sum_n log(p(x_1))) + (\sum_n\sum_t log(p(x_{n,t} | x_{n, t-1})) + (\sum_n\sum_t log(p(y_{n,t} | x_{n, t}))) =\\
f_1(X; \Sigma_0) + f_2(\{X_tX_{t-1}^{T}, X_tX_t^{T}, X_t: \forall t\}, A, Q, G) + 
f_3(\{X_tX_t^{T}, X_t: \forall t\}, C, G) $\\
\end{aligned}
</d-math>
This is very similar to what we saw in factor analysis, except there, we 
computed this for each individual time-step, whereas here we do it 
for all time-steps. From here, we proceed as usual in EM:
in the E-step, we estimate $X_tX_{t-1}^{T}$, $X_tX_t^{T}$, and $X_t$
by taking their expectation in respect to the observation, and in the 
M-step we use MLE in the typical fashion. 

## Non-Linear Systems

The approaches discussed thus far are designed to handle linear systems.
In order to handle a non-linear system, an approximation must be made. 
For example, for non-linear differentiable systems, Taylor expansion
allows us to use linear terms to approximate non-linear curves.

With that, we close the modeling section of the course and move on to the 
next subject.

### Approximate Inference and Topic Models: Mean Field and Loopy Belief Prop

Thus far in the course, we have covered the elimination algorithm, message passing, and
algorithms that are powered based on those principles. These techniques allowed for 
exact inference, and while they have been shown useful, they cannot cope with many of 
the settings and problems we wish to explore. This motivates uses of approximate
techniques, which we will begin discussing in this lecture.


[comment]: from roughly 41:00 to 43:00, Dr. Xing discussed the general thought process and
[comment]:     art of modeling, leading up to discussion of probabilistic topic models.

## Some Discussion of a Task, and How to Tackle It with Appropraite Modeling

With contemporary excitement about ML and particularly Deep Models, it is not 
uncommon for students to want to select a model that interests them and try
to apply it to some difficult tasks. It is typically more appropraite and sound
to go the other way - find the righ model and methods to handle a task at hand.

To begin discussion of the next subject and motive its development, we consider
the problem of trying to given someone a summary, a "bird's-eye view", or one
million or more documents. That is our task - we know at some point, to get a 
handle on it, we have to convert it to mathematical language. To do this, we 
have to consider a framework to put it in mathematically. Is this a classification
task? No, we have not even discussed labels. Is it a clustering task? Maybe, 
but the cluster-label itself would be very weakly informative of what is actually
going on in the documents. Embeddings, representing each document as a point
in a space or plane? Maybe. One has to decide on this matter to move forward.

Another point to decide is representation of the data. We want to deal with 
text ultimately, which is a sequence of words. How do we want to represent that?
Binary vectors? Counts? This is a design choice one must consider. 

After deciding the task and the data representation, one may consider a model
to fit these. From there, one can consider how inference can be done on the 
model. After that, how learning can be accomplished may be considered so that
parameters to the model may be filled in an informed fashion. Finally, after all
the modeling and processing is done, results may be evaluated to get a sense
of how well our methods are doing. In general, it is best to handle each 
step of this process one at a time. This is part of the art of modeling.


[comment]:^_^_^_^_^_^__^_^_^_^_^_^_^_^_^_^_^_^__^__^_^^_^^__^_^_^_^_^^__^_^__^^_^_^__^__^^_^_^

[comment]: below is where Bingqing started , I suspect... it looks like about 40 minutes into the 
[comment]:     video. 


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


[comment]: Above is Bingqing's section - I believe it was said more content is to 
[comment]: come. 



[comment]:V~V~V~~V~~VV~V~V~V~V~V~VV~V~~V~~VVV~V~V~V~V~V~V~~V~V~VV~VV~VV~VV~VV~V~~V~~V~V~V~V~V
[comment]: dcbayani section. Time in video: start:  , stop: 
[comment]:-----------------------------------------------------------------------------------




[comment]:^_^_^_^_^_^__^_^_^_^_^_^_^_^_^_^_^_^__^__^_^^_^^__^_^_^_^_^^__^_^__^^_^_^__^__^^_^_^








