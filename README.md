
# Analysis of White Wine Dataset 

As a wine lover, I would like to analyse the 'White Wine Quality' dataset and try 
to understand which attributes really contribute to the wine quality. As I am 
not an expert in wines, I am not sure what to look for exactly however I am 
hoping the dataset will give me a rough idea what to look for next time when I 
am purchasing wine. 


```{r echo=FALSE, message=FALSE, warning=FALSE, packages}
# Load all of the packages 

library(knitr)
library(dplyr)
library(ggplot2)
library(GGally)
```

```{r echo=FALSE, message=FALSE, warning=FALSE, Load_the_Data}
# Load the Data
wine <- read.csv('wineQualityWhites.csv')

```



# Univariate Plots Section

&nbsp;

#### The structure of the dataset:
The dataset contains 4898 observations with 13 variables.
```{r echo=FALSE, message=FALSE, warning=FALSE, Univariate_Plots}
str(wine)
```
&nbsp;

#### Missing values:
Before starting, I will check if there are any missing values in the dataset.
```{r echo=FALSE, message=FALSE, warning=FALSE}
length(wine[is.na(wine) == TRUE])
```

&nbsp;

#### Summary of the wine qualities:
The wine qualities range between 3 to 9. None of the 4898 observations got a 
score of 1, 2 or 10. The average quality is 5.878.
```{r echo=FALSE, message=FALSE, warning=FALSE}
summary(wine$quality)
```

&nbsp;

#### Distribution of wine qualities:

The bulk of the wines got a score between 5 to 7.
```{r echo=FALSE, fig.width=10}
ggplot(data = wine, aes(quality)) + geom_bar()

```

&nbsp;

#### Alcohol percentage of wines:

Alcohol percentage of wines have a range between 8.0 to 14.2. The average 
percentage is at 10.51. 


```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(alcohol)) + geom_histogram(binwidth = 0.1) +
  scale_x_continuous(breaks = seq(8,14,1))
```

&nbsp;

#### PH distribution of wines:

The pH values are distributed normally and range between 2.72 to 3.82. Mean is 
at 3.188.

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(pH)) + geom_histogram(binwidth = 0.01)
```

&nbsp;

#### Residual sugar in each wine:

Residual sugar determines the sweetness of the wines. It ranges between 0.6 to 
65.8 gr. per liter, wowever majority has 0.6 to 20 gr. per liter.
```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(residual.sugar)) + geom_histogram(binwidth = 0.5)
```

&nbsp;

#### Density of wines:

The densitiy ranges between 0.9871 to 1.0390. However the bulk fo the wines 
have a density until 1.0025. Mean densitiy for the dataset is 0.994

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(density)) + geom_histogram(binwidth = 0.001) +
  coord_cartesian(xlim = c(0.98, 1.01)) + scale_x_continuous(breaks = seq(0.98, 1.01, 0.005))
```

&nbsp;

#### Fixed Acidity:

The fixed acidity ranges between 3.8 and 14.2. Mean fixed acidity is at 6.855.


```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(fixed.acidity)) + geom_histogram()
```

&nbsp;

#### Volatile Acidity:

Volatile acidity starts from 0.08 and ends at 1.1 with a mean at 0.2782.


```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(volatile.acidity)) + geom_histogram()
```

&nbsp;

#### Citric Acid:

Some of the wines have no citric acid at all. The highest citric acid rate is 
at 1.66 and the average rate is 0.3342.


```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(citric.acid)) + geom_histogram()
```

&nbsp;

#### Chlorides:

The minimum chloride value for a wine is 0.0090 abd the max is 0.346. The mean 
is at 0.04577.

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(chlorides)) + geom_histogram()
```

&nbsp;

#### Free Sulfur Dioxide:

The minimum free sulfur dioxide value is 2 and the maximum is 298. However the 
main bulk is between 23 and 46. 

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(free.sulfur.dioxide)) + geom_histogram()
```

&nbsp;

#### Total Sulfur Dioxide:

The total sulfur dioxide has a nice normal distribution, starts at 9 and reaches up to 440. The average value is
138.4.

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(total.sulfur.dioxide)) + geom_histogram()
```

&nbsp;

#### Sulphates:



Sulphates have a bimodal distribution. The lowest value is 0.220 and max value 
is 1.08

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(sulphates)) + geom_histogram()
```

&nbsp;

# Univariate Analysis


### Structure of the dataset

The dataset holds information about 4898 white wines. For each wine, there are 
11 objective attributes of as well as a overall quality evaluation, which is 
the median quality evaluation of at least 3 wine experts. All of the attributes 
are either integer or numerical values.


### Main feature of interest

Main feature in the dataset is the quality. I am interested in finding out what 
attributes are affecting the perceived quality.   

### Other features in the dataset to support investigation

I am not a wine expert so I cannot say for sure which features are directly 
effecting the quality of the wines. However I believe alcohol percentage, 
pH level, residual sugar level and density might have a direct effect on the 
quality scoring. Nevertheless, it is a good idea to keep an eye open also for 
the other attributes. 


### Unusual distributions 

I found the distribution of alcohol percentages unusual. I always thought that 
almost all of the wines have 8-10% alcohol and that all above are rather rare. 
However, this is not the case. Alcohol disribution seems to be positively 
skewed however there are also many wines above 12%.  
Luckily, the dataset does not have any NA values. I only removed the column 
called 'X' as itwas only there to number the wines, which I will not need. 

# Bivariate Plots Section

Let's start by using GGPAIRS to investigate all bivariate relations:

&nbsp;

```{r echo=FALSE, Bivariate_Plots, fig.width= 14, fig.height= 16}
ggpairs(wine)
```

&nbsp;

The features that I mentioned above have the following correlations to quality:

Alcohol percentage: 0.436 

pH level: 0.0994 

Residual sugar: -0.0976 

Density: -0.307 

 
From those, only density and alcohol percentage have correlations that are 
somewhat high. Let's investigate them closer by creating boxplots and 
scatterplots:

&nbsp;

#### Quality vs. Alcohol:

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(x= as.factor(quality), y= alcohol)) + 
  geom_boxplot() 

```

&nbsp;

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(x= quality, y= alcohol)) + geom_jitter(alpha = 1/5) +
  geom_smooth(method='lm')

```

&nbsp;

#### Quality vs. Density

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(x= as.factor(quality), y= density)) + geom_boxplot()

```

&nbsp;

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(x= quality, y= density)) + geom_jitter(alpha = 1/10) +
  geom_smooth(method='lm')
```


There are several interesting things to see here. As mentioned above, there is 
a correlation of 0.436 between alcohol and quality. This can be seen in the 
boxplot, where quality from 5 - 9 increases always parallel to higher alcohol
percentages. Similarly, the scatter plot also shows a positive upwards trend 
between the two variables. This means, judges usually tend to give higher 
quality grades to wines with above 10% alcohol rate.

Density and quality also correlate (-0.307) however as opposed to the alcohol
and quality, these two variables have a negative relationship. Again in boxplot
chart, we see how quality between 5 - 9 increases as density continously
decreases. Also the scatter plot shows a negative trend between the two. 
Interestingly, in both alcohol and density, quality between 5 - 9 has really 
clear trends that either increaes or decreases. However quality scores of 
3 and 4 are not in line with these trends. This probably means there are some 
low quality wines with different attributes however in majority higher alcohol 
percentage and lower density are usually indicators of higher quality scoring. 


I also want to check the relationship between other variables. Two really 
strong correlations here are between density and residual sugar and density 
and alcohol.

&nbsp;

#### Density vs. Residual Sugar

The strongest correlation in the dataset is between density and residual sugar 
with 0.839:

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(aes(x = residual.sugar, y = density), data = wine) +
  geom_point(alpha = 1/5, position = 'jitter') +
    coord_cartesian(xlim = c(0, quantile(wine$residual.sugar, .99)), 
                    ylim = c(min(wine$density), quantile(wine$density, 0.99))) +
  geom_smooth(method = "lm", se = FALSE) 
```

&nbsp;

#### Density vs. Alcohol

The second strongest correlation in the dataset is between density and alcohol
with -0.78:

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(aes(x = density, y = alcohol), data = wine) +
  geom_point(alpha = 1/5, position = 'jitter') +
    coord_cartesian(xlim = c(quantile(wine$density, .01),
                           quantile(wine$density, .99))) +
  geom_smooth(method = "lm", se = FALSE) 
```

&nbsp;

# Bivariate Analysis


### Relationships observed about main feature

I wanted to find out which features directly relate to the quality variable. For
this purpose, I investigated alcohol percentage, pH level, residual sugar and 
density. I discovered that none of these features strongly correlated to 
quality. Among those, alcohol percentage with 0.436 correlation had the 
strongest relationship. I also discovered, among better quality wines, usually
higher percentage of alcohol led to better quality evaluations.
The second strongest correlation was the density with -0.307. Here, I saw an 
opposite trend: among good quality wines, the less dense ones scored overall 
better.
The pH level and residual sugar had a rather small impact on the quality to my 
surprise.

### Relationships between the other features

Two really strong relationships that I discovered were between density and 
residual sugar and density and alcohol. As expected more residual sugar meant 
denser wine and other way around more alcohol meant less dense wine.

### Strongest relationship found

The strongest relationship is between density and residual sugar with 0.839.

&nbsp;

# Multivariate Plots Section

&nbsp;

#### Alcohol vs. Density vs. Quality

As first, I want to investigate the relationships between alcohol, density and 
quality a bit closer.

```{r echo=FALSE, fig.width=10, Multivariate_Plots}
ggplot(data = wine, aes(x = density, y = alcohol, color = as.factor(quality))) + 
  geom_jitter(alpha = 1/3) + geom_smooth(method = "lm", se = FALSE,size=1) +
  coord_cartesian(xlim = c(quantile(wine$density, 0), 
                           quantile(wine$density, 0.99)) ,
                  ylim = c(min(wine$alcohol), quantile(wine$alcohol, 0.99))) +
  scale_color_brewer(type='qual', palette =  3)
```

Here, I plotted alcohol vs. density and colored the quality scores. We can see 
from the plot the negative relationship between alcohol and density: as alcohol 
percentage increases, density decreases. Moreover, going towards the top left, 
we are getting closer to the sweet spot. More and more wines are getting good 
scores at higher alcohol vs. lower density relationships.

&nbsp;

#### Density vs. Residual Sugar vs. Alcohol

As next, I would like to investigate the relationship between density, residual 
sugar and alcohol. For this purpose, I will first create buckets for alcohol 
percentages.


```{r echo=FALSE, message=FALSE, warning=FALSE}
wine$alcohol_bucket <- cut(wine$alcohol, c(7,9,10,11,12,13,15))
table(wine$alcohol_bucket)
```
&nbsp;

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10}
ggplot(data = wine, aes(x = residual.sugar, y = density, 
                        color = wine$alcohol_bucket)) + 
  geom_jitter(alpha = 1/3) +
  geom_smooth(method = "lm", se = FALSE,size=1) +
  coord_cartesian(xlim = c(0, quantile(wine$residual.sugar, 0.99)), 
                  ylim = c(min(wine$density), quantile(wine$density, 0.99))) +
  scale_color_brewer(type = 'qual', palette = 3)
 
```

This plot shows an interesting relationship between these 3 variables. As the 
wines become sweeter, the density increases. On the other hand, for the same 
sweetness level, more alcohol makes the wines less dense.  

&nbsp;

# Multivariate Analysis

### Multivariate relationships observed

The most interesting finding here was the relationship between alcohol, density 
and quality. I discovered denser wines with more alcohol percentage tend to get 
better scorings.


### Interactions between features

The relationship between density, residual sugar and alcohol was really 
interesting. The sweeter the wine, denser it is. On the other for the same 
residual sugar level, more alcohol percentage meant less density. 


------

# Final Plots and Summary


### Plot One



```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10, Plot_One}
ggplot(data = wine, aes(x= as.factor(quality), y= alcohol)) + 
  geom_boxplot(outlier.color = 'red', outlier.shape = 1) +
  geom_jitter( alpha = 1/6) + 
  stat_summary(fun.y = 'mean', geom = 'point', color = 'red', shape = 8, 
               size = 4) +
  xlab('Quality') +
  ylab('Alcohol') +
  ggtitle('Quality vs. Alcohol') +
  theme(plot.title = element_text(hjust = 0.5)) +
  scale_fill_brewer(palette=1)

```

&nbsp;

### Description One

As I found out in my investigation, alcohol has the strongest correlation with 
the quality scores. However, the relationship is not perfectly linear. To show 
this relationship best, I used boxplots for each quality and marked means of 
each quality score. The alcohol percentages goes initially down however at 
better quality ranges (5 - 9), it contiously increases.

&nbsp;

### Plot Two

```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10, Plot_Two}
ggplot(aes(x = residual.sugar, y = density), data = wine) +
  geom_point(alpha = 1/5, position = 'jitter', color = 'seagreen') +
    coord_cartesian(xlim = c(0, quantile(wine$residual.sugar, .99)), 
                    ylim = c(min(wine$density), quantile(wine$density, 0.99))) +
  geom_smooth(method = "lm", se = FALSE, linetype = 2) +
  xlab('Residual Sugar (g / dm^3)') +
  ylab('Density (g / cm^3)') +
  ggtitle('Density vs. Residual Sugar') +
  theme(plot.title = element_text(hjust = 0.5))

```

&nbsp;

### Description Two

Besides having the second strongest relationship with the quality, density also 
happens to have the strongest correlation among all of the features. With 0.839 
correlation to residual sugar, we get a nearly perfect linear relationship, 
which I tried to capture in the chart above.

&nbsp;

### Plot Three
```{r echo=FALSE, message=FALSE, warning=FALSE, fig.width=10, Plot_Three}
ggplot(data = wine, aes(x = density, y = alcohol, color = as.factor(quality))) + 
  geom_jitter(alpha = 1/3) + geom_smooth(method = "lm", se = FALSE,size=1) +
  coord_cartesian(xlim = c(quantile(wine$density, 0), 
                           quantile(wine$density, 0.99)) ,
                  ylim = c(min(wine$alcohol), quantile(wine$alcohol, 0.99))) +
  scale_color_brewer(type='qual', palette =  3, name = "Quality") +
  xlab('Density (g / cm^3)') +
  ylab('Alcohol %') +
  ggtitle('Quality by Alcohol vs. Density') + 
  theme(plot.title = element_text(hjust = 0.5))
```

&nbsp;

### Description Three

After finding out the strongest correlators of quality: alcohol and density, 
I plotted all three in a multivariate plot with using quality as color. As can 
be seen, quality increases rapidly towards upper left portion 
(more alcohol, less dense).

------

&nbsp;

# Reflection


Throughout this investigation, I discovered many cool things about white wines. 
I found out, that the quality scores did not rely on a sole feature but 
depended probably on a mixture of many. I discovered that the strongest 
influencer of the quality in this set was alcohol. After that, it was density. 
Overall, the judges scored less dense and higher percentage wines better. I 
also discovered that the relationship for both features were not linear 
(thus low correlation scores), although for higher scores, they showed clearer 
trends.    
One of the main advantages of the dataset was the fact that there were no 
missing data. The data was perfectly structured, so I could start right away 
with the investigation. The dataset also had nearly 5000 wine evaluations, 
which provided usually enough samples while doing multivariate analysis. 
One of the main struggles that I had was not having any direct strong influencer
of quality. Although there were many features in the dataset, they were mostly 
weakly correlated with the score.

I believe, as a future work, it would make definitely sense to expand the 
features to also cover other attributes like grapes types, land where the the 
wine is produced, year of production and etc. Currently, most of the features 
in this dataset are of chemical nature and they would probably offer way more 
insights in combination with non-chemical features
