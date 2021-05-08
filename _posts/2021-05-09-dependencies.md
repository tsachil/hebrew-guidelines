---
title: Dependencies
author: Stav Klein
date: 2021-05-09
category: Syntax
layout: post
---

> Last Modified: 05/05/2021


## References
[UD Relations][1] - **At the moment**, we do not use every relation listed on this page, but we can (and should) consult it if needed.

## General Principles
Annotating the syntactic relations of a word consists of two parts - First, Determine what is the `HEAD` of the word, which is either a token ID or 0 (more on that under `root`), then determine what is the relation to the `HEAD`. Normally we would want to choose from the [universal relations][1], but there will be cases in which we'll have to define a language-specific **subtype** of one of the relations. [Here][2] are language-specific relations that other langauges use. If you want to suggest a subtype, please look for it in other languages first. Subtypes that are very well motivated (at least in the sense that many other languages need them as well) are always preferred over re-inventing the wheel. Also keep in mind that the old treebank defined several subtypes - it's not mandatory that we use those as well.

## Comments on specific relations
The relations in the [general relations page][1] are well-organized and most of them are also pretty straightforward and contain nice examples, so it is strongly recommended to consult the general website. For those not familiar with the idea of annotating syntax in the form of relations, I suggest to read first the [general principles for annotating syntax][3]. Henceforth, this syntax page will only address relations and issues that are either a) new or particularly confusing for newcomers, b) Hebrew-specific or c) came up in the discussion and require more elaboration.


### `root`
The root node receives the value `0` (zero) under `HEAD`, essentially that means the root has no head (since no other token is indexed 0). The root node denotes the main predicate in the sentence, therefore there should always be only one root per sentence. This sentence can be very long and contain subordinated clauses and what not - and still there will be only one root, which is the main predicate. The examples in the UD website sometimes show sentences that start with the token `'ROOT'`, this token is added automatically with the index 0 and is the "artificial" `HEAD` for the root - you do not have to worry about that nor add this token by yourselves (this is a fully automated process).

### `compound` and `nmod`
In Hebrew we have two constructions of two nominals: compounds (הרכב) and smixut (סמיכות). The main difference between them is that smixut are compositional (e.g. שדה קוצים) while compounds are not (e.g. בית ספר). In both cases the token that is the `HEAD` of the construction will have a dependent with the relation `nmod` for smixut or `compound` for compounds. <br>
It's important to state here that Hebrew also exhibits a unique construction of nouns that modify adjectives, such as in: יפה נפש, טוב לב, אחרון המוהיקנים, etc. We will analyze those constructions as compounds with the adjective as the `HEAD` (as these are mostly fixed phrases and this construction is generally non-productive in modern Hebrew)


### `obl` vs. `obl:arg`
The UD scheme uses the relation `obl` to denote both arguments and adjuncts, which is not not consistent with our analysis (reminder: in our analysis `Oblique` is the value for the `Case` feature for necessary complements of a predicate). To be consistent with this analysis we will mark the `HEAD` of the oblique complement as the dependent of the predicate with the relation `obl:arg`. For a detailed description see [here][4].


### `aux` vs. `cop`
Similarly to their corresponding features, `aux` and `cop` define a relation between tokens that bear the POS tags `AUX` and `PRON` to their predicate (it's usually the main predicate in the sentence, but it doesn't have to be). The predicate is the `HEAD` and the auxiliary/copular tokens are the dependents. Note that `aux` cannot have dependents (in other words, it can't be the `HEAD` for another token).


[1]: https://universaldependencies.org/u/dep/index.html
[2]: https://universaldependencies.org/ext-dep-index.html
[3]: https://universaldependencies.org/u/overview/syntax.html
[4]: https://universaldependencies.org/u/dep/obl-arg.html
