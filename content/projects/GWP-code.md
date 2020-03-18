---
title: "Code - World Happiness Report Data Analysis"
author:
  name: KT Hobbs
date: '2020-03-14'
series: Hugo 101
linktitle: Code - World Happiness Report Data Analysis Life Value
type:
- post
- posts
weight: 10
---

Data 552 - Master of Data Science Project, UBC

----


### Part 1: Cleaning
```{r Cleaning}
# drop unneccessary columns
life2 <- life[1:16]

# rename columns for simplicity
colnames(life2) <- c("Country", "Year", "Ladder", "logGDP", "Support", "LifeExp", "Freedom", "Generosity", "Corruption", "PosAffect", "NegAffect", "GovConf", "DemQuality", "DeliveryQuality", "Inequality", "InequalityFromAverage")
```

```{r, include = F}
# find the smallest year that all countries have data for
max_min_year <- 2000

for (i in life2$Country){
  if (min(subset(life2, life2$Country == i)$Year) > max_min_year) {
    max_min_year <- min(subset(life2, life2$Country == i)$Year)
  } 
}

max(life2$Year)
```

### Part 2: Make measures and group data

```{r log GDP growth}
library(dplyr)

# subset years and assemble countries into 4 groups: ----
life3 <- subset(life2, Year >= 2017)

# sort by country ----
rwidx <- order(life3$Country, life3$Year)
life4 <- life3[rwidx, seq(1:16), drop = FALSE]

# initialize variables ----
j <- life4$Country[1]
dif <- NA

# determine differences in log GDP per nation over time (years) ----
for (i in seq(life4$Country[2:nrow(life4)])){
  
  if (life4$Country[i] == j){
    sub <- NA
    
    #print(paste(life4$Country[i], "is equal to", j))
    
    sub <- subset(life4, life4$Country == j)
    dif <- append(dif, diff(sub$logGDP))
   
    
  } else {
    
    #print(paste(life4$Country[i], "is not equal to", j))
    #print(paste(j, "is now", life4$Country[i+1]))
    j <- life4$Country[i+1]
    dif <- append(dif, NA)
   
  }
}


dif2 <- as.data.frame(dif)
length(dif2[is.na(dif2)])
```

*To many NA's generated when calculating log GDP growth due to insufficient data.*


```{r Measures}
# define positivity as the ratio of positive to negative thoughts/feelings
life3$Positivity <- life3$PosAffect/life3$NegAffect

# find thresholds using median to avoid outlier influence with mean:
## positivity
pos_threshold <- median(na.omit(life3$Positivity))
gov_threshold <- median(na.omit(life3$GovConf))
corrup_threshold <- median(na.omit(life3$Corruption))

## circumstance
soc_threshold <- median(na.omit(life3$Support))
free_threshold <- median(na.omit(life3$Freedom))
inequality_threshold <- median(na.omit(life3$Inequality))
gdp_threshold <- median(na.omit(life3$logGDP))

```

```{r Group data}
# A. positivity and negative circumstance ----
groupA <- subset(life3, 
       # positivity
       life3$Positivity > pos_threshold &
         life3$GovConf > gov_threshold &
          life3$Corruption < corrup_threshold &
         
         # negative circumstance
         life3$Support < soc_threshold &
         life3$Inequality > inequality_threshold &
         life3$logGDP < gdp_threshold   
         )

avgA <- mean(groupA$Ladder)


# B. negativity and positive circumstance ----
groupB <- subset(life3, 
       # negativity
       life3$Positivity < pos_threshold &
         life3$GovConf < gov_threshold &
         life3$Corruption > corrup_threshold &
         
         # positive circumstance
         life3$Support > soc_threshold &
         life3$Inequality < inequality_threshold &
         life3$logGDP > gdp_threshold   
         )

avgB <- mean(groupB$Ladder)


# C. POSITIVE CONTROL: positivity and positive circumstance ----
groupC <- subset(life3, 
        # positivity
       life3$Positivity > pos_threshold &
         life3$GovConf > gov_threshold &
          life3$Corruption < corrup_threshold &
         
         # positive circumstance
         life3$Support > soc_threshold &
         life3$Inequality < inequality_threshold &
         life3$logGDP > gdp_threshold  
         )

avgC <- mean(groupC$Ladder)


# D. NEGATIVE CONTROL: negativity and negative circumstance ----
groupD <- subset(life3, 
       # negativity
        life3$Positivity < pos_threshold &
        life3$GovConf < gov_threshold &
        life3$Corruption > corrup_threshold &
         
         # negative circumstance
         life3$Support < soc_threshold &
         life3$Inequality > inequality_threshold &
         life3$logGDP < gdp_threshold     
         )

avgD <- mean(groupD$Ladder)
```

### Part 3: Compare groups

```{r assess data, include = F}
# Assumption 1: is it iid?

# Assumption 2: is it Normal?
qqnorm(life3$Ladder)
```

```{r group data}
# put groups into one dataframe ----
A <- as.matrix(groupA)
rownames(A) <- c(rep("A", nrow(A)))

B <- as.matrix(groupB)
rownames(B) <- c(rep("B", nrow(B)))

C <- as.matrix(groupC)
rownames(C) <- c(rep("C", nrow(C)))

D <- as.matrix(groupD)
rownames(D) <- c(rep("D", nrow(D)))

ABCD <- rbind(A, B, C, D)
ABCD2 <-as.data.frame(ABCD)

# add group names
ABCD2$Group <-rownames(ABCD)
ABCD2$Group <- as.factor(ABCD2$Group)

# convert ladder from factor to numeric
ABCD2$Ladder <- as.numeric(as.character(ABCD2$Ladder))
ABCD2

# to CSV
write.csv(ABCD2, "life-study-groups.csv")
```

##### Calculate differences

```{r anova}
mod1 <- aov( Ladder ~ Group, data = ABCD2 )
summary(mod1)
```

We reject the null hypothesis ie. group means are significantly different from each other.

Which groups differ? Conduct t-tests....

```{r A-C calcs}
# A. vs C. ----
t.test(groupA$Ladder, groupC$Ladder)

```

```{r B-C calcs}
# B. vs C. ----
t.test(groupB$Ladder, groupC$Ladder)
```

```{r A-D calcs}
# A. vs D. ----
t.test(groupA$Ladder, groupD$Ladder)
```

```{r B-D calcs}
# B. vs D. ----
t.test(groupB$Ladder, groupD$Ladder)
```

##### Summary:

**Results:**
    
    * Significant difference between A. and C.
    * Significant difference between B. and C.
    * No significant difference between A. and D.
    * Significant difference between B. and D.
    
    
 | Interpretations 
---|-----------------
 | Negative circumstances influence perceived life value
 | Negativity influences perceived life value
 | Positivity does not influence perceived life value 
 | Positive circumstances influence perceived life value

    
**Conclusions:**

    * Positivity correlates with perceived life value
    * Positive circumstances correlates with perceived life value
    * Negativity does not correlates with perceived life value
    * Negative circumstances correlate with perceived life value
