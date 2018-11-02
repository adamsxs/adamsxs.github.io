---
layout: post
title: Scania Trucks Classification Project
---

![Scania promotional poster]({{site.url}}/images/metis_03_Scania/Scania_background.jpg)

The trucks in the above picture are made by a Swedish company, Scania, that produces commercial vehicles.
Back in 2016, they proposed a challenge at the [15th International Symposium on Intelligent Data Analysis](http://ida2016.blogs.dsv.su.se/):
given an assortment of features, could any aspiring data scientist predict whether or not the 
air presssure system (APS) had failed? The APS controls a heavy truck's breaks, so getting this
prediction right has clear consequences both in maintenance costs and for employee safety.

The [top submission](https://www.kaggle.com/uciml/aps-failure-at-scania-trucks-data-set#aps_failure_description.txt) 
to the symposium had an error score of 9920. I'm able to drop that score down to 8110 by using a Random Forest 
classifier from the Python Scikit-Learn module and then lowering the threshold at which the classifier predicts
an APS failure has occured.  

The main driver for minimizing the score comes down to how Scania wanted to weight different types of classification errors.
Missing a broken APS and running the risk of it breaking down on the road, a type II error, is rated as 50 times more
costly than performing an unnecessary check because of a false positive.
In effect, the easiest way to optimize is to lower the threshold enough so that the model becomes extremely 
sensitive to any potential possibility of failure, but not sensitive enough so as to predict a failure on everything.

![Dynamic Confusion Matrix]({{site.url}}/images/metis_03_Scania/confusion_threshold_animation.mov)

The above clip shows the confusion matrix, a visualization of the possible predictions and errors a binary 
classification model can make.
Focusing on the top right and bottom left numbers, it's clear that lowering the decision threshold leads to a 
significant increase in unnecessary checks by the mechanics but is cheaper for the company since fewer trucks
break down en route.
Adjusting model parameters, like the number of different decision trees to run in the random forest model, 
contributed to minimizing error but had less of an impact overall than tuning the decision threshold.

Making the model this sensitive to any potential signs of the positive class may seem like overkill, but it's 
helpful to look at the data while keeping that in mind. 
Using Principal Component Analysis (PCA), it's possible to reduce the data down from about 140 features to 3 
"principal components" that capture most of the variation in the data. 
The 3D scatter plot of those three principal components was made in Plotly for 5000 of the examples in the test set. 
While it may not be fully representative of the 140+ dimensional hyperplane on which the data actually exists, 
it's illustrative for showing that there isn't a clear demarcation between the classes. 
Minimizing the number of false negatives is going to produce a surge in false positives.  

![PCA Data Visualization]({{site.url}}/images/metis_03_Scania/3_D_data_vis.mov)

All said and done, there's still plenty to dig into here for steps in the project. 
I'll look to do a more thorough walkthough in the future, but for now I'm happy getting a score that's better 
than the original symposium submissions. 
[Feel free to check out my notebooks and code.]('https://github.com/adamsxs/metis_project_03')
I had a lot of fun learning about
different ways to impute data, about PCA, modularizing my Python functions, and the tradeoffs that different types 
of classification errors can have for a business case. 
