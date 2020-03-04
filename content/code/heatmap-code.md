---
author:
  name: "KT Hobbs"
date: 2019-12-01
linktitle: Heatmap of USA Airline Cancellation Ratios
type:
- post
- posts
title: Heatmap of USA Airline Cancellation Ratios
weight: 10
series:
- Hugo 101
---

Master of Data Science Project, UBC

--- 

### Backgound
**Who are you? i.e. one of "airline employee", "airline consultant", "air traffic regulator", "citizen watchdog", "reporter for NY Times", ...**
Journalist for Lonely Planet

**Who is your audience? i.e. one of "airline CEO", "Director of NAS", "general public", ...**
Travellers - for domestic USA flights

**Where you are presenting this? i.e. one of "newspaper", "TV public service announce- ment", as a static display on the website of a single airline, or the NAS, or the NY Times, ...**
E-magazine article

**Why are you presenting this? What is the basic message that you are trying to convey? (One sentence)**
To allow travellors to select the most suitable airline for their itinerary by providing information on the tendency of airline cancellations by origin.

---

### Analysis
```{r,echo = T, results='hide'}
library('data.table')
library('dplyr')
air <- read.csv("air.csv")

# checked, there's no NA in variable 'Cancelled', thus there's no need to remove or impute NAs
sum(air$Cancelled=='NA')
```


```{r,echo = T, results = 'hide'}
# calculate the number of cancels by origin and unique carrier 
cancels <- aggregate(air$Cancelled, by=list(air$Origin, air$UniqueCarrier), FUN=sum)
colnames(cancels) <- c("Origin", "UniqueCarrier", "CancelledSums")

# count the total number of flights by origin and unique carrier
counts <- air %>% 
  count(Origin, UniqueCarrier)
colnames(counts) <- c("Origin", "UniqueCarrier", "Counts")

# join the cancels dataset and counts dataset
cancelData <- full_join(cancels,counts,by = c("Origin", "UniqueCarrier"))

# calculate the cancel ratio 
cancelData$CancelRatio <- cancelData$CancelledSums/cancelData$Counts
```


```{r,echo = F}
# filter cancelData by top 20 most popular origins 
# plot barplot of top 20 Most Popular Departure Origins
library('viridis')
```

```{r, eval=T}
tableOrigin <- table(air$Origin)
popular_origin <- sort(tableOrigin, decreasing = T)
```
```{r, eval = F}
yticks <- c(0, 100000, 200000, 300000, 400000)
ylabels <- c('0', '10000', '20000', '300000', '400000')
barplot(popular_origin[1:20], ylim=c(0,450000), las=2, 
        axes=F,
        col=viridis(n=25, begin = 0, end = 1), cex.names=0.85)
axis(side=2, at=yticks, labels=ylabels, las = 2)
title("Most Popular Departure Origins for USA Flights")
```

```{r,echo = T, results = 'hide'}
# sort the filtered cancelData by frequency (popularity of the origin)
Origins <- as.data.frame(popular_origin)
colnames(Origins) <- c("Origin", "Frequence")

cancelData20 <-merge(cancelData %>% filter(Origin %in% Origins[1:20,]$Origin),Origins[1:20,], type='left', match='first')
cancelData20<-cancelData20[rev(order(cancelData20$Frequence)),]

```


```{r,echo = T}
# heatmap for cancel ratio by origin and carrier, dark blue represents low cancel ratio, red represents high cancel ratio, grey means no flights with the carrier from the origin
library(ggplot2)

cancel.hm <- ggplot(data = cancelData20 , rescalar = scale_colour_gradient2(), mapping = aes( x = UniqueCarrier,
                                                       y = Origin,
                                                       fill = CancelRatio)) +
 geom_tile() +
  xlab(label = "popular_origin")+
  scale_fill_gradient(name = "Cancellation Ratio",
                      low = "darkblue",
                      high = "red")

ggplotly(cancel.hm)
```


```{r,echo = T, results = 'hide'}
# import and format airportnames data table 
library(knitr)
library(kableExtra)
airportnames <- read.table('airportnames.txt')

df1 <- select(airportnames, 'code','fullname')
df1 <- df1[order(df1$code,decreasing = TRUE),]
rownames(df1)<-NULL
colnames(df1) <- c('Code','Fullname')

df1 %>%
  kable() %>%
  kable_styling(bootstrap_options = "striped", full_width = F, position = "left")
```


```{r,echo = T, results = 'hide'}
# import and format airlinecarriers data table 
airlinecarriers <- read.table('airlinecarriers.txt')
airlinecarriers<- select(airlinecarriers, 'carrierCode','carrier')

rownames(airlinecarriers)<-NULL
colnames(airlinecarriers) <- c('CarrierCode','Carrier')

airlinecarriers %>%
  kable() %>%
  kable_styling(bootstrap_options = "striped", full_width = F, position = "left")

```



# Data Sources
*Airline Carrier code `airlinecarriers.txt` information retrieved from: [IATA](https://www.iata.org/publications/pages/code-search.aspx)*

*Airport information retrieved from: [Open Flights](https://openflights.org/data.html)*

*Airport analysis data retrieved from: [ R Tricks for kids](http://rtricks4kids.ok.ubc.ca/wjbraun/DS550/air.csv.)*



Jasmine Chen & KT Hobbs

