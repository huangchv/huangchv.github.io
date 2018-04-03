---
date: "March 29, 2018"
layout: postrmd
author_profile: true
permalink: /coauthors/
title: Network Analysis of Breast Cancer Co-Authorships
description: Who should I try not to offend at conferences?
htmlwidgets: TRUE
---

# Introduction

Imagine going to a big conference as a young researcher. There are so many people. You have to network and foster relationships, but who should you go shmooze with? Or if you are like me, who should you avoid offending? If you inadvertantly piss off a senior PI who's connected to everyone in the field 
While we are at it, we can look at the field and see if we can answer some more questions.

For this project, I want to focus on a specific field: _Breast Cancer_
Why? Tons of paper and it's one of the most well-funded field. 

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
{% include figure image_path="/assets/images/pubmed/2018-03-29_pubnet_citations__cdf.png" alt="Figure 1. Cumulative distribution of citations in retrieved papers." caption="**Figure 1**. Cumulative distribution of citations in retrieved breast cancer papers published between 2007-2017" %}
Only 16.6% of the retrieved papers have not been cited. Of those papers, the journals with the greatest number of uncited breast cancer papers include Breast Cancer research and treatment, Oncotarget, and PLoS One. Oncotarget being a bit more frequent that POne was surprising to me, but it does confirm some of my suspicions. 
{% include figure image_path="/assets/images/pubmed/2018-03-29_pubnet_citations__cdf.png" alt="Figure 2. Journal with greatest number of uncited breast cancer papers (2007-2017)." caption="**Figure 2**. Top ten journals with the greatest number of retrieved and uncited breast cancer papers from 2007 to 2017." %}
Let's take a closer look at what's going on at the median. It appears that at the 50% mark, we have papers with 4 citations. In other words, in breast cancer research, you only need more than 4 citations to be officially ahead of the pack. This contrasts heavily with the median of 2 citations for random subset of papers. Thus, breast cancer papers  are generally more cited compared to the average paper. 
On the other end of the spectrum, let's look at what journals the top 1% most well-cited papers end up. JCO, Nature, Nature Genetics, Cell, Cancer Research. As expected, we see many of the top tier journals, but we also have JCO and cancer research, which have lower impact factors. 










# Discussion


*A journey of a thousand miles begins with a single step.*  