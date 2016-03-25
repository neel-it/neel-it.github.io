---
layout: default
title: NEEL
---
# Task Description

Tweets represent a great wealth of information useful to understand recent trends and user behaviors in real-time.
Usually, natural language processing techniques would be applied to such pieces of information in order to make them machine-understandable.
Named Entity rEcongition and Linking (NEEL) is a particularly useful technique aiming at assigning semantics to a text.
However, due to the noisy nature and shortness of tweets, this technique is more challenging in this context than elsewhere.
International initiatives provide evaluation frameworks for this task, e.g. the [Making Sense of Microposts workshop](http://microposts2016.seas.upenn.edu/challenge.html), currently re-organizing the NEEL challenge for the fourth time, or the [W-NUT workshop](https://noisy-text.github.io/ner-shared-task.html) at ACL 2015, but the focus is always and strictly on the English language.
We foresee an opportunity to (i) encourage the development of language independent tools for for Named Entity Recognition (NER) and Linking (NEL) systems and (ii) establish an evaluation framework for the Italian community.
NEEL-IT at EVALITA has the vision to establish itself as a reference evaluation framework  in the context of Italian tweets.


## Annotation
NEEL-IT will follow a setting similar to NEEL challenge for English Micropost on Twitter.
The task consists of annotating each named entity mention (like people, locations, organizations, and products) in a text by linking it to a knowledge base (DBpedia).
In the annotation process, a named entity is a string in the tweet representing a proper noun that:
1) belongs to one of the categories specified in a taxonomy and/or
2) can be linked to a DBpedia concept.
This means that some concepts have a NIL DBpedia reference: these concepts belong to one of the categories but they have no corresponding concept in DBpedia.
The taxonomy is defined by the following categories: Thing, Event, Character, Location, Organization, Person and Product.

From the annotation are excluded the preceding article (like il, lo, la, etc.) and any other prefix (e.g. Dott., Prof.) or post-posed modifier.

Each participant is asked to produce an annotation file with multiple lines, one for each annotation.
A line is a tab separated sequence of `tweet id`, `start offset`, `end offset`, `linked concept in DBpedia`, and `category`.
For example, given the tweet:

    Chameleon Launcher in arrivo anche per smartphone: video beta privata su Galaxy Note 2 e
    Nexus 4: Chameleon Laun...

the annotation should produce the following output:

    288976367238934528	0	18	NIL	Product
    288976367238934528	73	86	http://it.dbpedia.org/resource/Samsung_Galaxy_Note_II/ Product
    288976367238934528	89	96	http://it.dbpedia.org/resource/Nexus_4	Product

The annotation should also link Twitter mentions (`@`) and tags (`#`) that refer to a named entities, like:
otation is expected:

    288380466413854721	1	16 	http://it.dbpedia.org/resource/Piazzapulita	Product
    288380466413854721	41	50	http://it.dbpedia.org/resource/Renata_Polverini	Person

## Evaluation

Participants are allowed to submit up to 3 runs of their system as TSV files. An example of the submission format will be released with the development set. We encourage participants to make available their system to the community to facilitate reuse.

We will use the TAC KBP scorer (https://github.com/wikilinks/neleval/wiki/Evaluation) to evaluate the results and in particular we will focus on:

* **tagging** strong\_typed\_mention\_match (check entity name boundary and type)
* **linking**     strong\_link\_match
* **clustering**  mention\_ceaf (NIL detection)

The *strong_typed_mention_match* evaluates the micro average F-1 score for all annotations considering the mention boundaries and their types.
The *strong_link_match* is the micro average F-1 score for annotations considering the correct link for each mention. The *mention_ceaf* (Constrained Entity-Alignment F-measure) [5] is a clustering metric developed to evaluate clusters of annotations.
It evaluates the F-1 score for both NIL and non-NIL annotations in a set of mentions.
The final score will be computed as follows:

    score = 0.4 ∗ mention_ceaf + 0.3 ∗ strong_typed_mention_match + 0.3 ∗ strong_link_match

We will use the official scorer proposed for the [TAC KBP task](ttps://github.com/wikilinks/neleval/wiki/Evaluation).



---
## References

+ Giuseppe Rizzo, Amparo Elizabeth Cano Basave, Bianca Pereira, and Andrea Varga. Making sense of microposts (#microposts2015) named entity recognition and linking (NEEL) challenge. In _Making Sense of Microposts_, pages 44–53, 2015.

+ Amparo Elizabeth Cano Basave, Giuseppe Rizzo, Andrea Varga, Matthew Rowe, Milan Stankovic, and Aba-Sah Dadzie. Making sense of microposts (#microposts2014) named entity extraction & linking challenge. In _Making Sense of Microposts_, pages 54–60, 2014.

+ Xiaoqiang Luo. On coreference resolution performance metrics. *HLT/EMNLP’05*, 2005
