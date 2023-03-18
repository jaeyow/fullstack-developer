---
layout: posts
title: Data Science Bootcamp - Week 3
excerpt: On the third week of the GA Data Science bootcamp, we explore ideas for the Capstone Project
modified: 2021-11-06
date: 2021-11-06
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

## Not Hotdog App

I still remember the moment that piqued my interest in Data Science. It was probably a couple of years ago, I saw this segment in a popular [HBO sitcom - Silicon Valley](https://en.wikipedia.org/wiki/Silicon_Valley_(TV_series)){:target="_blank"}, and I wasn't even following the series. I don't remember, but for some reason I found myself watching [this on Youtube](https://www.youtube.com/watch?v=pqTntG1RXSY){:target="_blank"}. So hilarious when Jian Yang first demoed the Not Hotdog app. But when I discovered that it was actually a real app that they developed for the series, I couldn't resist, but I had to find out exactly [how they made it](https://medium.com/@timanglade/how-hbos-silicon-valley-built-not-hotdog-with-mobile-tensorflow-keras-react-native-ef03260747f3){:target="_blank"}.

[![alt text](../images/general-assembly/hotdog-not-hotdog.png "Silicon Valley Seson 4")](https://www.youtube.com/watch?v=pqTntG1RXSY)

## Week 3 - More Pandas

This week, we spent more time getting deeper experience with [Pandas](https://pandas.pydata.org/), how data scientists use it to slice and dice data and effectively use it for exploratory data analysis. As we get to use it more, we get the appreciation of how indespensible it is at the stage of this data science end to end process. And one can undestand why data scientists love using Jupyter notebooks at this stage in the process too. 

The course instructor always talks about that in data science, one needs to build this **intuition**, of being able to find a problem that is worth solving where it's solution has an impact as well as identify if the data we have available is of good quality. And that we can have all the volume of data we want, and if it is no good, then they still belong in the rubbish bin. My goal, by the end of this course, is to not only complete the Capstone project, but more importantly, to be able to understand at least how to achieve that intuition that he keeps on talking about. 

## Capstone Project proposal due at the end of next week

With the Capstone Project proposal due at the end of next week, I've been thinking about different options, inspecting several available public datasets, and researching problems that people (myself included) are experiencing that can be solved with data science. Because my data science intuition needs some improvement, it's also worth noting that I need to come up with a few ideas, since not all are good ideas, or are problems that are able to be completed with the limited time available to me by the end of the bootcamp. 

The following are the possibilities:
 
### Amazon Pricing Data
 
I've been interested with pricing related Amazon data since I looked into Amazon Fulfilment by Amazon (FBA) a while back. There are several problems that 3rd party sellers would want answers for such as:

- what the optimum selling price is for your chosen category
- what the best strategy for product launch is
- which version of product description page will convert better
- which keywords and and how much to bid for the most optimum PPC campaign

### Residential Property Price Index Dataset

Australian house prices are notorious worldwide for being overpriced and unreachable for many. There is a public data available from [Australian Bureau of Statistics](https://www.abs.gov.au/) that show historical property price index for different states from mid 2000 up to the present. From this information, in combination with data from other datesets, we want to:

- Find out when and where best to purchase your residential property
- Predict house/unit prices 3 months from now
- Find out the best locality to purchase an investment property
- Does government subsidised housing improve housing affordability in the long term

### Formula 1 Dataset

Ever since the first season of [Drive to Survive](https://en.wikipedia.org/wiki/Formula_1:_Drive_to_Survive), I've been captivated by the drama and excitement that is Formula 1. I've been consuming this public API in some of my past blog posts ([DynamoDB and Single-Table Design](https://fullstackdeveloper.tips/so-how-do-you-start-with-dynamodb/), [Simple GraphQL consumer with Apollo Client](https://fullstackdeveloper.tips/easy-graphql-consumer-with-apollo-client/)) and I thought it was fitting to continue this trend and explore the instights that can be gleaned from it:

- of course I would like to predict the winner of the next race
- explore the effect of the weather on the outcome of the rece
- who wins the constructor at the end of the year
- who is the last place in the next race

### Marathon time Dataset

As I have been dabbling in marathons and triathlons, on and off through the years, this is also one my interests. For years I have been wondering:

- what if can accurately predict my finishing marathon time? 
- how about predicting middle distances like the 10K and 21K?
- what is the effect of missed training sessions to my finishing time? 
- what is the optimum pace throughout the race to achieve my best time? 

I will be submitting my **Capstone Project proposal** at the end of next week, and the ideas I have presented above, in one form or another will most probably be it!

## Resources
- [How HBO’s Silicon Valley built “Not Hotdog” with mobile TensorFlow, Keras & React Native](https://medium.com/@timanglade/how-hbos-silicon-valley-built-not-hotdog-with-mobile-tensorflow-keras-react-native-ef03260747f3){:target="_blank"}
- [Kaggle - Your machine learning and data science community](https://www.kaggle.com/){:target="_blank"}
- [Pandas - Open source data analysis and manipulation tool](https://pandas.pydata.org/){:target="_blank"}