---
author:
  name: "KT Hobbs"
date: 2020-03-10
linktitle: Trusting the Numbers
type:
- post
- posts
title: Trusting the Numbers
weight: 10
series:
- Hugo 101
---

Data 552 - Master of Data Science Project, UBC

*Written by:* Kaitlyn Hobbs

----

Not too long ago, I was listening to an episode of my favourite podcast, Ted Radio Hour, entitled [*Can We Trust The Numbers*](https://www.npr.org/programs/ted-radio-hour/580617765/can-we-trust-the-numbers) that discusses importance and caveats associated with data in the average citizen's day-to-day, one particular concern citing misrepresentation of data. 

As we enter the crux of a Big Data Revolution, it is important to equip ourselves with skills required to think critically about the massive amount of data regularly being presented.


### Misrepresentation Using World Happiness Report Data

Using survey data collected by the Gallup World Poll and processed by [World Happiness Report](https://worldhappiness.report/ed/2019/), we can investigate how different visualizations suggest different conclusions. 

##### About the data

This dataset is comprised of numeric measures on inequality, confidence in national government, log GDP per capita, freedom to make life choices, social support, perceptions of corruption, positive affect (average measures of survey responses assessing an individual’s feelings happiness, laughter, and enjoyment in a day) and negative affect (average measures of survey responses evaluating worry, sadness, and anger in a day) to list a few. 

It also measures the long-term view of a nation's perceived value on their lives on a scale from 1 to 10, which we'll refer to as "life quality".


#### Misleading Correlations and Ignoring the Big-Picture

Let's pretend we're interested in evaluating influences of positivity and circumstance on perceived life value at the national level. To do this, we could look at only the information provided by the positive affect measure.


![](/GWP-scatterplot.png)

In the above scatterplot, we see a general positive trend that indicates nations with high positive thinking on a daily basis rate their overall lives highly compared to nations that score low on positive affect. 

You might even go so far as to conclude that positive-thinking can improve quality of life; however, you'd be making two fatal errors: 

  1. assuming that correlation between these two measures insinuates that one causes the other our data has many other measures and 
  2. ignoring other variables in the data set that may be influencing this trend.
    
    
Overall, this plot fails to consider how a nation's circumstance influences their life quality. 


#### Misleading Proportions with Spatial Representation

Instead, we can consider a more statistical analysis (I'll spare you the details) and group our data to only show nations that have very high or low levels of positivity given a poor or ideal national circumstance as follows:

Group ----|     Scenario
----------------|---------
A. | Positive Perception + Negative Circumstances
B. | Negative Perception + Positive Circumstances
C. | Positive Perception + Positive Circumstance
D. | Negative Perception + Negative Circumstances

![](/GWP-map.png)


We can try to read this visualization by observing the legend, which notates positive and negative perceptions or circumstances with a dash (-) or plus (+) sign, respectively.

At first glance, the colours are uninformative. A reader can't easily discern the difference between positive and negative categories.

Additionally, country borders are indistinguishable and identifying some locations requires extensive geographical knowledge. Can you see where Germany ends and Switzerland begins?

Moreover, a non-obvious concern for visualizing numerical comparisons on maps is that viewers will perceive coloured areas to be proportionate to their values. In this case, it looks as though Canada rates the highest in life quality of those nations with positive mindsets and circumstances when, in actuality, Finland ranks highest.


### Boring Yet Honest Visualizations

I know what you're thinking, a bar graph? Really? Yes. Really. 

![](/GWP-bar.png)

The colours used clearly group data by perceptions (green tones for negative perceptions and red tones for positive) and dark/light shading contrasts positive/negative circumstances. Vertical bars allow readers to compare groups accurately and instantaneously while requiring little background knowledge in statistics.

Using the same legend as the map, we can better observe that nations with positive circumstances and positive thinking rate their life quality much higher than those who think positively yet have negative circumstances - *a contrast to our original scatterplot that suggested positive thinking could improve overall life quality!*

Moving forward, we should be more aware of the possibility that other variables not considered in correlation graphics may be involved in the story being told by the data before conclusions are drawn.

---

#### Take Away

Using the Gallup World Poll results as interpreted by World Happiness Report, we saw how correlation does not imply causation and how misleading representing quantities in a map can be.

It may seem a little disappointing that the most informative, easily read, and truthful illustration of data can sometimes be as simple as a bar plot; however, with the massive amounts of data circulating our perceptions every day, it is vital that we be presented with information thats representative *at first glance*.
