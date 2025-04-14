+++
date = '2025-04-11T11:07:47-04:00'
draft =  false
title = 'The Pythia and Ithaca tools'
+++

The [Pythia](https://doi.org/10.18653/v1/D19-1668) and [Ithaca](https://doi.org/10.1038/s41586-022-04448-z) papers, by Assael et al., describe deep learning approaches to deciphering epigraphic data.

<!--more-->

I want to focus on the _methods_ used in the papers, partly because the details matter, and can help direct my own research. Because the Pythia paper is more recent, I will focus on it.

## Preprocessing

The Pythia system uses the Packard Humanities Institute (PHI) [corpus of Greek epigraphic data](https://inscriptions.packhum.org/). The researchers do the following normalization:

1. Remove all diacritics and case-normalize (convert to lowercase)
2. Use reconstructed letters as present in the corpus
3. Use `-` for still unknown letters -- although it looks more like they space separate the unknown characters.
4. Seem to remove some characters (like `:` ? in the example below)

Example [Raw and processed inscription](https://www.nature.com/articles/s41586-022-04448-z/figures/4) copied from the Ithaca paper:

![Reconstructed epigraph](41586_2022_4448_Fig4_ESM.webp)

Note: **This is still a work in progress**

## Bibliography

1. Assael, Y., Sommerschield, Th, Prag, J., 2019. Restoring ancient text using deep learning:
   a case study on Greek epigraphy. In: Proceedings of the 2019 Conference on
   Empirical Methods in Natural Language Processing and the 9th International Joint
   Conference on Natural Language Processing. Hong Kong, China, November 3–7,
   Association for Computational Linguistics, Hong Kong, pp. 6368–6375.
   https://doi.org/10.18653/v1/D19-1668.

2. Assael, Y., Sommerschield, Th, Shillingford, B., Bordbar, M., Pavlopoulos, J.,
   Chatzipanagiotou, M., Androutsopoulos, I., Prag, J., de Freitas, N., 2020. Restoring
   and attributing ancient texts using deep neural networks. Nature 603, 280–283.
   https://doi.org/10.1038/s41586-022-04448-z.
