+++
date = '2025-04-23T09:34:01-04:00'
draft = false
title = 'Deep Learning'
+++

In this brief article, I will discuss an overview article from 2015 -- a long time ago in research years -- in _Nature_ called [_Deep Learning_](https://www.nature.com/articles/nature14539), essentially the underlying architecture of what is called machine learning these days. One of the co-authors is Geoffrey Hinton, who was awarded a Nobel Prize for his work over the decades on neural networks (Cool fact: Hinton is the great-great-grandson of George Boole, after whom boolean logic is named).

But it would be better to read the [article](https://www.nature.com/articles/nature14539) itself, which is relatively well-written.

I think the key insights of this paper are severalfold.

## General > Specific

General architectures are counter-intuitively better than specific architectures for machine learning. One would expect that bespoke engineering would be better at solving tasks in a domain: for example, one would expect providing a machine with paradigm charts of Greek verbs would better than not providing them. But, in the end, such systems with hand-built features are difficult to create, have sharp failure points, and eventually are overwhelmed by literally exponential improvements in the processing power of computers.

The give the example of creating a classifier that can distinguish between white wolves and Samoyeds; two images of the same Samoyed might look radically different due to lighting, and an image of a white wolf and a Samoyed might look very similar. They write:

> The conventional option is
> to hand design good feature extractors, which requires a consider-
> able amount of engineering skill and domain expertise. But this can
> all be avoided if good features can be learned automatically using a
> general-purpose learning procedure. This is the key advantage of
> deep learning.

This is also true in modeling language:

> The issue of representation lies at the heart of the debate between
> the logic-inspired and the neural-network-inspired paradigms for
> cognition. In the logic-inspired paradigm, an instance of a symbol is
> something for which the only property is that it is either identical or
> non-identical to other symbol instances. It has no internal structure
> that is relevant to its use; and to reason with symbols, they must be
> bound to the variables in judiciously chosen rules of inference. By
> contrast, neural networks just use big activity vectors, big weight
> matrices and scalar non-linearities to perform the type of fast ‘intuitive’
> inference that underpins effortless commonsense reasoning.

## Much more > More

Deep learning succeeds in part because much more data is used, and many more detectors and layers are used than previous machine learning models could use. One of the disadvantages of neural networks is their tendency to get stuck in "local minima," but with lots of very shallow local minima, systems tend not to get caught. An analogy is the difference between walking in the forest and getting caught in one deep ravine versus walking in a forest with many small depressions.

## Cheaper > Expensive

Architectural advances have made it possible to train models more efficiently, and these can accelerate the "much more > more" quality of networks. For example, the article mentions GPUs and the use of rectified linear units (ReLUs). In general, improvements in neural network architecture tend to focus on doing less with more: smaller amounts of computation on ever more data.

> Recent ... architectures have 10 to 20 layers of ReLUs, hundreds of
> millions of weights, and billions of connections between
> units. Whereas training such large networks could have taken weeks
> only two years ago, progress in hardware, software and algorithm
> parallelization have reduced training times to a few hours.

## Standard datasets and metrics > Bespoke datasets and metrics

Somewhat implied in the article is the importance of creating standard datasets and metrics. For example, the mention the ImageNet competition, which contained about a million images defined in about a thousand classes. This allowed the field to have common data on which to train and evaluate systems, and it was easy to acknowledge that convolution nets were much better than competing systems.

I have not really discussed many of the specific parts of deep learning here, such as the structure of deep learning networks, gradient descent, convolutional networks, or long short-term networks (LTSMs). The paper does a pretty good job of this.
