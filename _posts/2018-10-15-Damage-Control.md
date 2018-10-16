---
layout: post
title: Proactive Damage Control
---

![NOAA Image of Hurricane Michael 10/10/18]({{ site.url }}/images/metis_02_NOAA/hurricane_michael_NOAA.png)

It's been a busy season for Atlantic hurricanes. Hurricane Florence, a category 4 storm at its peak, 
dumped nearly 36 inches of rain on the Carolinas en route to causing more than $13 billion in damage. 
Despite having weakened to a Category 1 storm by the time it made landfall in the US, it was one of the wettest 
tropical storms on record. 
Last week, Hurricane Michael was the first ever storm to make landfall in the Florida gulf coast as a Category 4 hurricane. 
Peak winds of 155 mph and a strong storm surge contributed to damage estimates of over $8.1 billion and couting. 
The season's not over quite yet, and currently we're looking at more than $21 billion in total damages and 
more than 80 people dead as a result.  

While we're pretty insulated from the effects of hurricanes up in Chicago, I wanted to take some of the regression 
techniques we've been learning at Metis to try and anticipate the damage these storms cause. 
Being able to proactively identify when these storms will inflict severe damage would hopefully allow 
agencies like FEMA to allocate resources efficienty and be on the scene when residents need them the most.  

Like many government agencies, the National Oceanic and Atmospheric Administration has a treasure trove of data 
at their disposal. 
I took storm time series data from 1851 until the present from the [HURDAT](https://www.nhc.noaa.gov/data/) 
database and aggregated thousands of 6-hourly measurements into overall storm characteristics on windspeed, pressure, 
windspeed radius, duration, and distance travelled, and more. 
Cost estimates for each storm can be found in individual NOAA Hurricane Center after action reports, although 
thankfully those reports are cited in 
[season summary tables on Wikipedia](https://en.wikipedia.org/wiki/2017_Atlantic_hurricane_season) for 1968 onwards. 
I scraped these cost values into a Pandas dataframe and merged them with the meteorological data to get 
a set of 728 storms on which to try and train a model.  

The regression models I applied to the data didn't fare so well. 
Despite trying out feature-shrinking options like Lasso and Ridge, ordinary Linear Regression was my best option 
for predicting the damage value, with an R<sup>2</sup> value of 0.206. 
Predictions were off my a root-mean-square amount of $692 million. 
In the context of $125 billion dollar storms like Hurricane Harvey this is hardly inaccurate, but it reflects 
that most storms cause a negligible amount of damage and that the prediction values aren't reliable. 
Meteorological data like the storm's highest attained category simply don't correlate with storm damage; 
my highest-correlated features barely surpass 0.21.  

![Gamma Distribution of Storm Costs]({{ site.url }}/images/metis_02_NOAA/StormsDistribution.png)

Taking a look at the storm damage values, it's clear that the distribution of damage values is very right shifted. 
The graph above shows the frequencies of storm costs for my dataset, where storms that do any damage at all 
are relative outliers. 
The same distribution appears even if I eliminate the values either below or above $1 billion, which 
fundamentally doesn't really square that well with some of the assumptions needed that underpin linear regression. 
To address this, I looked at using my model to predict the log<sub>10</sub> of storm cost, which bumped up the 
R<sup>$</sup> to 0.608 on the log value without increasing the RMSE of the cost predictions themselves. 

Engineers like myself love heuristics, and I had imagined this model as a quick way to use Hurricane 
meteorological data, something the NOAA can get live and reliably, to produce "back of the envelope" 
numbers forecasting the need for government aid and the ensuing property damage. 
Looking at how the [Congressional Budget Office calculates damage estimates](https://www.americanbar.org/content/dam/aba/images/disaster/51610-Hurricanes_WP.pdf) 
it's clear that more features could improve on the high bias estimates I'm currently getting. 
The government's method takes into account topograhical vulnerability, population density, and the amount of 
coastal development to give state-specific damage estimates. 
Combined with targeted wind and precipitation numbers, these topographic and demographic considerations 
increase the reliability of damage estimates.  

When I get the time to revisit this project, I'm looking forward to trying out some new methodologies. 
Other algorithms like Generalized Linear Models (GLM's) can better mimic the gamma distribution of target values. 
Since most storms in this database cause minor damage at most, this might also be better as a classification problem 
that leverages concepts from anomaly detection to identify high damage storms, rather than the damage value itself.  
