---
layout: single
author_profile: true
permalink: /coauthors/
title: Network Viz of Breast Cancer Co-Authorships
description: Who should I try not to offend at conferences?
htmlwidgets: TRUE
---

# Introduction

Imagine going to a big conference as a young researcher. There are so many people. You have to network and foster relationships, but who should you go shmooze with? Or if you are like me, who should you avoid offending? If you inadvertantly piss off a senior PI who's connected to everyone in the field, your academic career will probably hit some insurmountable barriers. 
While we are at it, we can look at the field and see if we can answer some more questions.

For this project, I want to focus on a specific field: _Breast Cancer_
Why? Tons of paper and it's one of the most well-funded field. Also, amazing p-values. 

Here, I will present my take on developing interpersonal relationships in academia. 

{% include toc %}

# Methods
## Dataset 
## Parsing 
## Network characterization

# Results

## Summary stats
To begin the author search, a set of 1,000 random papers on breast cancer were retrieved between the 2007 and 2017. After removing papers with 0 citations, I retrieved _all_ papers for each author with at least 3 papers in the initial search.   
In total, 45,623 papers were retrieved. Unlike the previous project that sampled random papers. It appears that breast cancer papers from authors that publish regularly tend to be well-cited (Figure 1). 
{% include figure image_path="/assets/images/pub_net/2018-03-29_pubnet_citations__cdf.png" alt="Figure 1. Cumulative distribution of citations in retrieved papers." caption="**Figure 1**. Cumulative distribution of citations in retrieved breast cancer papers published between 2007-2017" %}
Only 16.6% (7,618/45,623) of the retrieved papers have not been cited. Of those papers, the journals with the greatest number of uncited breast cancer papers include Breast Cancer Research and Treatment, Oncotarget, and PLoS One. Oncotarget being a bit more frequent that POne was surprising to me, but it does confirm some of my suspicions. 
{% include figure image_path="/assets/images/pub_net/2018-04-02_uncited_papers.png" alt="Figure 2. Journal with greatest number of uncited breast cancer papers (2007-2017)." caption="**Figure 2**. Top ten journals with the greatest number of retrieved and uncited breast cancer papers from 2007 to 2017." %}
Let's take a closer look at what's going on at the median. It appears that at the 50% mark, we have papers with 4 citations (Figure 1). In other words, in breast cancer research, you only need more than 4 citations to be officially ahead of the pack. This contrasts heavily with the median of 2 citations for random subset of papers. Thus, breast cancer papers are generally more cited compared to the average paper. 
On the other end of the spectrum, what are the top 1% most well-cited papers? JCO, Nature, Nature Genetics, Cell, and Cancer Research. As expected, we see many of the top tier journals, but we also have JCO and cancer research, which have lower impact factors. 
{% include figure image_path="/assets/images/pub_net/2018-04-02_most_cite_multi.png" alt="Figure 3. Journal with greatest number of uncited breast cancer papers (2007-2017)." caption="**Figure 3**. Top ten journals with the greatest number of highly cited breast cancer papers (top 1%) from 2007 to 2017." %}
Next, we wanted to get a better idea of the overrepresentation of the journals by calculating percent of retrieved papers amongst the journals that are highly cited. Here, high impact journals clearly dominate: Cell, Nature, NatGen, and NEJM. Out of the 10 journals, all but Breast Cancer Research were significantly enriched for highly cited papers (Q < 0.05; hypergeometric test). 








# Discussion


*A journey of a thousand miles begins with a single step.*  