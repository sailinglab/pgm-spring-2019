---
layout: page
permalink: /project/
title: Course Project
description: Guidelines and suggestions for course projects
---

Your class project is an opportunity for you to explore an interesting problem in the context of a real-world data sets.
Projects should be done in teams of three students.
Each project will be assigned a TA as a project consultant/mentor; instructors and TAs will consult with you on your ideas, but of course the final responsibility to define and execute an interesting piece of work is yours. Your project will be worth 46% of your final class grade, and will have 4 deliverables:

1. **Proposal** : 2 pages excluding references (10%)
2. **Midway Report** : 5 pages excluding references (20%)
3. **Presentation** : poster presentation (20%)
4. **Final Report** : 8 pages excluding references (50%)

All write-ups should use the [ICML style](https://media.neurips.cc/Conferences/ICML2019/Styles/icml2019_style.zip).

***

* (The list will be replaced with the table of contents.)
{:toc}

***

### Team Formation

You are responsible for forming project teams of 3-4 people.
In some cases, we will also accept teams of 2, but a 3-4-person group is preferred.
Once you have formed your group, please send one email per team to the class instructor list with the names of all team members.
If you have trouble forming a group, please send us an email and we will help you find project partners.

### Project Proposal

You must turn in a brief project proposal that provides an overview of your idea and also contains a brief survey of related work on the topic.
We will provide a list of suggested project ideas for you to choose from, though you may discuss other project ideas with us, whether applied or theoretical.
Note that even though you can use datasets you have used before, **you cannot use work that you started prior to this class as your project**.

Proposals should be approximately **two pages long**, and should include the following information:

- Project title and list of group members.
- Overview of project idea. This should be approximately half a page long.
- A short literature survey of 4 or more relevant papers. The literature review should take up approximately one page.
- Description of potential data sets to use for the experiments.
- Plan of activities, including what you plan to complete by the midway report and how you plan to divide up the work.

The grading breakdown for the proposal is as follows:

- 40% for clear and concise description of proposed method
- 40% for literature survey that covers at least 4 relevant papers
- 10% for plan of activities
- 10% for quality of writing

The project proposal will be due at **11:59 PM on Friday, February 22th**, and should be submitted via [Gradescope](https://www.gradescope.com/courses/36025).

### Midway Report

The midway report will serve as a check-point at the halfway mark of your project.
It should be about **5 pages long**, and should be formatted like a conference paper, with the following sections: introduction, background & related work, methods, experiments, conclusion.
The introduction and related work sections should be in their final form; the section on the proposed methods should be almost finished; the sections on the experiments and conclusions will have the results you have obtained, perhaps with place-holders for the results you plan/hope to obtain.

The grading breakdown for the midway report is as follows:

- 20% for introduction and literature survey
- 40% for proposed method
- 20% for the design of upcoming experiments and revised plan of activities (in an appendix, please show the old and new activity plans)
- 10% for data collection and preliminary results
- 10% for quality of writing

The project midway report will be due at **11:59 PM on Friday, March 29th**, and must be submitted via [Gradescope](https://www.gradescope.com/courses/36025).

### Final Report

Your final report is expected to be **8 pages excluding references**, in accordance with the length requirements for an ICML paper. It should have roughly the following format:

- Introduction: problem definition and motivation
- Background & Related Work: background info and literature survey
- Methods
-- Overview of your proposed method
-- Intuition on why should it be better than the state of the art
-- Details of models and algorithms that you developed
- Experiments
-- Description of your testbed and a list of questions your experiments are designed to answer
-- Details of the experiments and results
- Conclusion: discussion and future work

The grading breakdown for the final report is as follows:

- 10% for introduction and literature survey
- 30% for proposed method (soundness and originality)
- 30% for correctness, completeness, and difficulty of experiments and figures
- 10% for empirical and theoretical analysis of results and methods
- 20% for quality of writing (clarity, organization, flow, etc.)

The project final report will be due at **11:59 PM on Friday, May 10th** (tentative), and must be submitted via [Gradescope](https://www.gradescope.com/courses/36025).

### Presentation

All project teams will present their work at the end of the semester.
We will have a 2-3-hour long poster session held in NSH atrium on April 30.
Each team should prepare a poster (similar in style to a conference poster) and present it during the allocated time.
If applicable, live demonstrations of your software are highly encouraged.

## Project Suggestions

If you are interested in a particular project, please contact the respective *contact person* to get further ideas or details.
We may add more project suggestions down the road.

***

#### Deep generative models for disentangled representation learning
**Contact person:** [Paul Liang](https://www.cs.cmu.edu/~pliang/){:target="\_blank"}

Disentangled representation learning involves learning a set of latent variables that each capture individual factors of variation in the data.
For example, when we learn a generative model for shapes, it would be ideal if each latent variables would correspond to the shapes pose, shadow, rotations, lighting etc.
This improves interpretability of our learned representations and allows flexible generation from latent variables.
You can explore new methods of learning disentangled representations in both supervised and unsupervised settings (i.e. whether information about pose, shadow, rotations are given or not), design metrics for improved evaluation of disentanglement in models, as well as new applications of disentangled representation learning to improve performance on NLP, vision, and multimodal tasks.

**References:**

1. [Papers in NIPS 2017 workshop on disentangled representation learning](https://sites.google.com/view/disentanglenips2017){:target="\_blank"}.
2. Denton et al., [Unsupervised Learning of Disentangled Representations from Video](https://papers.nips.cc/paper/7028-unsupervised-learning-of-disentangled-representations-from-video){:target="\_blank"}. NIPS 2017.
3. Chen et al., [InfoGAN: Interpretable Representation Learning by Information Maximizing Generative Adversarial Nets](https://arxiv.org/abs/1606.03657){:target="\_blank"}. NIPS 2016.
4. Kulkarni et al., [Deep Convolutional Inverse Graphics Network](https://arxiv.org/abs/1503.03167){:target="\_blank"}. NIPS 2015.

***

#### Deep generative models for video, text, and audio generation
**Contact person:** [Paul Liang](https://www.cs.cmu.edu/~pliang/){:target="\_blank"}

Generative models are important for probabilistic reasoning within graphical models. Recent advancements in parameterizing these models using deep neural networks and optimizating using gradient-based techniques have enabled large scale modeling of high-dimensional, real-world data. Deep generative models have been successfully been applied for image, text, and audio generation.
You can explore new applications of deep generative models, improve the theoretical understanding and empirical optimization of deep generative models, design metrics for improved evaluation of deep generative models, and other new directions. 

**References:**

1. [IJCAI Tutorial on Deep Generative Models by Aditya Grover and Stefano Ermon](https://ermongroup.github.io/generative-models/){:target="\_blank"}.
2. [ICML Workshop on Deep Generative Models](https://sites.google.com/view/tadgm/home){:target="\_blank"}.
3. Brock et al., [Large Scale GAN Training for High Fidelity Natural Image Synthesis](https://arxiv.org/abs/1809.11096){:target="\_blank"}. ICLR 2019.
4. Hu et al., [Toward Controlled Generation of Text](https://arxiv.org/pdf/1703.00955.pdf){:target="\_blank"}. ICML 2017.
5. van den Oord et al., [WaveNet: A Generative Model for Raw Audio](https://arxiv.org/abs/1609.03499){:target="\_blank"}. arXiv 2016.

***

#### Squeezing NO TEARS: scalable Bayesian network structure learning
**Contact person:** [Xun Zheng](https://www.cs.cmu.edu/~xunzheng/){:target="\_blank"}

Estimating Bayesian network structure from data is one of the fundamental problems in graphical models. 
A similar problem of estimating Markov network structure has efficient solutions such as the graphical lasso [1]. 
However, compared to Markov networks, estimating Bayesian networks involves extra challenges: 1) the adjacency matrix is not symmetric; 2) the acyclicity constraint is combinatorial. 
Recently [2] proposed a smooth characterization of directed acyclic graphs, enabling continuous optimization for Bayesian network structure learning, similar to graphical lasso for Markov networks. 

In this project, your goal would be to scale up the algorithm of [2] to thousands of nodes. 
Some computation can be saved by exploiting the problem structure, and some computation can be made more efficient using various approximation techniques. 

**References:**

1. Friedman, J., Hastie, T., & Tibshirani, R. (2008). Sparse inverse covariance estimation with the graphical lasso. Biostatistics.
2. Zheng, X., Aragam, B., Ravikumar, P., & Xing, E. P. (2018). DAGs with NO TEARS: Continuous Optimization for Structure Learning. In Advances in Neural Information Processing Systems.

***

#### Optimization-based decoding for improved neural machine translation
**Contact person:** [Maruan Al-Shedivat](https://www.cs.cmu.edu/~mshediva/){:target="\_blank"}

Encoder-decoder [1] with attention [2] is a typical architecture of modern neural machine translation (NMT) systems.
Arguably, the quality of the decoder (as well as the decoding process itself) significantly affects translation and often requires large amounts of parallel training data.

In this project, your goal would be to explore the potential of building more efficient decoders using pre-trained target language models (LMs).
The idea is inspired by a recent technique used in model-based reinforcement learning [3]:

> Given a sentence in the source language and a pre-trained target LM, generate a sequence of words in the target language by starting from a random sequence and iteratively refining it to increase its likelihood under the given LM.

The challenge is to ensure that by optimizing the language model (that represents an unconditional distribution), the generated sentence is a valid translation (i.e., preserves the meaning of the source sentence).

**References:**

1. Sutskever, Vinyals, Le. [Sequence to sequence learning with neural networks](http://papers.nips.cc/paper/5346-sequence-to-sequence-learnin){:target="\_blank"}. NIPS 2014.
2. Bahdanau, Cho, Bengio. [Neural machine translation by jointly learning to align and translate](https://arxiv.org/abs/1409.0473){:target="\_blank"}. ICLR 2015.
3. Srinivas, Jabri, Abbeel, Levine, Finn. [Universal Planning Networks](https://arxiv.org/abs/1804.00645){:target="\_blank"}. ICML 2018.

***

#### Learning contextual models for personalization, interpretability, and beyond
**Contact person:** [Maruan Al-Shedivat](https://www.cs.cmu.edu/~mshediva/){:target="\_blank"}

Oftentimes, we would like the models of our data to be not only accurate, but also human-interpretable.
A recently developed class of models, called Contextual Explanation Networks (CENs) [1], provides a flexible way to achieve this: on a high level, it allows to learn families of contextualized simple/interpretable models (e.g., sparse linear), called explanations, which are 'glued' together via deep neural networks.
In essence, CENs model conditional probability distributions of the form $$P(Y \mid X, C)$$, distinguishing between semantic (or interpretable) features $$X$$ and non-semantic features $$C$$.
There is a number of interesting directions one could take CEN further.

1. **Beyond linear explanations.** <br>
The original paper [1] developed CEN with only linear explanations (for scalar and structured output spaces).
Is it possible to use other types of simple models?
For instance, lists of rules [2] or their causal version [3] is a popular method when it comes to interpretability.
However, is it possible to integrate such models into the CEN framework and make them trainable end-to-end?
Applications of ML in the healthcare domain may significantly benefit from such models.

2. **Beyond conditional models.** <br>
CEN was designed to represent conditional distributions, i.e., directly answer queries such as, *What is the probability of $$Y$$ given $$X$$ and $$C$$?*
The problem is that the model always requires having access to *two modalities* of the input ($$X$$ and $$C$$), which is a limitation, since in a real-world scenario, certain data modalities might be missing or hard to obtain.
Hence, is it possible to build a CEN model that works with missing or latent $$X$$ or $$C$$ variables?
Is building a contextual model for the join distribution over $$X, C, Y$$ the right way to go?

3. **CEN for few-shot learning and/or meta-learning.** <br>
Note the CEN framework technically uses DNNs to generate parameters for simpler models (to contextualize them).
More generally, part of the model is used to 'modulate' another part of the model, which has been successful in a number of areas [4], including zero-shot learning, multilingual translation [5], etc.
Multitask few-shot learning and meta-learning [6] pose a new interesting setup, in which contextual/conditional models could work very well [7].
Another direction to explore in your projects is the design and implementation of CEN-like models for these new tasks.

**References:**

1. Al-Shedivat, Dubey, Xing. [Contextual explanation networks](https://arxiv.org/abs/1705.10301){:target="\_blank"}. arXiv 2017.
2. Wang, Rudin. [Falling rule lists](https://arxiv.org/abs/1411.5899){:target="\_blank"}. AISTATS 2015.
3. Wang, Rudin. [Causal falling rule lists](https://arxiv.org/abs/1510.05189){:target="\_blank"}. FATML workshop 2017.
4. Dumoulin et al. [Feature-wise transformations](https://distill.pub/2018/feature-wise-transformations/){:target="\_blank"}. Distill 2018.
5. Platanios et al. [Contextual parameter generation for neural machine translation](https://blog.ml.cmu.edu/2019/01/14/contextual-parameter-generation-for-universal-neural-machine-translation/){:target="\_blank"}. EMNLP 2018.
6. Finn, Abbeel, Levine. [Model-agnostic meta-learning for fast adaptation of neural networks](https://arxiv.org/abs/1703.03400){:target="\_blank"}. ICML 2017.
7. Garnelo et al. [Conditional neural processes](https://arxiv.org/abs/1807.01613){:target="\_blank"}. ICML 2018.

***

#### Hierarchical RL & Maximum Entropy RL

**Contact person:** [Lisa Lee](http://leelisa.com){:target="\_blank"}

Reinforcement learning (RL) is typically formulated as a **Markov decision process (MDP)** of an agent interacting with the environment to maximize its cumulative reward. More specifically, an MDP is a tuple $$(\mathcal{S}, \mathcal{A}, \mathcal{T}, \mathcal{R}, \gamma)$$ where $$\mathcal{S}$$ is a set of states, $$\mathcal{A}$$ is a set of actions, $$\mathcal{T}(s' \mid s, a)$$ is the transition probability of ending up in state $$s' \in \mathcal{S}$$ when executing action $$a \in \mathcal{A}$$ in state $$s \in \mathcal{S}$$, $$\mathcal{R}: \mathcal{S} \rightarrow \mathbb{R}$$ is the reward function, and $$\gamma \in (0, 1]$$ is a discount factor. A policy $$\pi$$ maps each state-action pair $$(s, a) \in \mathcal{S} \times \mathcal{A}$$ to the probability $$\pi(s, a)$$ of taking action $$a$$ when in state $$s$$. The agent's goal is to learn a policy that maximizes its cumulative discounted reward $$\mathbb{E}_\pi\left[\sum_t \gamma^t r_t \right]$$.

In the last several years, deep learning has helped achieve major breakthroughs in RL by enabling methods to automatically learn features from high-dimensional observations (e.g., raw image pixels). These advances have especially benefited vision-based RL problems and robotic manipulation methods. Despite the progress, several key challenges limit the applicability and scalability of deep RL algorithms. For example, efficient exploration and long-term credit assignment remain core problems, especially in settings with sparse or delayed rewards. Another challenge is that the data inefficiency of deep RL algorithms makes training computationally expensive and difficult to scale in the complexity and number of tasks.

One framework to tackle these challenges is **hierarchical RL (HRL)**, which enables temporal abstraction by learning hierarchical policies operating at different timescales and decomposing tasks into smaller subtasks. Another interesting line of work is **maximum entropy RL** which encourages agents to learn diverse behaviors agnostic of the task.

I'd be happy to share more specific project ideas and advise students. Please feel free to stop by office hours if interested.

**Some relevant works:**

1. [Feudal Reinforcement Learning (1993)](http://www.cs.toronto.edu/~fritz/absps/dh93.pdf){:target="\_blank"}
2. [Between MDPs and semi-MDPs: A framework for temporal abstraction in reinforcement learning (1999)](https://www.sciencedirect.com/science/article/pii/S0004370299000521){:target="\_blank"}
3. [FeUdal Networks for Hierarchical Reinforcement Learning (2017)](https://arxiv.org/abs/1703.01161){:target="\_blank"}
4. [Hierarchical Deep Reinforcement Learning:Integrating Temporal Abstraction andIntrinsic Motivation (2016)](http://papers.nips.cc/paper/6233-hierarchical-deep-reinforcement-learning-integrating-temporal-abstraction-and-intrinsic-motivation.pdf){:target="\_blank"}
5. [Learning Diverse Skills via Maximum Entropy Deep Reinforcement Learning (2017)](https://bair.berkeley.edu/blog/2017/10/06/soft-q-learning/){:target="\_blank"}
6. [Modular Multitask Reinforcement Learning with Policy Sketch (2017)](https://arxiv.org/pdf/1611.01796.pdf){:target="\_blank"}
7. [On the Complexity of Exploration in Goal-Driven Navigation (2018)](https://arxiv.org/abs/1811.06889){:target="\_blank"}
8. [Learning Self-Imitating Diverse Policies (2018)](https://arxiv.org/abs/1805.10309){:target="\blank"}

***

#### Large-scale (scalable) Machine Learning

**Contact person:** [Hao Zhang](http://www.cs.cmu.edu/~hzhang2/){:target="\_blank"}

Machine Learning nowadays has been applied in extremely large dataset, posing many challenges on existing models and algorithms -- lack of scalability, lack of guarantee of convergence, inefficient inference, difficulty of programming over big data and big models, etc. This topic will allow us to explore different directions in large-scale machine learning to address the aforementioned problems:

- **Data parallelism and model parallelism** [1-4]
- **Large batch SGD, SGD with staleness** [3, 4, 5, 7]
- **Efficient Training/inference of Dynamic Neural Networks** [6, 8]
- **Scalable ML Systems** [1-8]

**References**:

1. [Large Scale Distributed Deep Networks](https://www.cs.toronto.edu/~ranzato/publications/DistBeliefNIPS2012_withAppendix.pdf){:target="\_blank"}.
2. [Intro to Distributed Deep Learning Systems](https://medium.com/@Petuum/intro-to-distributed-deep-learning-systems-a2e45c6b8e7){:target="\_blank"}.
3. [More Effective Distributed ML via a Stale Synchronous Parallel Parameter Server](https://www.petuum.com/pdf/SSPTable_NIPS2013.pdf){:target="\_blank"}.
4. [Accurate, Large Minibatch SGD: Training ImageNet in 1 Hour](https://arxiv.org/abs/1706.02677){:target="\_blank"}.
5. [An Empirical Model of Large-Batch Training](https://arxiv.org/abs/1812.06162){:target="\_blank"}.
6. [Cavs: An Efficient Runtime System for Dynamic Neural Networks](https://www.usenix.org/system/files/conference/atc18/atc18-xu-shizhen.pdf){:target="\_blank"}.
7. [Toward Understanding the Impact of Staleness in Distributed Machine Learning](https://arxiv.org/abs/1810.03264){:target="\_blank"}.
8. [On-the-fly Operation Batching in Dynamic Computation Graphs](https://arxiv.org/abs/1705.07860){:target="\_blank"}.

***

#### Machine Learning on/with Graphs

**Contact person:** [Hao Zhang](http://www.cs.cmu.edu/~hzhang2/){:target="\_blank"}

Machine learning on graphs is an important and ubiquitous task with applications ranging from drug design to friendship recommendation in social networks. The primary challenge in this domain is finding a way to represent, or encode, graph structure so that it can be easily exploited by machine learning models. Traditionally, machine learning approaches relied on user-defined heuristics to extract features encoding structural information about a graph (e.g., degree statistics or kernel functions). However, recent years have seen a surge in approaches that automatically learn to encode graph structure into low-dimensional embeddings, using techniques based on deep learning and nonlinear dimensionality reduction. Below are a few interesting topics that have been developed very actively in recently years and worth some explorations in the class:

- **Deep Generative Models for Graphs** [1, 2, 4]
- **Combing Graphical Models with Neural Networks** [1-5]
- **Semi-supervised Learning on Graph-structured Data** [3, 5]

**References**:

1. [Learning Deep Generative Models of Graphs](https://arxiv.org/abs/1803.03324){:target="\_blank"}.
2. [GraphRNN: Generating Realistic Graphs with Deep Auto-regressive Models](https://cs.stanford.edu/people/jure/pubs/graphrnn-icml18.pdf){:target="\_blank"}.
3. [Semi-Supervised Classification with Graph Convolutional Networks](https://arxiv.org/abs/1609.02907){:target="\_blank"}.
4. [Learning Multimodal Graph-to-graph Translation for Molecular Optimization](https://arxiv.org/pdf/1812.01070.pdf){:target="\_blank"}.
5. [Representation Learning on Graphs: Methods and Applications](https://arxiv.org/pdf/1709.05584.pdf){:target="\_blank"}.

***

#### Automated Machine Learning

**Contact person:** [Hao Zhang](http://www.cs.cmu.edu/~hzhang2/){:target="\_blank"}

The goal of AutoML is to make machine learning more accessible by automatically generating a data analysis pipeline that can include data pre-processing, feature selection, and feature engineering methods along with machine learning methods and parameter settings that are optimized for your data. Recently we have witnessed very active development toward a few directions such as hyperparameter searching, neural architecture search, etc. However, most of the existing methods only address a very small component from an end-to-end ML pipeline (from data to values), and they usually exhibit unsatisfactory efficiency and scalability.

- **Efficient Search for Better Model Architectures, Optimization Methods, or Both** [1-5, 7, 8, 9]
- **Searching for Better End-to-end ML Pipelines** [7]
- **AutoML (for) Systems** [6, 9]

**References**:

1. [ProxylessNAS: Direct Neural Architecture Search on Target Task and Hardware](https://arxiv.org/abs/1812.00332){:target="\_blank"}.
2. [AutoLoss: Learning Discrete Schedules for Alternate Optimization](https://openreview.net/pdf?id=BJgK6iA5KX){:target="\_blank"}.
3. [DARTS: Differentiable Architecture Search](https://arxiv.org/abs/1806.09055){:target="\_blank"}.
4. [Neural Optimizer Search with Reinforcement Learning](https://arxiv.org/abs/1709.07417){:target="\_blank"}.
5. [Neural Architecture Search with Bayesian Optimisation and Optimal Transport](https://arxiv.org/pdf/1802.07191.pdf){:target="\_blank"}.
6. [Ray: A Distributed Framework for Emerging AI Applications](https://www.usenix.org/system/files/osdi18-moritz.pdf){:target="\_blank"}.
7. [AutoAugment: Learning Augmentation Policies from Data](https://arxiv.org/pdf/1805.09501.pdf){:target="\_blank"}.
8. [MnasNet: Platform-Aware Neural Architecture Search for Mobile](https://arxiv.org/abs/1807.11626){:target="\_blank"}.
9. [Device Placement Optimization with Reinforcement Learning](https://arxiv.org/abs/1706.04972){:target="\_blank"}.
