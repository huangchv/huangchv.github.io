---
layout: single
author_profile: true
permalink: /coauthors/
title: Coauthor Network Viz
description: Who should I try not to offend at conferences?
---

# Introduction

If you are a scientist or a researcher, you may have published your research in a peer-reviewed journal. Publishing papers can serve many purposes, one of which may include disseminating your findings to the community so others can build upon it. However, we are only human, and we take pride in our work. We want to be successful.

{% include toc %}

# Methods
## Dataset 
Data was pulled from from the PubMed API using the RISmed R package. Query to API was `"journal article"[Publication Type] AND "english"[Language] AND hasabstract[text]` as it will ideally yield English research papers with an abstract. We extracted 5,000 abstracts for each year from 2010 to 2015. To avoid pulling papers in order, which will produce swathes of papers from the same journal, the function queries for 10x the number of requested abstracts, and then randomly selects the requested number from the returned PMIDs. From each abstract object, we extracted title, abstract, author's list, number of citations, month submitted, and month published. Abstracts without text in the actual abstract were dropped.

## Parsing 
<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRvszMJ05uAPvGILSyfMU-bORpcadUyCzg1PKEdtdEWhXgx3XpFLHl5k3LpRWyuiBBAo3M0zG5z203-/pubchart?oid=170923216&amp;format=interactive"></iframe>
## Network characterization

# Results
## Summary stats

### Are there journals that are over-represented?

### Do manuscript submissions wax and wane with the seasons? 

### Modeling and Feature Importance



{% include figure image_path="/assets/images/pubmed/anger_anticipation_cloud.png" alt="Figure 8. Anger and Anticipation Word Clouds" caption="**Figure 8**. Words associated with *anger* and *anticipation* according to the National Research Council (of Canada :))." %}


# Discussion


*A journey of a thousand miles begins with a single step.*  