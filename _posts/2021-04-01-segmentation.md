---
title: Segmentation
author: Stav Klein
date: 2021-04-03
category: morphology
layout: post
---

> Last Modified: 03/04/2021

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

	FORM		LEMMA		POS		FEATS
	אצל		אצל		ADP 	_
	נו		הוא		PRON	Person=1|Num=Plur.|Gender=M,F
 
 Note that for forms like "איתו" (with him) the lemma of the preposition differs from the form, and the lemma for all the pronouns is always 3rd.sg.masc.

    FORM		LEMMA
    אית		עם
    ו		הוא

> **Decision**: Separate the inflection from the "stem" (the word stem means different things to different people, so you may call this substring whatever you like)

### Inflected verbs
Generally, this principle also holds for verbs, but is more fine-grained as verbs inflect in many ways (voice, tense, binyan, person, number and gender). So for example the verb ראיתי is segmented as follows:

    FORM		LEMMA		POS		FEATS
    ראיתי		ראה		VERB
    ראי		_		_		Voice=Act|Tense=Past|Binyan=Paal|Root=ראה
    תי		_		_		Person=1|Number=Sing.|Gender=M,F


Remember we do the actual segmentation in the lines under the full (unsegmented) token. We want to reflect the fact that the "morphological load" is split unevenly between the stem and the suffix, and we want to be as accurate as possible in stating which part carries which morphological features. Yet, in order to comply with UD standards we must assign each token a lemma, which is problematic in the cases of verb conjugations.

> **Decision**: Specify the lemma ONLY on the full verb form and leave `FEATS` empty. For the little segments the lemma is _ (underscore) and the features are according to the segment's content.

We separate **where possible** and for each segment we specify only those features that this segment contributes, for example - ישלחו

    FORM		LEMMA		POS		FEATS
    ישלחו		שלח		VERB
    י		_				Tense=Fut.|Person=3		
    שלח		_				Voice=Act.|Binyan=Paal|Root=שלח
    ו		_				Number=Pl.|Gender=M,F


Note that in this example the verb is out of context so the appropriate gender is `M, F` but in a real context the gender will be clear and should be stated unambiguously.
 
What must be specified for each type of word in the `FEATS` column can be found in the `Morphological Features` page.

### The notorious accusative marker
Inflected accusative marker (את) is analyzed as follows:

    FORM	LEMMA	POS
    אות 		את		ADP
    נו		הוא		PRON

Note that only in uninflected form את appears without the infix.


### Genitive nouns
Forms like ספרו (his book), כלבה (her dog) etc. are **traditionally** segmented as:

    ספר
    _של_
    _הוא_

> **Decision**: We will NOT follow this tradition (for the reasons stated above)

Instead, we will follow our decision to segment only the surface form and keep the underlying morphology in the `FEATS`section (while maintaining a 1:1 mapping with the traditional form). Therefore, the segmentation will go as follows:

    FORM		POS		FEATS
    כלב		NOUN		Gender=Masc.|Number=Sing.
    ה		PRON		Gender=Fem.|Number=Sing.|Poss=Yes



