---
author:
  name: "KT Hobbs"
date: 2020-06-23
linktitle: Modeling and Visualization of COVID-19 in Ontario
type:
- post
- posts
title: Modeling and Visualization of COVID-19 in Ontario 
weight: 10
series:
- Hugo 101
---

Master of Data Science Capstone Project, UBC

[Bringing Understanding to the COVID-19 Outbreak in Ontario](https://masterdatascience.ubc.ca/data-stories/data-action-bringing-understanding-covid-19-outbreak-ontario)

[D3 Interactive Visualization](https://ubco-mds-2019-labs.github.io/data-599-capstone-statistics-canada/kt/)

---

### Objectives: 

* To produce an inferential statistical model of factors that may be associated with the probability of COVID-19 outbreaks in different LTC homes in Ontario.

* To produce an inferential statistical model of the proximity and health factors that may be  associated with COVID-19 disease activity at the level of the PHU regions in Ontario.

* To produce an interactive web page using QGIS and D3 to visualize the results from both PHU region analysis and LTC homes analyses.

* To leverage open data sources in meaningful, exploratory analyses.
 
### Summary of Results:
 
 
#### Long-term care homes
 
It has been suggested that the current COVID-19 crisis in long-term care (LTC) homes has been many years in the making, a consequence of chronic under funding, neglect, and ineffective models of care both in Canada and elsewhere (Werner et al., 2020). However the individual factors and mix of factors that beget quality, or that put a home at risk of a devastating COVID-19 outbreak in the medium term, are unclear. In the long term, smaller scale family style homes with small numbers of residents have been put forth as being a higher quality alternative to the current model of institutional care. In the medium term, with respect to the current pandemic, a study examining the COVID-19 outbreak in LTC homes in Ontario showed that a greater number of beds and location in a high prevalence region increases the risk of an outbreak. For-profit status was not associated with likelihood of an outbreak but was associated with the size of an outbreak and the number of resident deaths (Stall et al., 2020). Our analysis adds new information to the existing knowledge, showing that in addition to the number of beds, the total number complaint reports is also associated with the likelihood of an outbreak. Moreover, municipal non-profit home-type and the total number of non-complaint reports are protective.


#### Public Health Unit analysis

In this study, open data from several Statistics Canada and Government of Ontario resources were successfully integrated and utilized in a meaningful, macro-level, exploratory analysis of COVID-19. Evaluating high proportions of COVID-19 using health indicators and degree of “connectedness” seem to suggest a profile of less healthy, highly connected Public Health Units. Yet, these associations are neither definitive or comprehensive. In fact, through LASSO and PCA, indicators of poor health, such as heavy drinking, were determined to be protective as they were prevalent in regions with low case proportions. Toronto Public Health may have low proportions of “heavy drinking” yet is the most connected health unit. As a result of the associative nature of this research, the results may misleadingly suggest that health indicators are protective. Heavy drinking may also be confounding to a latent variable that was not captured in this study. Further investigation with additional data may be more telling.

Similarly, investigation of COVID-19 fatality proportion showed a relationship between regions with people reporting a strong sense of belonging and lower COVID-19 fatality proportion. This also suggests that having strong community sense is protective; however, as stated previously, this may be related to a confounding or latent variable that were either overlooked or incapable of being captured with the available open data. 




