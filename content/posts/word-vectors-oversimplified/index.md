+++
date = '2025-04-23T12:52:35-04:00'
draft = false
title = 'Word Vectors Oversimplified'
+++

_This is a [reposting of an article](https://willwhim.wpengine.com/2015/05/12/word-vectors-machine-learning-oversimplified/) I wrote in May, 2015._

Word vectors have become increasingly important in as features in machine learning models for natural language processing. The idea is to represent a word in some multidimensional space (the vector) in which words which are “similar” are similar in that space. Typically, one hopes that word vectors will provide some kind of semantic similarity. A typical party trick is to use word vectors to solve word analogy problems; e.g., king is to queen as man is to ? And hope that answer is woman.

Word vectors are often created using distributional data. That is, words that co-occur tend to be more similar to words that don’t co-occur. So, a typical second step is to create a co-occurrence matrix of probabilities among words. Second step? Yes, because the first step (as usual) is to break things up into “words” (tokenization). Different tokenization schemes will create different models, of course, and there’s no particular reason to limit the tokens to dictionary words.

So, one way to think about a word vector of k feature weights is that the dot product of the word vectors of two words should be their co-occurrence probability. So this becomes the objective function to create a learned model; details are in the [GloVe paper](https://nlp.stanford.edu/pubs/glove.pdf) (pdf file).

These models can be computationally expensive to create. Fortunately, Stanford and Google have provided word vector models based on a variety of corpora (and various hyperparameters, such as the number of dimensions). Stanford provides [word vectors](http://nlp.stanford.edu/projects/glove/) trained on Wikipedia plus the [Gigaword](https://catalog.ldc.upenn.edu/LDC2011T07) corpus, [Common Crawl](https://commoncrawl.org/), and two billion Twitter tweets at various dimension sizes. Google’s [word2vec](https://code.google.com/p/word2vec/) system provides word vectors trained on 100 billion words from Google News, and anoother set created from Freebase entities.

## Example

I’m from Michigan, and my wife and I often noted the similarity of Michigan to Wisconsin. The Detroit of Wisconsin is Milwaukee (largest, industrial cities); the Ann Arbor of Wisconsin is Madison (liberal, best college towns), and so on. But the Lansing of Wisconsin is also Madison (capital cities).

Radim Řehůřek created a fun little app[^1] that uses the Google word2vect on the backend to do word analogies.

Here’s the word2vec results for the Michigan/Wisconsin comparisons:

- Michigan is to Detroit as Wisconsin is to Milwaukee. (yay!)
- Michigan is to Ann Arbor as Wisconsin is to La Crosse. (boo!)
- Michigan is to Lansing as Wisconsin is to La Crosse. (boo!)
- Michigan is to Grand Rapids as Wisconsin is to La Crosse. (boo!)

Ok, it seems to have a thing for La Cross. So, it’s not magic. But the fact that it’s producing somewhat similar cities (and not random words) is promising.

[^1]: Alas, no longer working.
