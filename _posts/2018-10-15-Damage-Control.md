---
layout: post
title: Proactive Damage Control
---

It's been a busy season for Atlantic hurricanes. Hurricane Florence, a category 4 storm at its peak,
dumped nearly 36 inches of rain on the Carolinas en route to causing more than $13 billion dollars in damage.
Despite having weakened to a Category 1 storm by the time it made landfall in the US, it was one of the wettest
tropical storms on record.
Last week, Hurricane Michael was the first ever storm to make landfall in the Florida gulf coast as a Category 4 hurricane. Peak winds of 155 mph and a strong storm surge contributed to damage estimates of over $8.1 billion. The season's not over quite yet, and currently we're looking at more than $21 billion in total damages and more than 80 people dead as a result. While we're pretty insulated from the effects of Hurricanes up in Chicago, I wanted to take some of the regression techniques we've been learning at Metis to try and anticipate the damage these storms cause. Being able to proactively identify when these storms will inflict severe damage would hopefully allow agencies like FEMA to allocate resources efficienty and be on the scene when residents need them the most.  

Like many government agencies, the National Oceanic and Atmospheric Administration has a treasure trove of data at their disposal. I took storm time series data from 1851 until the present from the HURDAT database and aggregated those 6-hour measurements into overall storm characteristics on windspeed, pressure, windspeed radius, duration, and distance travelled, to name a few.
Cost estimates for each storm can be found in individual NOAA Hurricane Center after action reports, although thankfully those reports are cited in the annual tables on Wikipedia for 1968 onwards.
I scraped these cost values into a Pandas dataframe and merged them with the meteorological data to get a set of 728 storms on which to try and train a model. 

The regression models I applied to the data didn't fare so well. Linear Regression was my best option for predicting the damage value, with an $R^{2}$ value of 0.206. Predictions were off my a mean amount of $692 million.
In the context of $125 billion dollar storms like Hurricane Harvey this is hardly inaccurate, but it speaks to the fact that most storms cause a negligible amount of damage and that the prediction values aren't reliable. Meteorological data like the storm's highest attained category simply don't correlate with storm damage, my highest feature coming in at a measly 0.20 correlation.

[Storm Damage Histogram]

Taking a look at the storm damage values, it's clear that right data is very right shifted. The graph above shows the frequencies of storm costs for my dataset, where storms that do any damage at all are relative outliers. The same distribution appears even if I cut off the values either below or above $1 billion, which fundamentally doesn't really square that well with some of the assumptions needed that underpin linear regression. To address this, I looked at using my model to predict the $log_{10}$ of storm cost, which bumped up the $R^{2}$ to 0.608 on the log value without increasing the RMSE of the cost predictions themselves.

Engineers love heuristics, and I had imagined this model as a quick way to use Hurricane meteorological data, something the NOAA can get live and reliably, to produce "back of the envelope" numbers forecasting the need for government aid and the ensuing property damage.
Looking at how the [Congressional Budget Office calculates damage estimates](https://www.americanbar.org/content/dam/aba/images/disaster/51610-Hurricanes_WP.pdf) it's clear that more features could improve on the high bias estimates I'm currently getting.
The government's method takes into account topograhical vulnerability, population density, and the amount of coastal development to give state-specific damage estimates. Combined with targeted wind and precipitation numbers, these topographic and demographic considerations increase the reliability of damage estimates.

When I get the time to revisit this project, I'm looking forward to trying out some new methodologies. Other algorithms like Generalized Linear Models (GLM's) can better mimic the gamma distribution of target values. Since most storms in this database cause minor damage at most, this might also be better as a classification problem that leverages concepts from anomaly detection to identify high damage storms, rather than the damage value itself.
