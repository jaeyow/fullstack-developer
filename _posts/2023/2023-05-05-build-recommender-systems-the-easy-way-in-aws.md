---
layout: posts
title: Build Recommender Systems the Easy Way in AWS
excerpt: Building and maintaining a recommender system that is tuned to your business' products or services can take great effort. The good news is that AWS can do the heavy lifting for you. Let's get started. 
modified: 2023-05-04
date: 2023-05-04
tags: [AI, ML, Recommender System, Recommender Engine, Recommendation System, Recommendation Engine]
header: 
  overlay_image: /images/amazon-personalize/rsz_hoover-tung-bslsdcqww0m-unsplash.webp
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: true
canonical_url: https://cevo.com.au/post/build-recommender-systems-the-easy-way-in-aws/
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

## Introduction

AWS provides users with the flexibility to build machine learning (ML) applications from scratch, but they also offer various high-level AI services that allow consumers to leverage the power of machine learning without any prior knowledge of the subject.

In this article, we will explore the fascinating world of recommender systems. As this is our first foray into this topic, let’s use an AWS service to speed up our ability to add recommendations into our product.

This AWS service is called [Amazon Personalize](https://aws.amazon.com/personalize/) - a fully managed and scalable AI service that simplifies the ability to add personalisation into your product. In fact, in this article, we will be adding recommendations to [an existing e-commerce application](https://github.com/cevoaustralia/cevo-shopping-demo), so we can see what is involved in this process. Towards the end of the article, we will also be doing a quick cost / benefit analysis to understand the upsides it can contribute to your business. 

However, before we dive into Amazon Personalize, let's take a step back and get a deeper understanding of the what, why and how of recommender systems.

## What are Recommender Systems?

A [recommender system](https://en.wikipedia.org/wiki/Recommender_system) (also called [RecSys](https://recsys.acm.org/)) is a sophisticated information filtering system that leverages user preferences, interests, and behaviours to provide personalised recommendations. It helps improve sales conversion and user retention by assisting customers find catalogue items they like but won't organically find, based on content they have already shown interest in.

## Why are Recommender Systems needed?

Recommender systems are valuable because they help users discover products, services, or content that they may not have otherwise found on their own. These systems use data analysis techniques to make predictions or suggestions based on several factors depending on the technique used. 
By providing personalised recommendations, these systems can improve user engagement and satisfaction, increase customer loyalty, and drive sales.
Let's look at how we identify relevant items through filtering.

## Recommender System Techniques

Recommender systems utilise various techniques, including content-based filtering, collaborative filtering, and hybrid filtering. Content-based filtering makes use of item attributes to recommend items that are similar to the ones the user has previously liked, answering questions like **"What items have I liked in the past, as I might enjoy similar items like that?"**

<figure>
	<a href="../images/amazon-personalize/content-based-filtering.webp"><img src="../images/amazon-personalize/content-based-filtering.webp"></a><figcaption>Content based filtering. image copyright Nvidia</figcaption>
</figure>

On the other hand, collaborative filtering analyses user behaviour and identifies users with similar preferences, answering questions like **"What do users similar to me like, as I might like these items too?"**

<figure>
	<a href="../images/amazon-personalize/collabrative-filtering.webp"><img src="../images/amazon-personalize/collabrative-filtering.webp"></a><figcaption>Collaborative filtering. image copyright Nvidia</figcaption>
</figure>

Hybrid filtering combines both approaches to provide more accurate and comprehensive recommendations, taking advantage of the strengths of each method.

Recommender systems are ubiquitous and are widely employed in e-commerce, online advertising, social media, and entertainment industries to enhance customer satisfaction, boost sales, and improve engagement. They are a valuable tool for businesses to offer personalised experiences to their users, leading to increased user engagement and loyalty.

## What is Amazon Personalize?

[Amazon Personalize](https://aws.amazon.com/personalize/), a ready-to-use AI service, is a recommender system that uses your data to generate item recommendations for your users. Amazon makes it easy by providing a system where you don’t even need to know much about machine learning; just feed it a user, an item and user-item interaction data, and you will be serving recommendations in your project in no time. 

## Challenges in building and maintaining a bespoke RecSys

There are multiple challenges to building and maintaining a bespoke recommender system. 

**Coverage** - With an ever increasing catalogue of items, user base and interactions, it's a challenge to maintain a model that can handle all that with low latency. 

**Adaptability** - Keeping data up to date is a challenge. In this case, the users, items and interactions data will need to be up to date using data pipelines that you will have to build and maintain yourself. The ability to ingest data in real time or through a batch process will need to be supported too. The system will need periodic training of the ML model as the data changes. 

**Cold starts** - The ML model has to handle user and item cold starts well. User cold start is when the logged-in user has just been added to the system, while item cold start is when a new product is added to it. In both these cases, they do not yet have any interaction history from which to draw the recommendations from. 

**Scalability** - The system should be able to scale to millions of users and products, each with their own list of interests and properties. 

**User preferences** - The system should be able to handle changing trends and preferences for the number of users in the system. 

**Evaluation** - A recommender system is not an install-and-forget system. They should be periodically evaluated with known metrics and retrained when model drift has been detected.

## Amazon Personalize Case Studies

Many satisfied customers have leveraged the power of Amazon Personalize to elevate their product offerings through effective personalisation strategies. Here are just a few:

<img src="../images/amazon-personalize/Warner-Brothers-Discovery_logo.769fd6aa6bd330ad7f45b4d2b8f3de79db29d92c-300x157.webp">

Warner Bros. Discovery, a premier global media and entertainment company, offers audiences the world's most differentiated and complete portfolio of content, brands and franchises across television, film, streaming and gaming.

>"Our team at Warner Bros. Discovery wanted to build a promotion engine to customize movie and show recommendations for unauthenticated users across our digital properties. We wanted to drive cross brand engagement as users traverse the brands and content across the WBD ecosystem. With Amazon Personalize we were able to build and train a real-time recommendation engine POC within two days. Since deployment on our TBS, TNT, TruTV and Adult Swim web properties, over 25k unique consumers have clicked on cross-portfolio promotions for the movies, shows and site sections recommended by Amazon Personalize. These promising results have paved the way for us to deploy our promo engine on CNN next month. For the users receiving personalized promotions we have seen total user engagement increase by 14% and cross brand engagement increase by 12% compared to a randomized control group. We have also observed a 2x to 3x increase in response rate using personalized promotions vs. simply promoting our most popular items to consumers. Amazon Personalize has been instrumental in showcasing content that our fans want to see more effectively across our various brands." - **Don Browning, VP Cloud Architecture, WBD**

<img src="../images/amazon-personalize/400w-lotte-mart.f00f83c2a5e02e084a418414de594d9e0a194ab6-300x188.webp">

Lotte Mart is a subsidiary of Lotte Conglomerate, the leading retail company in Korea. It operates hypermarket, members-only warehouse discount outlets, electronics digital shops, and toysRus stores in Korea. It has 187 stores in Korea, Indonesia and Vietnam.

>“By using Amazon Personalize, we have seen a 5x increase in response to recommended products compared to our prior big data analytics solution resulting in increased revenue per month. In particular, Amazon Personalize has increased the number of products that the customer has never purchased before up to 40%. The new recommendation service powered by AWS is the first of a much broader roll-out of AI technologies across our organization.” - **Jaehyun Shin, Big Data Team Leader, Lotte Mart**

<img src="../images/amazon-personalize/Intuit_Customer-Reference_Logo.2b56bca425e62e2ec721b5416f5477778099d7c1.png">

Intuit is a business and financial software company that develops and sells financial, accounting and tax preparation software and related services for small businesses, accountants and individuals.

>"With Amazon Personalize, we were able to quickly design and launch a recommendation engine for Intuit’s Mint budget tracker and planner app. Using customer profile and behavioral data, with machine learning, the service helps deliver the right financial offer to the right customer at the right time, based on their spending habits, lifestyle, and goals." - **Qiang Zhu, Director of Data Science, Intuit**

Please see more Amazon Personalize [customer successes here](https://aws.amazon.com/personalize/customers/).

## Can I use Amazon Personalize for my project?

The more user, item and user-item interaction data in your dataset, the better the recommendations that are returned by the system. As a guideline, for all use cases (domain dataset groups) and custom recipes, your interactions data must have the following:

A minimum of **1000 interactions records** from users interacting with items in your catalogue. These interactions can be from bulk imports, or streamed events, or both.
A minimum of **25 unique user IDs** with at least **two interactions** for each.
For quality recommendations, we recommend that you have at least **50,000 interactions** from **at least 1,000 users** with **two or more interactions each**.

## Adding product recommendations to an e-commerce app

One of the more common use cases for Amazon Personalize is to **add a recommender to an already existing e-commerce application**. It is a win-win situation for both the buyer and the seller; with effective recommendations, buyers will be delighted to use the application since the results are in sync to their preferences resulting in improved user engagement. Sellers on the other hand, will benefit with more clicks, better conversion and ultimately more profit. 

For the e-commerce domain, we have a selection of built-in Personalize use cases to choose from, including:
**Customers who viewed X also viewed** - Get recommendations for items that customers also viewed based on an item you specify.
**Frequently bought together** - Get recommendations for items that customers frequently buy together along with an item you specify.
B**est sellers** - Get recommendations for popular items based on how many times your customers purchased an item.
**Most viewed (Will be implemented in this article)** - Get recommendations for popular items based on how many times your customers viewed an item.
**Recommended for you (Will be implemented in this article)** - Get personalised recommendations for items based on a user you specify.
 
So, follow along in the next section to find out what is involved in creating recommenders for **Most viewed** and **Recommended for you** use cases and integrating them into an existing e-commerce application. 

## Method

### Step 0 - Identify sections in your codebase to call the recommender API 

For this article, I have created an e-commerce application so that we can have a project to apply recommendations with. [Here is the GitHub repo for the project](https://github.com/cevoaustralia/cevo-shopping-demo). The main page returns a list of products ranked in order of recommendation.

For users who are not logged in, or have logged in for the first time, there is no user-item interaction history, so this list of products represents the most popular products in the system. For all returning and logged-in users, it should return the recommended items based on the user and item history.

<figure>
	<a href="../images/amazon-personalize/rsz_100-cevo-shopping-demo.webp"><img src="../images/amazon-personalize/rsz_100-cevo-shopping-demo.webp"></a><figcaption>E-Commerce application</figcaption>
</figure>

### Step 1 - Generate Item, User, and Interaction Data

When working with machine learning in the AWS ecosystem, everything revolves around the S3 bucket. It is no different with high level AI services like Personalize where the following scripts [01-prepare-users.py](https://github.com/cevoaustralia/cevo-shopping-demo/blob/main/scripts/aws-personalize/01-prepare-users.py), [02-prepare-items.py](https://github.com/cevoaustralia/cevo-shopping-demo/blob/main/scripts/aws-personalize/02-prepare-items.py) and [03-prepare-interactions.py](https://github.com/cevoaustralia/cevo-shopping-demo/blob/main/scripts/aws-personalize/03-prepare-interactions.py) generate synthetic users, items and interactions data, in the form of csv files, and dump them into a known location in S3. 

In this e-commerce application, we have created **2,465 items or products**, **6,000 users**, and **675,000 user-item interactions**. 
<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.06-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.06-pm.webp"></a><figcaption>Users generation</figcaption>
</figure>
<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.25-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.25-pm.webp"></a><figcaption>Items generation</figcaption>
</figure>
<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.45-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-5.07.45-pm.webp"></a><figcaption>Interactions generation</figcaption>
</figure>

### Step 2 - Setup Amazon Personalize Datasets

Although these steps can all be done from the AWS console, I have done all these from python scripts so that they are easier to repeat, and so that you can easily add them to your CI/CD system, if needed.

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-23-at-9.20.13-am.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-23-at-9.20.13-am.webp"></a>
</figure>

This is the script for this step: [04-prepare-dataset-group.py](https://github.com/cevoaustralia/cevo-shopping-demo/blob/main/scripts/aws-personalize/04-prepare-dataset-group.py), where it creates items, user and interactions schema, in preparation for the creation of the recommenders in the next step. This is responsible for making Personalize understand the contents of the dataset we have just dumped into S3.

Now that the dataset’s schema has been created, it can now be imported into Personalize to get it ready for the training stage when the recommenders are created in the next step.

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-5.31.33-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-5.31.33-pm.webp"></a><figcaption>Getting the datasets ready</figcaption>
</figure>

Once the datasets have been imported and ready for the creation of recommenders, the dataset import can then commence. Once completed, the datasets will show a green tick and status as active, like in the next image:

<figure>
	<a href="../images/amazon-personalize/04-personalize-create-datasets.webp"><img src="../images/amazon-personalize/04-personalize-create-datasets.webp"></a><figcaption>Datasets are active</figcaption>
</figure>

### Step 3 - Create Recommenders

At this point, we can now create the recommenders, this is when the training happens, and this is done on the dataset that we have submitted to the item, user and interaction dataset group. Note that training time depends on the size of the datasets. In our example, training time takes about an hour.

<figure>
	<a href="../images/amazon-personalize/05-create-recommenders-inprogress-1.webp"><img src="../images/amazon-personalize/05-create-recommenders-inprogress-1.webp"></a><figcaption>Recommenders build in progress</figcaption>
</figure>

We have just created two recommenders:

**popular-items recommender**, which returns recommendations for the most popular items, and
**recommended-for-you recommender**, which returns predictions for a particular user

### Step 4 - Test your Recommenders

The python script below allows us to quickly test the recommended-for-you recommender. In line 15, we call the `get_recommendations` method of the Personalize runtime, passing the ARN for the recommended-for-you recommender, which is a parameter we stored in [System Manager Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html). We also pass the `userId` of the user we want to get the recommendations for. Finally, we specify the number of results we would like it to return.

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-6.06.30-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-6.06.30-pm.webp"></a><figcaption>Testing the recommenders</figcaption>
</figure>

### Step 5 - Add a recommender API 

[In our python backend](https://github.com/cevoaustralia/cevo-shopping-demo/blob/main/amplify/backend/function/getProducts/src/index.py), I have added [boto3 calls](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/personalize.html) to the recommenders that we have just created. In the function `get_recommended_items`, we are calling `get_recommendations` against the **recommended-for-you** recommender to return the recommended items for the specified user. 

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-6.19.14-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-6.19.14-pm.webp"></a><figcaption>Recommended for you recommender</figcaption>
</figure>

The python function `get_popular_items` uses the `get_recommendations` API call against the **popular-items** recommender to return popular items, notice that we are passing dummy user id ‘x’, so the call is not really for any particular user. 

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-6.18.57-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-6.18.57-pm.webp"></a><figcaption>Popular items recommender</figcaption>
</figure>

### Step 6 - Wire up your frontend to the recommender API

To wire the API call with the frontend, we simply pass the saved user id to the API call, and simply return the response. 

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-22-at-6.29.09-pm.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-22-at-6.29.09-pm.webp"></a><figcaption>Wire-up the recommenders from the front end</figcaption>
</figure>

So, if you select a shopper persona from the selection, the user id is passed to the API call, which calls the recommended-for-you recommender. This then returns the recommended items for this user. In this example, this user likes instruments, books and electronics, and on the header it will say “Inspired by your shopping trends” and the recommended items now return the recommended items from our recommender. 

<figure>
	<a href="../images/amazon-personalize/rsz_02-shopping-persona.webp"><img src="../images/amazon-personalize/rsz_02-shopping-persona.webp"></a><figcaption>Recommended items for user</figcaption>
</figure>

If you select another persona, for example, a user that has a liking for footwear, jewellery and furniture, this user will now get recommendations according to their personal inclinations.

<figure>
	<a href="../images/amazon-personalize/rsz_03-another-persona.webp"><img src="../images/amazon-personalize/rsz_03-another-persona.webp"></a><figcaption>Recommended items for another user</figcaption>
</figure>

Lastly, if no user persona is selected, the API just returns a list returned by the popular-items recommender, and in this case, a slice pepperoni pizza for dinner! 

<figure>
	<a href="../images/amazon-personalize/rsz_100-cevo-shopping-demo.webp"><img src="../images/amazon-personalize/rsz_100-cevo-shopping-demo.webp"></a><figcaption>Anonymous shopper or fist time logged in</figcaption>
</figure>

## How often do we train these recommenders?

Once both recommenders have been set up, they should then be ready to supply you with your recommendations. However, when new data is available such as when new users, items or interactions need to be added, [there are several methods](https://docs.aws.amazon.com/personalize/latest/dg/incremental-data-updates.html) of how they can be added to the system. 

For example, we can use the [Amazon Personalize Kafka Connector](https://github.com/aws/personalize-kafka-connector) to stream data in real time. However, if there is a large amount of historical records, the recommendation is to import the data in bulk, like what we did and then import the data individually as necessary.

Although available but not included in this demo, you can also stream real time interaction data using events, in particular the [PutEvents operation](https://docs.aws.amazon.com/personalize/latest/dg/recording-events.html#event-record-api), and the recommendations will reflect the data in real time. For example, we might want to update the model whenever a user adds items to the shopping cart, or when they check out their cart for payment. 

## How much does it cost to run, and how does it benefit me?

Let us estimate the setup and ongoing costs involved for the two recommenders we just added to our e-commerce application. Most of the costs involved are based on the amount of the time the recommender is running regardless of them serving recommendations or not. 

Here is a rough and conservative estimate using [AWS Cost calculator for Personalize](https://calculator.aws/#/addService/personalize) for each recommender, assuming a data ingestion of 1GB a month, 6,000 users, running 720 hours (24 hours, 7 days a week), and not going over the included free recommendations. One recommender per month costs **USD 270.05**, and **USD 540.10** monthly for both. 

Using the general understanding that using recommender systems lead to somewhere [between 10% to 25% increased revenue](https://www.youtube.com/watch?v=Eeg1DEeWUjA), if your revenue is $200,000 per month pre-recommendations, you can expect from **$20,000 to $50,000 sales monthly uplift** if you opted to use recommendations similar to what we did in this article.

For a recommender system that runs by itself, ingests data on the fly, re-trains automatically, where you don’t need to employ your own data science and machine learning team, and finally contributes more to your bottom line, AWS presents really great value here and is worth your consideration. 

<figure>
	<a href="../images/amazon-personalize/Screenshot-2023-04-23-at-9.35.34-am.webp"><img src="../images/amazon-personalize/Screenshot-2023-04-23-at-9.35.34-am.webp"></a><figcaption>Cost / Benefit analysis</figcaption>
</figure>

 Please see the [current pricing chart](https://aws.amazon.com/personalize/pricing/) for more details. 

## Conclusion

We've come to the end of our whirlwind introduction to recommender systems, where we've explored the high-level AI service in Amazon Personalize. However, we've only scratched the surface as this powerful service offers many more features.

For companies with limited resources, or organisations who want to extract value quickly, or when you want something out of the box, Amazon Personalize can be a viable option. With Personalize, we can easily bring machine learning-based personalization to existing e-commerce applications. By ingesting our own user, item, and interaction data, and building recommenders that seamlessly integrate into our codebase, we can create a fully managed recommender system that delights our customers and boosts our bottom line.

However, it's important to note that while Amazon Personalize is a powerful AI service, it's still a black box algorithm. It may not cover all specialised use cases, and building a custom recommender system from scratch might be necessary in these cases. Nevertheless, for many e-commerce businesses, high level AI services like Amazon Personalize offer the quickest way to derive value by using machine learning to solve real business problems.

Note: This article was originally published on [Cevo Australia's website](https://cevo.com.au/post/build-recommender-systems-the-easy-way-in-aws/)

## References

- [What's New in Recommender Systems](https://aws.amazon.com/blogs/media/whats-new-in-recommender-systems/)
- [Recommendation System Nowadays](https://qymatix.de/en/recommendation-systems-nowadays/)
- [Amazon Personalize can now create up to 50% better recommendations for fast changing catalogs of new products and fresh content](https://aws.amazon.com/blogs/machine-learning/amazon-personalize-can-now-create-up-to-50-better-recommendations-for-fast-changing-catalogs-of-new-products-and-fresh-content/)
- [Recommender System](https://en.wikipedia.org/wiki/Recommender_system)
- [Recommendation System](https://www.nvidia.com/en-us/glossary/data-science/recommendation-system/)
- [Incrementally update a dataset with a bulk import mechanism in Amazon Personalize](https://aws.amazon.com/blogs/machine-learning/incrementally-update-a-dataset-with-a-bulk-import-mechanism-in-amazon-personalize/)
- [Maintaining recommendation relevance](https://docs.aws.amazon.com/personalize/latest/dg/maintaining-relevance.html)


