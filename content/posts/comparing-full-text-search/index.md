+++
date = '2025-05-07T09:10:10-04:00'
draft = true
title = 'Comparing Full Text Search'
+++

## TLG Full Text Search

[Full text search](https://stephanus.tlg.uci.edu/Iris/demo/tsearch.jsp)

Breadth of search:

1. Full corpus
2. Works by Author

Flags:

1. Case sensitive
2. Exact match
3. Diacritic sensitive
4. Adscript as subscript
5. Wildcard

Proximity (within _n_ words)

- Near (before or after)
- Before
- After

The proximate can be _word form_, _lemma_, or _grammatical category_.

### Search Guide

The search language seems to be a subset of regular expressions; the definition is given by example.

This is from the full text search guide:

Wildcard searches are possible in both Simple and Proximity Word Index and Textual Search.

Examples of possible wildcard combinations:

- Search for ANA as part of a word: ANA
- Search for ANA as a prefix (word index)/at the start of a line (full text): ^ANA
- Search for ANA as a suffix (word index)/at the end of a line (full text): ANA$
- Search for the word ANA (word index only): ^ANA$
- Search for ANADU or ANEDU: AN[AE]DU
- Search for ANADU or ANEDU: ANADU|ANEDU
- Search for ANADU or ANEDU: (ANA|ANE)DU
- Search for A)NADU or A)NEDU: (A\)NA|A\)NE)DU
- Search for ANAD followed by anything but U: ANAD[^U]
- Search for a word consisting of ANAD, then any two letters, then U: ^ANAD..U
- Search for EDU or ANEDU: (AN)?EDU
- Search for a numeric digit: [0-9]
- Search for an Arabic numeral (a sequence of one or more digits): [0-9]+
- Search for a quotation mark Beta escape (" followed by zero or more digits): "[0-9]\*

Note: In both Word index and Textual search, special beta character such as \*()/|+ should be escaped by prefixing them with backslash ().

Input methods:

1. Greek
2. Betacode
3. Transcriptions

### Example searches

Starting from "ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον ἡδέως ζῆν."[^1]

| Search string                                               | Mutation                      | Success?                           |
| ----------------------------------------------------------- | ----------------------------- | ---------------------------------- |
| ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον ἡδέως ζῆν.         | None                          | Yes                                |
| ὅτῳ δὲ τοῦτο μὴ ὑπάρχει οὐκ ἔστι τοῦτον ἡδέως ζῆν           | remove punctuation            | yes                                |
| **ὅτωι** δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον ἡδέως ζῆν.    | adscript                      | yes (with 'adscript as subscript') |
| **ὅτω** δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον ἡδέως ζῆν.     | remove subscript              | yes                                |
| ότῳ δὲ τοῦτο μὴ υπάρχει, οὐκ ἔστι τοῦτον ηδέως ζῆν          | remove breathing              | yes                                |
| ὁτῳ δε τουτο μη ὑπαρχει, οὐκ ἐστι τουτον ἡδεως ζην          | remove accents                | yes                                |
| οτω δε τουτο μη υπαρχει ουκ εστι τουτον ηδεως ζην           | remove all                    | yes                                |
| ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, οὐκ **ἔϲτι** τοῦτον **ἡδέωϲ** ζῆν. | lunate sigma                  | yes                                |
| ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον **ἡδέωσ** ζῆν.     | σ-regularization              | yes                                |
| οτω δε τουτο μη υπαρχει ουκ εϲτι τουτον ηδεωϲ ζην           | remove all, ϲ-regularization  | yes                                |
| ὅτῳδὲτοῦτομὴὑπάρχειοὐκἔστιτοῦτονἡδέωςζῆν                    | remove spaces and punctuation | no                                 |
| **ὅτῳ ?δὲ** τοῦτο μὴ ὑπάρχει                                | space optional wildcard       | no                                 |
| οὐκ ἔστι τοῦτον **(ἡδέως\|καλῶς)** ζῆν.                     | word level alteration         | yes[^2]                            |
| ὅτῳ δὲ τοῦτο μὴ **ὑπάρχειν?**                               | optional letter               | yes[^2]                            |

## Scaife Text Search

[Text search](https://scaife.perseus.org/search/)

Breadth of search:

- Full corpus

Input methods:

- Unicode

### Search Guide

- `+` signifies AND operation
- `|` signifies OR operation
- `-` negates a single token
- `"` wraps a number of tokens to signify a phrase for searching
- `*` at the end of a term signifies a prefix query
- `(` and `)` signify precedence
- `~num` after a word signifies edit distance (fuzziness)
- `~num` after a phrase signifies slop amount

Scaife search has two types: _form_ and _lemma_ search. Form search is standard text search, lemma search searches using the base lemma. For example, in lemma search, using `"ἀρχῆ ο λογος"` as the search string returns results with substring `ἀρχῆθεν τὸν λόγον`, `ἀρχῆς ὁ λόγος`, `ἀρχὴν τοῦ λόγου`, `ἀρχὰς τοῦδε τοῦ λόγου`, etc. It will not understand `"ἀρχὴν τοῦ λόγου"` since none of these are lemmas.

Scaife does not currently implement regular expressions except for prefix search (for example `ἀρχ* + λογ*`).

Scaife does not currently implement proximity search or search based on morphological features.

### Example searches

Starting from "ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, οὐκ ἔστι τοῦτον ἡδέως ζῆν."[^3]
| Search string | Mutation | Success? |
|------------------------------------|-------------------------------|-----------------------|--|
| "ὅτῳ δὲ τοῦτο μὴ ὑπάρχει" | None | Yes |
| "**ὅτωι** δὲ τοῦτο μὴ ὑπάρχει" | adscript | yes |
| "**ὅτω** δὲ τοῦτο μὴ ὑπάρχει" | remove subscript | no |
| "ότῳ δὲ τοῦτο μὴ υπάρχει" | remove breathing | yes |
| "ὁτῳ δε τουτο μη ὑπαρχει" | remove accents | yes |
| "οτω δε τουτο μη υπαρχει" | remove accents & breathing | yes |
| οὐκ **ἔϲτι** τοῦτον **ἡδέωϲ** ζῆν. | lunate sigma | yes |
| οὐκ ἔστι τοῦτον **ἡδέωσ** ζῆν. | σ-regularization | yes |
| ουκ εϲτι τουτον ηδεωϲ ζην | remove all, ϲ-regularization | yes |
| οὐκἔστιτοῦτονἡδέωςζῆν | remove spaces and punctuation | no |
| οὐκ ἔστι τοῦτον (ἡδέως | καλῶς) ζῆν | word level alteration | yes[^2] |

[^1]:
    "Without (living prudently and justly), it is impossible for anyone to live pleasantly."
    G. Arrighetti, Epicuro. Opere, Turin: Einaudi, 1960: 119-137.
    Retrieved from [TLG](http://stephanus.tlg.uci.edu/Iris/Cite?0537:001:1380).

[^2]: System often fails to complete search with longer strings.
[^3]:
    The version of Epicurus on Scaife, [Ratae Sententiae](https://scaife.perseus.org/reader/urn:cts:greekLit:tlg0537.tlg013.1st1K-grc1:139-143/)
    Ratae Sententiae, does not have this as a complete sentence, but has some intervening, bracketed text: ὅτῳ δὲ τοῦτο μὴ ὑπάρχει, [οὐ ζῇ φρονίμως. καὶ καλῶς καὶ δικαίως ὑπάρχει] οὐκ ἔστι τοῦτον ἡδέως ζῆν. Therefore, we can't search for the whole text string directly.
