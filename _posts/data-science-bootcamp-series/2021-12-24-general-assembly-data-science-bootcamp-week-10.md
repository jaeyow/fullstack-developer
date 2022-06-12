---
layout: posts
title: Data Science Bootcamp - Week 10
excerpt: Final week of the General Assembly Data Science bootcamp, and the Capstone Project has been completed!
modified: 2021-12-24
date: 2021-12-24
tags: [General Assembly Bootcamp, Data Science]
header: 
  overlay_image: /images/general-assembly/sajad-nori-xihagoynhn4-unsplash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: true
---
<section id="table-of-contents">
  <header>
    <h3>Overview</h3>
  </header>
  <div id="drawer" markdown="1">
  *  Auto generated table of contents
  {:toc}
  </div>
</section>

#### Part of the [General Assembly Data Science Bootcamp Series](../tags/#general-assembly-bootcamp)

[Github link to the full Capstone Project](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb){:target="_blank"}

![](https://raw.githubusercontent.com/jaeyow/f1-predictor/main/images/f1-mclaren-car.png)

## Capstone Project Recap

This is a recap of my Capstone Project where I describe in high level detail the process I went through to complete the course, and achieve a machine learning model that can predict the winner of a 2021 Formula 1 race.

Before the start of this bootcamp, I had beginner level Python, even though I had been developing software for many years. I had attempted an end-to-end Data Science project once before, but when doing these type of things on your own, these are bound for failure, at least for me.

I cannot emphasize this enough, that courses like this [GA Data Science bootcamp](https://generalassemb.ly/education/data-science/sydney){:target="_blank"}, will give you the best chance of achieving your goal. For me it was to be able to complete an end-to-end project. And I'm pretty proud of myself, but surely wouldn't have done it if not for the course, very capable and supportive instructors and equally curious cohorts.

### Problem Statement

Ever since the first season of [Drive to Survive](https://en.wikipedia.org/wiki/Formula_1:_Drive_to_Survive){:target="_blank"} , I've been captivated by the drama and excitement that is Formula 1. I've been consuming this public API in some of my past blog posts and I thought it would be fun to continue this trend and explore the insights and predictions that can be gleaned from past race data:

- predict the race winner in a race
- explore the effect of factors such as Constructor/team membership, weather, home circuit advantage, age/years of experience of driver, qualifying position, etc on the outcome of the race

Even though this post is just skimming the surface, and is really meant as a high level summary, there are still lots of details in it, and will not be very interesting for many of you. If you are in this boat, please fast forward to the [conclusion](#conclusion) to skip through all the details.

### Data Sources

[Ergast Motor Racing](http://ergast.com/mrd/) has been publishing these Formula 1 results from 1950 up to the present. Majority of my data set will be from this API. 

I will also be scraping some data from the following sites:
- [Chicane F1](https://chicanef1.com/){:target="_blank"}  - Since 1997 this website has been publishing F1 Race statistics and may have some data that is missing in the Ergast API. I did not end up needing data from this site after all, but it does have some race insights which are handy to know, like this [2021 points graph](https://chicanef1.com/graphpts.pl?year=2021){:target="_blank"} .
- [Wikipedia](https://en.wikipedia.org/){:target="_blank"}  - Weather information is missing in the Ergast data set and this can be scraped from Wikipedia
- [World Weather Online](https://www.worldweatheronline.com/){:target="_blank"}  - some weather information is also missing from Wikipedia, so we can use WWO as a backup
- [F1 Metrics](https://f1metrics.wordpress.com/){:target="_blank"}  - We are not really using any dataset from F1 Metrics, however, the author of this blog had so many past predictions and analysis, that I felt it important to consider his domain knowledge as I develop the machine learning models in this project. It is a shame that his blog updates are few and far between, however when he does, it's gold.

### What's Machine Learning again?

I've been a developer for some time now, and for a while I've been fascinated by machine learning. In software development, I can make computers do what I want, by programming them. However, in machine learning, you are not and cannot do that.

>In machine learning, you need to prepare your data in such a way so that when you show this data to your algorithms, it can understand and see the patterns and can come to a conclusion, without being explicitly programmed to do so.

This is the part that perplexed me from the start, its kind of smoke and mirrors. However having successfully gone through the process, it all makes sense to me now. And working on another end-to-end project by myself is not that unconceivable anymore.

### Feature Engineering, Importance and Selection

Although the data that we extracted from Ergast is great, it needs to be improved upon if we want to be able to successfully predict the race winner. Apart from the weather information that I scraped from an external source (Wikipedia), we already had all the data we need. We just needed to create "features" from the data already there. In Data Science, we call this Feature Engineering. If you want to see how I did these, [please check it out here](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb#feature_eng){:target="_blank"}. At the end of this process, I had about 110 features. 

![](/images/general-assembly/f1-feaure-importance.png)

Next is to determine the importance of these features, since we don't want to use all of them in the modelling stage. During this Feature Importance stage, we identify the most important and relevant features, and drop the rest. All these processes are all done with Python, here's what I did to quantify the [feature importance](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb#feature_importance){:target="_blank"} of the data.

Finally, once we have identified the relevant features, we can now safely drop the inconsequential features (that just contributes to model bloat), and keep the most significant ones. And finally, at this stage we are now ready to build our models. 

### Regression or Classification

We have a multitude of machine learning algorithms that we can use to build our model. Since this is my first attempt I wanted to use as many models as I can. At this stage I didn't really know about any of them, much less building one that can do predictions!

In this project we used 2 types of Supervised machine learning techniques. One is called [Regression models](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb#regression_approaches){:target="_blank"} , where this type can predict a continuous number like the finishing order. The second type is called [Classification models](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb#classification_approaches){:target="_blank"} , where I used it to predict if a driver Wins a race, or Not. 

### Parameter search methodology

Python has made it relatively easy to build a model. There's a library called [Sci Kit Learn](https://scikit-learn.org/stable/){:target="_blank"}  open source and free, where building a model can be as easy as finding an appropriate algorithm, supply the data, and parameters, and train it with your training data. 

To find the most optimum parameters, this is called [Hyperparameter tuning](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters) in machine learning-speak. There are libraries to do this easily, however I have opted to do this manually using Python **for** loops. I have tried the automated way, but for this project, I got better results without it. 

I have actually combined my hyperparameter tuning with running the actual predictions, this took a while, and it depends on the type of algorithms you end up using, but for me initially it took more than 5 hours  (I left it running overnight), and found out later that one of the Classification models I used (SVM) was so slow, without much difference as the other models which were much quicker to train. So I ditched that, and for all the models I used (**15 in total** including the Dumb Classifier), it took about **1.7 hours** using my trusty old MacBook Pro. 

![](/images/general-assembly/f1-summary-table.png)

## Conclusion

![](/images/general-assembly/f1-model-summary.png)

Following our [Champion/Challenger](https://medium.com/@awaiskaleem/mlflow-tips-n-tricks-eb1ac013edd1) methodology, the winning model is the one built with [Bagging Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.BaggingRegressor.html) ([Decision Tree Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html?highlight=decisiontree#sklearn.tree.DecisionTreeRegressor)). This is an ensemble model fron SKLearn which uses DecistionTreeRegressor as its base estimator.

[Neural Network - MLP Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html?highlight=mlp#sklearn.neural_network.MLPRegressor) ended up with the same precision score, however because it took 10x more in training time, I have delegated it to 2nd place. 

- Bagging Regressor (Decision Tree Regressor)
- Train time: 0.97s
- Test time: 0.42s
- **Grid**, **ConstructorRecentForm**, **DriverRecentForm** and **DriverRecentWins** round out the most significant features. The last 3 are one of the features we engineered for this project.
- Precision score: **61.9%**
- For each race, the finishing order is also available, but omitted here for brevity
- Correctly predicting the winner in **13 out of 21** races in 2021 Season

## What's next
- automate the training, building and deploying the model
- create an API that exposes this functionality to
- a web application allowing others to interact with it
- get more exposure to other types of machine learning projects and domains. The F1 prediction project is but a tiny speck in the machine learning/AI universe. 
- keen to volunteer or collaborate with a worthwhile project that needs my help

[Github link to the full Capstone Project](https://nbviewer.org/github/jaeyow/f1-predictor/blob/main/final-project-part3-technical-notebook.ipynb){:target="_blank"}

## Resources
- [Formula 1 Race Predictor](https://towardsdatascience.com/formula-1-race-predictor-5d4bfae887da){:target="_blank"}
- [F1 Metrics](https://f1metrics.wordpress.com/){:target="_blank"}
- [Predicting the Results for the World’s Most Expensive Sport](https://medium.com/@ajleo899/predicting-the-results-for-the-worlds-most-expensive-sport-102e7bc97b25){:target="_blank"}
- [Who’s The Best Formula One Driver Of All Time?](https://fivethirtyeight.com/features/formula-one-racing/){:target="_blank"}
