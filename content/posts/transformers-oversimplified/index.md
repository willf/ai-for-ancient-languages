+++
date = '2025-05-01T19:22:28-04:00'
draft = false
title = 'Transformers (Way) Oversimplified'
+++

The 2017 paper [_Attention is all you need_](https://arxiv.org/pdf/1706.03762), was revolutionary for machine learning for sequential data, in particular language data. In some ways, the main idea behind the paper is simple. Previous ML models processed each item in a sequence sequentially, with perhaps a small amount of context. This paper laid the groundwork for _transformer models_. The abstract lays this out:

> The dominant sequence transduction models are based on complex recurrent or
> convolutional neural networks that include an encoder and a decoder. The best
> performing models also connect the encoder and decoder through an attention
> mechanism. We propose a new simple network architecture, the Transformer,
> based solely on attention mechanisms, dispensing with recurrence and convolutions
> entirely. Experiments on two machine translation tasks show these models to
> be superior in quality while being more parallelizable and requiring significantly
> less time to train. Our model achieves 28.4 BLEU[^1] on the WMT 2014
> English-to-German translation task, improving over the existing best results, including
> ensembles, by over 2 BLEU. On the WMT 2014 English-to-French translation task,
> our model establishes a new single-model state-of-the-art BLEU score of 41.8 after
> training for 3.5 days on eight GPUs, a small fraction of the training costs of the
> best models from the literature. We show that the Transformer generalizes well to
> other tasks by applying it successfully to English constituency parsing both with
> large and limited training data.

So, the major claims of this paper are:

1. The only thing needed is the _attention_ model ("Attention is all you need.") because this simpler model achieves better results than more complicated models.
2. This simpler model is cheaper to train.

This has been borne out in subsequent research.

So, the basic question to answer: What is an attention model?

Language data is essentially sequential in nature: one damn thing after another. A first step in language processing to to break the text into words, or more specifically tokens. These tokens have a natural order: each token could be assigned an index number corresponding to its position in the stream of tokens. For example, "the cat sat on the mat" might be broken down into the tokens _the<sub>1</sub>_, _cat<sub>2</sub>_, _sat<sub>3</sub>_, _on<sub>4</sub>_, _the<sub>5</sub>_, and _mat<sub>6</sub>_. Most previous ML models ignored most of that sequential context, although they might look at very local contexts[^2].

But attention models pay attention to those positions. This requires more memory and processing. For example, a particular architecture might have a window of 1024 tokens, each with an index, and each numbered token conditioning or conditioned by any other token in that window.

Essentially, a particular model learns to _pay attention_ to (assign higher weights to) different parts of longer sequences.

Consider a "fill in the gap" task where the model is expected to fill in the gap in sentences like:

> 1. The astronomer saw the moon with a \_\_\_\_.
> 2. The chemist saw the atom with a \_\_\_\_.

We, as humans, pay attention to the subject of these sentences (_astronomer_, _chemist_) and use their semantics to help us predict what is likely to fill the blanks (_telescope_, perhaps, for the astronomer and _microscope_, perhaps, for the chemist).

This is more than hand-waving, it's hand-waving from very far away, but to do any more we'd have to do some math.

So, there is a lot of math, but it's relatively simple and straight-forward, at least compared to other architectures (the paper mentions recurrent and convolutional architectures) which lead to the speed-up in training.

[^1]: BLEU scores: "BLEU (Bilingual Evaluation Understudy) is an algorithm for evaluating the quality of text which has been machine-translated from one natural language to another." [Reference](https://huggingface.co/spaces/evaluate-metric/bleu). For what it's worth, the score runs from 0.0 to 1.0 (or 0 to 100) where higher is better, and 1.0 (or 100) is perfect.
[^2]: For example, _n_-grams, where is an 'n-gram' is a series of _n_ words or tokens, typically five tokens or fewer. Given the general distributional nature of words, larger n-grams sizes tend to create very sparse data. For example, if there are 10,000 words in the languages vocabulary (a low number), there are 10,000<sup>5</sup>, or 10,000,000,000,000,000,000 distinct n-grams. But it's unlikely that any particular n-gram ("blubber zoom the delightful happily") actually occurs.
