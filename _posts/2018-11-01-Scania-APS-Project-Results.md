---
layout: post
title: Scania Trucks Classification Project
---

![Scania promotional poster]({{ site.url }}/images/metis_03_Scania/Scania_background.jpg)

The trucks in the above picture are made by a Swedish company, Scania, that produces commercial vehicles.
Back in 2016, they proposed a challenge at the [15th International Symposium on Intelligent Data Analysis]
(http://ida2016.blogs.dsv.su.se/):
given an assortment of features, could any aspiring data scientist predict whether or not the 
air presssure system (APS) had failed? The APS controls a heavy truck's ability to break, so getting this
prediction right has clear consequences both in maintenance costs and for employee safety.

Talk about previous submission scores on a high level. Say that mine is slightly better. Show differnce in cost.

Talk about the custom cost function Scania provided and how it heavily penalizes Type II errors. Demonstrate 
that the easiest way to optimize is to lower the threshold enough so that the model becomes extremely sensitive 
to any potential possibility of failure, but not low enough so as to predict to check everything.

![Dynamic Confusion Matrix]({{ site.url }}/images/metis_03_Scania/confusion_threshold_animation.mov)

Show that data doesn't separate neatly, hence in order to minimize the cost and reduce missed APS failures
it's cost-effective to perform more unnecessary checks.

![PCA Data Visualization]({{ site.url }}/images/metis_03_Scania/3_D_data_vis.mov)

Explain that I leanred a lot about data imputation, PCA, classification modelling, and types of errors that I'll go into more depth on in a future post.