---
layout: single
author_profile: true
permalink: /pubmed_class/
title: Textmining fun with Pubmed II - The Journal Strikes Back
description: Tailoring language to journals as easy as 1, 10, 100
---

# Introduction

One day, your boss goes through your research report and says good, _"let's draft this up into a manuscript and submit it to a high impact journal"_. 

Is there a way to tailor the language of the manuscript in such a way that it matches up to the language used in high impact journals, and if we were able to do so, would it improve the chance of the paper making it through? Obviously, even if we match it up, but submit gibberish, reviewers will just set it aflame. However, getting it past the editor and to the review process improves your chance of acceptance. =) 

The first idea would be to feed it into a neural net, but I don't want quite to tackle that yet (because of computational limits). I can revist this in a later project. I would like to try and do this just by treating this as a multi-class classification problem with a handful of higher impact and lower impact journals. 

Let's see if certain words are used together more often than not, or if a certain sentiment is associated with the paper. Again, this will be a tongue-in-cheek text-mining analysis, with slightly more sophisticated text mining techniques. 

{% include toc %}

# Methods
## Dataset 
WIP

- 9 journals: Scientific Reports, PLoS One, Nature, Nature Communications, Cell, Cell Reports, Science, Lancet, New England Journal of Medicine
- Pull 1,000 abstracts from each of the 9 journals between 2000 to 2017
- Pull 1,000 abstracts from each of the 9 journals between 2000 to 2017 but use 'cancer' as a keyword 
- Fewer abstracts because not all journals will have a ton of papers (looking at your PLoS One and Scientific Reports)

## Parsing 
The syuzhet R package was used to perform NRC sentiment analysis on the text of each abstract. Sentiment values were retained as features for downstream analyses.

The tm R package was used to clean up the title and abstract text, remove stopwords, extract stem words, before converting word frequencies to 'term frequency-inverse document frequency' (TF-IDF). Sparse terms that occured in less than 5% of abstracts or less than 1% of titles were dropped. Title and abstract TF-IDF were extracted separately, and are used separately as features. 

## Model fitting

# Results
## Summary stats

# Discussion
