---
author:
  name: "KT Hobbs"
date: 2019-12-13
linktitle: Blog for U.S. Airline Cancellations Ratios
type:
- post
- posts
title: Blog for U.S. Airline Cancellations Ratios
weight: 10
series:
- Hugo 101
---

Master of Data Science Project, UBC

--- 

### Reliable airlines for your USA itinerary
									
The United States is a buzzing tourism hub for many, offering scenes from dense natural reserves to innovative cityscapes, and every combination between.

With 9.834 million km² to explore, it's no surprise that even locals look for quick vacation getaways or short-term adventure travels here.
										
To help narrow down the backyard traveller's itinerary and ensure every minute of travel is optimized, Lonely Planet has sent their top data scientists finger-tips-first into 2008's USA flight data.

First, let's observe the most popular departure origins for domestic flights in the USA.

![Barchart of frequent origins](/barchart.png)

![Airports and abbreviations](/airport1.png)

![Airports and abbreviations](/airport2.png)								
												
											
Not surprisingly, the most popular airports for departures are in some of America's largest cities. 
Now that we have narrowed down where you'll likely be traversing from, let's make sure you choose the right airline so you can get to your next destination on schedule.

							
![Heatmap](/hm.png)	

							
To read this heatmap, begin by searching for your departure airport along the vertical axis. The corresponding airline carrier (shown on the horizontal axis) is shaded according to the ratio of flight cancellation to total number of flights. Red shades indicate a high frequency of cancellations for a flight carrier departing from this origin, while dark blue indicates no cancellations.

Grey blocks represent airports that an airline does not depart from. </br>

From this analysis, it's safe to say if you're departing from Salt Lake City, steer clear of flying with 9 Air Co Ltd! 


Unsure what all these abbreviations stand for? Check out the reference table below!

![Airline carriers and codes](/carrier1.png)
![Airline carriers and codes](/carrier2.png)

Airline Carrier code information retrieved from: [IATA](https://www.iata.org/publications/pages/code-search.aspx)


Airport information retrieved from: [Open Flights](https://openflights.org/data.html)


Airport analysis data retrieved from:  [R Tricks for Kids](http://rtricks4kids.ok.ubc.ca/wjbraun/DS550/air.csv)

