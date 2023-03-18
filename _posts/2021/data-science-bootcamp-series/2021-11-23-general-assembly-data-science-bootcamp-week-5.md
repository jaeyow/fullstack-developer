---
layout: posts
title: Data Science Bootcamp - Week 5 & 6
excerpt: Fifth and Sixth week, and we are now working with Machine Learning algorithms and a Capstone Project update
modified: 2021-11-23
date: 2021-11-23
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

## What is the difference between Statistics and Machine Learning?

Who knew!? I never knew they were different until I've attended this course!

> “The major difference between machine learning and statistics is their purpose. **Machine learning models** are designed to make the most accurate **predictions** possible. **Statistical models** are designed for **inference** about the relationships between variables.”

<figure>
	<a href="https://en.wikipedia.org/wiki/Statistics">
    <img src="../images/general-assembly/seaborn-sample-pairplot.png">
  </a>
  <figcaption>Statistics VS Machine Learning</figcaption>
</figure>


<figure>
	<a href="https://becominghuman.ai/an-introduction-to-machine-learning-33a1b5d3a560">
    <img src="../images/general-assembly/machine-learning.png">
  </a>
  <figcaption>Machine Learning VS Statistics (Copyright becominghuman.ai)</figcaption>
</figure>


It is still a bit unclear to me because the the lines are really blurred with both overlapping in capabilities. Perhaps this is best shown by explaining what the difference is between **inference** and **prediction** by means of an example. 

### Prediction

When we aim to predict the outcome of a future race, as in the case of my Capstone Project, this is an example of a prediction, fairly obvious there. In applying machine learning techniques, we typically train the machine learning model using a training/test set. When we need to make a prediction, we pass the input variables to the model, and we expect the prediction as the output of that model.

Machine learning is better at predictions, but it can also do a good job in inference. 

### Inference

Inference, is similar, but with a subtle difference. For example, you are a Data Scientist in the Formula 1 organization, and it has been decided that a new race will be added to the Global calendar. Your boss approached you with this problem - *Can you create a statistical model that can infer which country/where the best location of that new race is going to be?*

This differs from prediction, because we are not actually predicting something, however, we are somewhat creating an outcome based on past and current data to find relationships, and come up with the best country/location for the next race. 

Statistical modeling tend to be better at making inferences, but they can also be good in making predictions.

Clear as mud, right? 

## Assignment #2 due Monday last week

I originally planned to write something about this Data Science bootcamp every week, and up until last week I intended to. However, many things conspired that I was not able to complete that. We were also required to submit our EDA (Exploratory Data Analysis) assignments that weekend, plus a few other things, so something's got to give. 

## Special Guest this week

This week, we had a special guest brought in by our instructor. A Senior Data Scientist from a well known international tech company came in an gave us an hour and a half talk regarding his Data Science journey.

With a smart and resourceful personality, but what was more exciting was that he was also talking about his recent Data Science projects, both at his work, and more interestingly, his personal projects. Seeing these gave us cohorts that dose of motivation to soldier on with the rest of the course, well at least for me, that's for sure! 

## Update on the Capstone project
 
 So yeah, I am well and truly into my Capstone project. I have started getting all the required data from my sources. Instead of taking the easier way of just downloading data from sites like [Kaggle](https://www.kaggle.com/) and [Google Dataset](https://datasetsearch.research.google.com/), I have decided to find and extract and transform all the data myself. I have to experience how if feels to go through the process. I feel that this is the only way to learn. 

 I have also dumped all the race and results data to a [MongoDB](https://www.mongodb.com/) collection. It's been a long time since the last time I have tinkered with Mongo, but just the same, it's still easy and wonderful to work with. I picked it, not really specifically for working with Python, but I am planning to write an API and application with the Capstone, if time permits. 

 Below is the script I used to prepare the race results Data Frame, the main data I would need to commence EDA:

{% highlight python linenos %}
def create_results_dataframe_from_mongodb_collection():
    db = connect.f1Oracle
    collection = db.results

    for_da_result = {'Season':[],'Round':[],'Race Name':[],'Race Date':[],'Race Time':[],'Position':[],
                     'Points':[],'Grid':[],'Laps':[],'Status':[],'Driver':[],'DOB':[],
                     'Nationality':[],'Constructor':[],'Circuit Name':[],'Race Url':[],
                     'Lat':[],'Long':[],'Locality':[],'Country':[]}
    for race in races:
        race_results = list(collection.find({'season':f"{race['season']}",'round': f"{race['round']}"}))
        for results in race_results:
            for item in results['Results']:
                for_da_result['Season'].append(f"{results['season']}")
                for_da_result['Round'].append(f"{results['round']}")
                for_da_result['Race Name'].append(f"{results['raceName']}")
                for_da_result['Race Date'].append(f"{results['date']}")
                for_da_result['Race Time'].append(f"{results['time']}" if 'time' in results else '10:10:00Z')
                for_da_result['Position'].append(f"{item['position']}")
                for_da_result['Points'].append(f"{item['points']}")
                for_da_result['Grid'].append(f"{item['grid']}")
                for_da_result['Laps'].append(f"{item['laps']}")
                for_da_result['Status'].append(f"{item['status']}")
                for_da_result['Driver'].append(f"{item['Driver']['givenName']} {item['Driver']['familyName']}")
                for_da_result['DOB'].append(f"{item['Driver']['dateOfBirth']}")
                for_da_result['Nationality'].append(f"{item['Driver']['nationality']}")
                for_da_result['Constructor'].append(f"{item['Constructor']['name']}")
                for_da_result['Circuit Name'].append(f"{results['Circuit']['circuitName']}")
                for_da_result['Race Url'].append(f"{results['url']}")
                for_da_result['Lat'].append(f"{results['Circuit']['Location']['lat']}")
                for_da_result['Long'].append(f"{results['Circuit']['Location']['long']}")
                for_da_result['Locality'].append(f"{results['Circuit']['Location']['locality']}")
                for_da_result['Country'].append(f"{results['Circuit']['Location']['country']}")


    return pd.DataFrame(for_da_result)

results_df = create_results_dataframe_from_mongodb_collection()
results_df

{% endhighlight python %}

### Capstone Dataset

[Ergast Motor Racing](http://ergast.com/mrd/) has been publishing these Formula 1 results from 1950 up to the present. Majority of my data set will be from this API. 

I will also be scraping some data from the following sites:
- [Chicane F1](https://chicanef1.com/) - Since 1997 this website has been publishing F1 Race statistics and may have some data that is missing in the Ergast API
- [Wikipedia](https://en.wikipedia.org/) - Weather information is missing in the Ergast data set and this can be scraped from Wikipedia
- [World Weather Online](https://www.worldweatheronline.com/) - some weather information is also missing from Wikipedia, so we can use WWO as a backup
- [F1 Metrics](https://f1metrics.wordpress.com/) - We are not really using any dataset from F1 Metrics, however, the author of this blog had so many past predictions and analysis, that I felt it important to consider his domain knowledge as I develop the machine learning models in this project. It is a shame that his blog updates are few and far between, however when he does, it's gold. 

### Capstone Problem Statement

Ever since the first season of [Drive to Survive](https://en.wikipedia.org/wiki/Formula_1:_Drive_to_Survive), I've been captivated by the drama and excitement that is Formula 1. I've been consuming this public API in some of my past blog posts and I thought it would be fun to continue this trend and explore the insights and predictions that can be gleaned from past race data:

- predict the podium placers (1st, 2nd, 3rd) in a race
- predict the winner (pole-position) in a qualifying race
- predict who wins the fastest lap in the race
- who wins the constructor at the end of the year
- explore the effect of factors such as Constructor/team membership, weather, home circuit advantage, age/years of experience of driver, qualifying position, etc on the outcome of the race

## Resources
- [Statistics vs Machine Leaning, fight!](http://brenocon.com/blog/2008/12/statistics-vs-machine-learning-fight/){:target="_blank"}
- [A Brief History of Machine Learning](https://www.dataversity.net/a-brief-history-of-machine-learning/#){:target="_blank"}
- [The Actual Difference Between Statistics and Machine Learning](https://towardsdatascience.com/the-actual-difference-between-statistics-and-machine-learning-64b49f07ea3){:target="_blank"}