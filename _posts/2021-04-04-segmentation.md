---
title: Segmentation
author: Stav Klein
date: 2021-04-03
category: morphology
layout: post
---
Segmentation is the very first stage in the annotation process. Before you do anything else, make sure the whole sentence is segmented properly.

## How to Segment
We get space-delimited tokens and we want to split them according to their **concatenative** morphemes. That is, we don't account for root and template morphemes at this stage (we will deal with them later).
Example: the word "והכלב", is split into

    ו
    ה
    כלב

## Special Cases
The example before is pretty straightforward, of course Hebrew morphology exhibits many interesting ( = beautiful, challenging) phenomena that require special treatment.

### The covert definite article
Take a word like "בבית" which is ambiguous (can be read as either definite or indefinite, depending on the context). The old guidelines state that there are two possible segmentations:

    ב
    בית
   
or
  
    ב
    _ה_
    בית

where the second segmentation reflects the definite reading (with the definite article stated as covert on the surface form).

> **Decision:** We will use the same segmentation for both definite and indefinite readings

We will address the embedded definiteness of the preposition in the morphological features column (see the guidelines for morphological features annotation). The motivation behind this decision (and generally throughout the guidelines) is two-fold:

 1. Minimize potential errors in segmentation
 2. Keep a one-to-one mapping between the segmentation in new guidelines and the old guidelines

### Inflected prepositions
Examples of inflected prepositions: אצלי, ממך, לנו, שלו, לידה etc.
These prepositions get segmented linearly, like before, where the pronominal features are specified on the pronominal suffix. e.g. "אצלנו"

    FORM	LEMMA 	POS		FEATS
     אצל		אצל		ADP 	_
	  נו		הוא		PRON	Person=1|Num=Plur.|Gender=M,F
 

Note that for forms like "איתו" (with him) the lemma of the preposition differs from the form, and the lemma for all the pronouns is always 3rd.sg.masc.
 
	FORM	LEMMA
    אית		עם
    ו		הוא

### The notorious accusative marker
Inflected accusative marker (את) is analyzed as follows:

    FORM	LEMMA	POS
    אות		את		ADP
    נו		הוא		PRON

Note that only in uninflected form את appears without the infix.

### Genitive nouns

