---
layout: post
title: Taking the Plunge into Data Science
---

In nearly every opportunity I've had thus far, professional or otherwise, I've been asked to jump into the job with little direct experience and learn on the fly.
That trend continued last week while going through the first week of the Metis Data Science immersive bootcamp, and I couldn't be happier.  

We dove right into exploratory data analysis, the process that transforms an idea into a working project.
This is a fundamental component of scoping out a project: you determine whether the necessary data exists, clean out a myriad of possible errors and inconsistencies,
and visualize the remaining data in different ways to get a sense of what patterns may lay within.
While there are a plenty of pitfalls for a project at this stage, it's inherently fun.
Exploring the data is an opportunity to manifest all the "what if" questions that pop up while thinking about a topic.

## EDA with a purpose

Let's say you want to send out volunteers to drum up excitement for a fundraising event in New York City.
The organization is advancing the cause for more women in tech, and they want your help.
How do you go about providing a recommendation?  

We looked at the NYC Metro Transit Authority's [data](http://web.mta.info/developers/turnstile.html) on subway turnstiles to deduce the busiest stops in the city.
[Pandas dataframes](https://pandas.pydata.org/) made reading in and structuring the data much more palpable.
We developed distinct processes for cleaning the data and then grouping it so as to generate time series ridership data for individual stations.
The figure below ranks the top 10 stations by average daily total of entries and exits.  
 
![Ridership Insights from MTA Data]({{ site.url }}/images/metis_01_MTA/stations_filtered.png)

The data science process, however, isn't just about pure number crunching and taking your results at face value.
In an alternative to foot traffic data, we also leveraged the fact that [96% of the tech companies in NYC](https://www.builtinnyc.com/2016/12/13/big-tech-companies-nyc-locations)
are located in a roughly triangular area covering much of the middle and lower west side of Manhattan.
Referencing station coordinates, we filtered for heavy traffic stops near the demographic most interested in the client's cause.
The above bars in blue represent stations outside of the relevant areas.  

If you want to target stations purely by foot traffic, consider:
* 34th St - Penn Station
* 42nd St - Grand Central Station
* 34th St - Herald Square

There is also plenty of opportunity in relatively high traffic stations near a nucleus of tech companies:
* Fulton St
* stations along 23rd St

What has struck me the most since completing the project is just how many different ways other people have come up with to answer the same question.
During the presentations this past Friday, other classmates looked at targeting affluent parts of town, identified correlations (or lack thereof) with the weather,
and created interesting visualizations for the results. I'm excited to see what else this current cohort comes up with going forward.

## Content in the Pipeline

When the program wraps up this December, we'll have covered a large swath of content at a pretty good pace.
The machine learning algorithms, what I'm most excited about, are varied enough to get a fundamental understanding of the field:
* supervised learning (regression and classification)  
* natural language processing  
* unsupervised learning algorithms  
* deep learning  

To complement those concepts we'll touch on related tools and techniques like:
* web scraping techniques  
* processing costly tasks through AWS  
* SQL and NoSQL (MongoDB) database use  
* Data visualization with D3  
* big data tools like Spark and Hadoop    

This experience is all about learning by doing, and I'm looking forward to sharing future passion projects on this site.
