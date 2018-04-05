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
### Citations
To begin the author search, a set of 1,000 random papers on breast cancer were retrieved between the 2007 and 2017. After removing papers with 0 citations, I retrieved _all_ papers for each author with at least 3 papers in the initial search.   
In total, 45,623 papers were retrieved. Unlike the previous project that sampled random papers. It appears that breast cancer papers from authors that publish regularly tend to be well-cited (Figure 1). 
{% include figure image_path="/assets/images/pub_net/2018-03-29_pubnet_citations__cdf.png" alt="Figure 1. Cumulative distribution of citations in retrieved papers." caption="**Figure 1**. Cumulative distribution of citations in retrieved breast cancer papers published between 2007-2017" %}
Only 16.6% (7,618/45,623) of the retrieved papers have not been cited. Of those papers, the journals with the greatest number of uncited breast cancer papers include Breast Cancer Research and Treatment, Oncotarget, and PLoS One. Oncotarget being a bit more frequent that POne was surprising to me, but it does confirm some of my suspicions. 
{% include figure image_path="/assets/images/pub_net/2018-04-02_uncited_papers.png" alt="Figure 2. Journal with greatest number of uncited breast cancer papers (2007-2017)." caption="**Figure 2**. Top ten journals with the greatest number of retrieved and uncited breast cancer papers from 2007 to 2017." %}
Let's take a closer look at what's going on at the median. It appears that at the 50% mark, we have papers with 4 citations (Figure 1). In other words, in breast cancer research, you only need more than 4 citations to be officially ahead of the pack. This contrasts heavily with the median of 2 citations for random subset of papers. Thus, breast cancer papers are generally more cited compared to the average paper. 
On the other end of the spectrum, what are the top 1% most well-cited papers? JCO, Nature, Nature Genetics, Cell, and Cancer Research. As expected, we see many of the top tier journals, but we also have JCO and cancer research, which have lower impact factors. 
{% include figure image_path="/assets/images/pub_net/2018-04-02_most_cite_multi.png" alt="Figure 3. Journal with greatest number of uncited breast cancer papers (2007-2017)." caption="**Figure 3**. Top ten journals with the greatest number of highly cited breast cancer papers (top 1%) from 2007 to 2017. Left subpanel shows absolute count, middle panel shows percent of all retrieved papers from that journal, and rightmost shows significance as calculated using a hypergeometric test." %}
Next, we wanted to get a better idea of the overrepresentation of the journals by calculating percent of retrieved papers amongst the journals that are highly cited. Here, high impact journals clearly dominate: Cell, Nature, NatGen, and NEJM. Cell had the highest percentage (25/49; 51%), but Nature has more in terms of absolute counts (36/77; 46.8%). Out of the 10 journals, all but Breast Cancer Research were significantly enriched for highly cited papers (Q < 0.05; hypergeometric test). 
The last thing I wanted to check is to see if a relationship exists between the number of authors and number of citations. Previously, I showed that the number of authors can be used as a predictor for citations, but a univariate relationship does not appear to exist here (Figure 4). Although correlation was significant (P < 0.01), the Rho was low (0.15) and may be the result of the sheer number of papers. 
{% include figure image_path="/assets/images/pub_net/2018-04-03_pubnet_citation_authors.png" alt="Figure 5. Number of citations versus number of authors in retrieved breast cancer papers published (2007-2017)." caption="**Figure 5**. Number of citations versus number of authors in retrieved breast cancer papers published (2007-2017). Boxplot at top and right show distribution of citations and author counts respectively." %} 

### Authors and Publications
In total, I ended up with 198,187 authors, but I really don't want to make a graph with 200k nodes. Where should I cut it off? 
{% include figure image_path="/assets/images/pub_net/2018-04-03_pubnet_pubs_cdf.png" alt="Figure 5. Cumulative distribution of authors by number of breast cancer papers published (2007-2017)." caption="**Figure 5**. Cumulative distribution of authors by number of breast cancer papers published (2007-2017)." %} 
I want to cut it off at 10 papers, which just happens to be at an awkward top 3.7th percentile. My reasoning is if you are in academia for the past 10 years, and you average one paper a year, that is not very productive. If you are a young researcher and you are pretty productive, you will easily hit 10 papers. However, if you are just passing through the revolving door of academia, then you probably will not hit 10 papers in the field within 10 years. Thus, I can keep the top 3.7% (7k authors) and have my network be cleaner to look at. 
I also eliminate coauthor relationships that are smaller than 20. Again, this seems pretty arbitrary but consider the number of people that tend to show up in your papers. If you are coauthors with someone more than twice a year for 10 years, you probably work together or at least closely. Furthermore, this is really to improve the network visualization. 

### Network Viz Time
Let's take a quick look at subnetwork sizes (Figure 6). Immediately, you can see there are a ton of small networks and one giant network consisting of ~4200 authors. 
{% include figure image_path="/assets/images/pub_net/2018-04-03_subnetwork_sizes.png" alt="Figure 6. Number of subnetworks at various sizes." caption="**Figure 6**. Number of subnetworks at various sizes." %} 

[Subgraph 1](https://huangchv.github.io/coauthors_sg1/)
[Large subgraphs minus SG1](https://huangchv.github.io/coauthors_not_sg1/)
