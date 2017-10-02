---
layout: single
author_profile: true
permalink: /pubmed/
title: Textmining fun with Pubmed
description: Fun is an arbitrary value between 1 and 10
---

# Introduction

If you are a scientist or a researcher, you may have published your research in a peer-reviewed journal. Publishing papers can serve many purposes, one of which may include disseminating your findings to the community so others can build upon it. However, we are only human, and we take pride in our work. We want to be successful.

So how does one go about evaluating whether their paper is successful? Easy, citations. 
The more times your paper is cited, the more _successful_. But is it possible to predict the number of citations you can get based on your abstract? 

Are there certain keywords you can use in your abstract that will immediately:
- Get you tons of citations? 
- The respect of your colleagues?
- The attention of the cute post doc in the neighbouring lab
- The Nobel prize? 

Let's find out if we can answer that first question. I don't think I can help you with the others.

Here, I will present a tongue-in-cheek analysis of citations based on text mining data from PubMed. 

{% include toc %}

# Methods
## Dataset 
Data was pulled from from the PubMed API using the RISmed R package. Query to API was `"journal article"[Publication Type] AND "english"[Language] AND hasabstract[text]` as it will ideally yield English research papers with an abstract. We extracted 5,000 abstracts for each year from 2010 to 2015. To avoid pulling papers in order, which will produce swathes of papers from the same journal, the function queries for 10x the number of requested abstracts, and then randomly selects the requested number from the returned PMIDs. From each abstract object, we extracted title, abstract, author's list, number of citations, month submitted, and month published. Abstracts without text in the actual abstract were dropped.

## Parsing 
The syuzhet R package was used to perform NRC sentiment analysis on the text of each abstract. Sentiment values were retained as features for downstream analyses.

Journal impact factors and Eigenfactors from 2017 were obtained from Thomas Reuters and placed into a lookup table. Journal names were cleaned up and parsed to match the names in the impact factor lookup data as well as possible before being matched with an impact factor and Eigenfactor. Remaining journal names that defied parsing and matching to lookup table were assigned an impact factor from a Gaussian distribution centered around 2.5 and an SD of 0.83, while an Eigenfactor was assigned from a distribution centered around 0.002120 and an SD of 0.0007066667.

The tm R package was used to clean up the title and abstract text, remove stopwords, extract stem words, before converting word frequencies to 'term frequency-inverse document frequency' (TF-IDF). Sparse terms that occured in less than 5% of abstracts or less than 1% of titles were dropped. Title and abstract TF-IDF were extracted separately, and are used separately as features. 

## Model fitting
boooop WIP 
I'm reallllly lazy. It might just be easier to go through my code instead. 

# Results
## Summary stats
In total, 30k abstracts were pulled from PubMed, but 70 were missing abstracts *(of course, why should life ever be so easy)*. We proceeded with the remaining 29,930 abstracts. The extracted feature set consisted of 141 and 313 TF-IDF values from the title, and abstract respectively, the 10 NRC sentiments, impact factor, Eigenfactor, number of authors, and publication year for a total of 468 features. 

{% include figure image_path="/assets/images/pubmed/2017-09-30_citation_cumulative_dist.png" alt="Figure 1. Cumulative Distribution of Citations" caption="**Figure 1**. Cumulative distribution of citations across the 30k abstracts. Subplot panel shows a higher resolution of the citation distribution." %}

Figure 1 shows the cumulative distribution of citations and it appears to approach 99% at approximately 30 citations. Furthermore, a third of the papers were not cited at all, and if a paper received at least two citations, then it was already *ahead of the curve* (Figure 1). 

### Are there journals that are over-represented?
We extracted the top 10 recurrent journals and appended journals that we typically aim to publish in. 

{% include figure image_path="/assets/images/pubmed/2017-10-01_popular_journals.png" alt="Figure 2. Popular Journals" caption="**Figure 2**. Top 10 recurrent journals in the dataset and popular journals that our lab aims to publish in. Forest plot indicates median number of citations as well as the distribution of citations for studies in the paper. Impact factor of journal is indicated in barplot on the right." %}

We find that PloS one is a clear outlier with ~3% of the dataset going into the journal. The distribution of citations for PloS one paper tends to be fairly low. In contrast, the third most popular journal was the Proceedings of the National Academy of Science (PNAS), which outputs papers with a right skewed distribution of citations. Much like PNAS, higher impact journals such as the trifecta - Nature, Science, and Cell - have similar citation distributions for their smaller number of papers, but with a higher median, and a greater skew. 

### Do manuscript submissions wax and wane with the seasons? 
Out of the 30k abstracts, 48.2% have data for month of submission. 

{% include figure image_path="/assets/images/pubmed/2017-09-10_papers_months.png" alt="Figure 3. Paper Season" caption="**Figure 3**. Bottom panel shows distribution of manuscript submission over the 12 months while violin plot above shows the log2 distribution of citations. Colours of barplots denotes 'seasonality'." %}

There is a clear preference for submissions between July and September with fewer manuscripts being submitted during the winter months. Why this trend exists could be due to a myriad of reasons that we cannot prove as it is beyond the scope of this study. However, we can make baseless speculations:
- Undergraduate student doing a summer project managed to complete it and the boss wants to push out a manuscript. 
- Undergraduate student doing a summer project did not complete it and want to push out a paper anyway because they think science is easy and they are hot stuff. 
- Principal investigators (PIs) are all flying to conferences in Hawaii and got around to reading their backlog of manuscripts and approving them for submission while on the plane.
- During the winter, PIs are at home with their family and knows that editors are on vacation too so your manuscript goes onto the pile of 'To Dos'. 

We can take the analysis a bit further by returning to the target journal set. It is important to keep in mind that the data that was extracted from PubMed were papers that were *accepted and published* by the journal. 
{% include figure image_path="/assets/images/pubmed/2017-09-10_journals_months.png" alt="Figure 4. Journal Season" caption="**Figure 4**. Individual season frequency plot for journals of interest. Journals are indicated at the top of their panels. Most successful papers in high impact journals were *not* submitted during the winter. NEJM did not report submission information." %}

Although there are fewer papers from the target journals, Figure 4 shows a clear dearth of published papers that were submitted in January or December. It is difficult to draw a conclusion without seeing the number of papers that were submitted in each month. Are editors and reviewers more harsh during the winter? Or are there fewer manuscripts being submitted? If we go back to Figure 3, the violin plot clearly shows the presence of highly cited papers regardless of when they were submitted. Needless to say, if your research is high impact, it will be cited no matter what month you submit in. 

### Modeling and Feature Importance
To determine which features were important in determining the 'success' of an abstract, and consequently the paper, we performed a boosted tree regression using the `xgboost` R package. For evaluating performance of the model, a holdout of 25% was set aside. We tuned `nrounds` using nested cross validation with 4 inner folds and 10 outer folds with RMSE as the performance measure. Is this a little over the top? Probably, but I think I passed that threshold when I decided to use `xgboost` instead of `glmnet`. Throughout the tuning, `nrounds` was capped at 100 to avoid overfitting. In some of my preliminary runs, I noticed that the `nrounds` hit 400, and I get a beautiful fit for the train data, but the test data was just a blob (aka, overfitting). It appears that overfitting gradient boosted trees is just easy, who would've thought. 

Model was evaluated by predicting on the hold out set. 
{% include figure image_path="/assets/images/pubmed/2017-10-01_main_model_predicted.png" alt="Figure 5. Model Evaluation" caption="**Figure 5**. Predicted and true values for both the training and test set with RMSE indicated." %}

The RMSE for both train and test were fairly comparable (Figure 5). The blob near the origin is a little concerning, but as previously mentioned, 2/3 of the data points have 2 or fewer citations, which means we have at least 10,000 points sitting there. Model was not overfitted, and did a decent job with the held out set. I think I might be able to do a better job if I tuned more intensely with a grid search or used GLMNET. 

What I'm actually interested in are the important features in the model. 
{% include figure image_path="/assets/images/pubmed/2017-10-01_feature_importance_main_model.png" alt="Figure 6. Feature Importance" caption="**Figure 6**. Important features associated with citation numbers." %}
According to Figure 6, if you are interested in being cited a ton of times, the most important thing to do is to just publish in a high impact journal. *Sure, why don't I just publish **all** my papers in New England. Easy.* The second most important feature is 'year'. I guess you just wait for the citations to roll in? 

Okay, well, that wasn't completely unexpected. For the rest of the features, we have keywords in the abstract including: 
- gene
- analysi-
- requir-
- key
- provid-
- specfi-
- character- (this is probably something like characterized)
- protein
- evid- (like evidence)
- avail- 

Number of authors also appears to be an important feature, and this may be tied into impact factor of paper. For title feature, there was only one and it was 'analysi-'. There were also two sentiments, "anger" and 'anticipation'. We will revisit these in a later plot. 

Next, we wanted to see how these feature importances change year-over-year. Thus, we fit the model again, but separately per year, and by dropping the year feature as well (as it will be invariant). We didn't generate a regression plot, and only grabbed the feature importance. 
{% include figure image_path="/assets/images/pubmed/2017-10-01_all_models_importance.png" alt="Figure 7. Feature Importance Over Time" caption="**Figure 7**. Important features associated with citation numbers for each year between 2010 and 2015. Features in whole model were retained if importance was greater than 0.01, while per year features were kept if they were above 0.05. Features were ordered descendingly by their importance in the *all* model. Features below the red line were importance in a year model, but not the *all* model." %}
Again, the most important feature was publication in a high impact journal. ¯\\\_(ツ)\_/¯ However, in certain years, some sentiments and some keywords were also important. 

Anger and anticipation popped out as important sentiments. What words were associated with these sentiments? I intersected the words for the first 1,000 abstracts with the NRC sentiment dictionary and generated two word clouds.
{% include figure image_path="/assets/images/pubmed/anger_anticipation_cloud.png" alt="Figure 8. Anger and Anticipation Word Clouds" caption="**Figure 8**. Words associated with *anger* and *anticipation* according to the National Research Council (of Canada :))." %}

Alrighty, so it's clear that papers on cancer will probably receive more citations (Figure 8). On the anticipation side, we see risk and time. How do they fit in? I will probably guess risk stratification for disease (such as cancer), and time to death or relapse, as these are commonly analyzed in cancer datasets. 

# Discussion
In this study, we analyzed about 30k abstracts between 2010 and 2015 to determine if certain features can be linked to increased citations. We determined that to maximize citations, the authors should aim to publish in a high impact journal (not easy to do), have many co-authors (easy to do, and people will self-cite), or work in cancer or health research (yes, I would like to refocus this ecological lab to studying mesothelioma. What do you mean no?). At first glance, it is true that highly cited papers tend to be either well used tools like BLAST, or maybe health policy related studies, and of course, cancer, but we failed to take into account the min and max of different fields. Different disciplines may publish in niche journals, and being cited 10 times may be considered successful for that discipline. Moreover, we also don't consider what it means to others to be *successful*. Here, I am equating it to a measurable value. To some, it may be publishing in Nature Genetics, or the trifecta. To others, it could be obtaining a PI position, or maybe even to push out good, sound, replicable science. Perhaps some people like being cited many times. 
Regardless, success is personal. We should always set reasonable and incremental goals to make ourselves better, and to make the world a better place. =) 

*A journey of a thousand miles begins with a single step.*  