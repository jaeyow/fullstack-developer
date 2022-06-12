---
layout: posts
title: Data Science Bootcamp - MLOps on the cheap!
excerpt: Using [Github Actions](https://github.com/features/actions){:target="_blank"} as a practical (and Free<sup>*</sup>) MLOps Workflow tool for your Data Pipeline. This completes the [Data Science Bootcamp Series](https://fullstackdeveloper.tips/tags/#general-assembly-bootcamp){:target="_blank"}
modified: 2022-01-02
date: 2022-01-02
tags: [General Assembly Bootcamp, Data Science, MLOps]
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

[Github link to the full Capstone Project](https://github.com/jaeyow/f1-predictor){:target="_blank"}

![](https://raw.githubusercontent.com/jaeyow/f1-predictor/main/images/f1-mclaren-car.png)

## What is MLOps?
After recently finishing the Capstone Project, one of the "What's Next" actions that I have identified was to:

- automate the training, building model deployment
- create an API that exposes this functionality

After looking into this a little bit more, I realized that there is a term for this activity - [MLOps](https://towardsdatascience.com/what-is-mlops-everything-you-must-know-to-get-started-523f2d0b8bd8){:target="_blank"} - the crossover of [Machine Learning](https://towardsdatascience.com/machine-learning-an-introduction-23b84d51e6d0){:target="_blank"} and [DevOps](https://www.atlassian.com/devops){:target="_blank"}. This relatively new term is defined by [Towards Data Science](https://towardsdatascience.com/what-is-mlops-everything-you-must-know-to-get-started-523f2d0b8bd8) as:

> It is an engineering discipline that aims to unify ML systems development(dev) and ML systems deployment(ops) to standardize and streamline the continuous delivery of high-performing models in production.

And there is more to MLOps than just that, in fact listed below are the other operations that are collectively grouped under the MLOps umbrella:
- data sourcing
- data preparation
- feature engineering 
- feature selection
- model training
- model selection
- model building 
- maintaining data pipelines
- deployment of model to production
- monitor, governance, optimize and maintain models

As you can see, model building is merely a tiny part in that process. To facilitate all these activities, there are many [MLOps tools](https://neptune.ai/blog/best-open-source-mlops-tools) available to us, however, there is a one tool popular to most developers which is curiously missing in that list - [GitHub Actions](https://github.com/features/actions)!

## OK, Let's use GitHub Actions, then!

There's not much ML resources using GitHub actions as an ML Workflow tool, but having used actions in previous projects, I know that with little work, it can be used satisfactorily, instead of more popular tools such as [Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-model-management-and-deployment) or [Apache Airflow](https://airflow.apache.org/). 

<script src="https://gist.github.com/jaeyow/9f9143d09c0438876b42da374982e5b5.js"></script>

In the GitHub workflow above, these are process we went through that ended up with our model deployed to an API in Production:

### Checkout latest code from source control

The model and ML workflow presented here are available in this [GitHub repo](https://github.com/jaeyow/f1-predictor){:target="_blank"}, free to reuse. Currently this is run manually, but can be easily run using a cron schedule, or as part of your CI workflow, through a Pull Request, or a repo update.

### Set up Python v3.8

You'll also notice that this workflow will be running on `ubuntu-latest`. This is what's great with using GitHub actions, is that get a selection of GitHub-hosted runners. And they are all [free<sup>*</sup>](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration){:target="_blank"}. All we need to do is select our preferred runner, and install all the dependencies that the workflow needs.

First is to install our preferred Python version and it's dependencies defined in `requirements.txt`

- Set up Node.js environment
- Upgrade Python and dependencies

### Install Chrome browser

Chrome is also required since part of our Feature Engineering is web scraping Wikipedia for some of the weather information. At some stage, we need Selenium to click on links, and further scrape those pages. 

### Run data sourcing scripts

Our data comes from [Ergast Motor Racing](http://ergast.com/mrd/){:target="_blank"}, so we read this API and dump the data into MongoDB. You'll notice that even though there are secrets involved, we are not sharing these in the actions yml file. 

### Run data preparation scripts

This is an intermediate step that classifies weather information into 6 weather types - getting it ready for the model building process. 

### Perform Feature Engineering

The data we got from Ergast is not ready as is, so we we had to engineer a few features. This is easy to do from our workflow by calling some custom-made Python functions. 

![](../images/general-assembly/feature-engineering.png)

### Build ML model and score

In the previous article we have identified the [most optimal ML model](https://fullstackdeveloper.tips/general-assembly-data-science-bootcamp-week-10/#){:target="_blank"} for this problem - Bagging Regressor (using Decision Trees), so in this step, we just build the model and generate the [Pickle file](https://docs.python.org/3/library/pickle.html){:target="_blank"} which our API will use to perform the on-demand predictions.

![](../images/general-assembly/model-building-scoring.png)

### Setup [Serverless](https://www.serverless.com/){:target="_blank"} framework

Serverless makes it easy to setup our AWS Lambda as a public API. I wanted to use [Pulumi](https://www.pulumi.com/), perhaps let's do this in another blog post. In the meantime, Serverless was the easiest and fastest way (for me) to push this to our production environment. 

![](../images/general-assembly/serverless-install.png)

### Deploy ML Model and API to production

The last but not the least! Certainly the most exciting part! The final part of the GitHub MLOps workflow is to be able to deploy our model (and the Serverless API) to production.

I have opted to use [Flask](https://flask.palletsprojects.com/en/2.0.x/), since I already had scripts in Python, so it was minimal work to adapt for the public API. 

![](../images/general-assembly/deploy-model-and-api.png)

Once deployed, the API is now available to the public. If time permits, I might create a web application that consumes this API, but because this is a public API, this is now ready for prime time!

![](../images/general-assembly/api-invocation.png)

## Conclusion

In this article, we have demonstrated the use of GitHub Actions, a general purpose GitHub-based CI/CD tool that many developers love. Although not a tool typically used for ML workflows, its general purpose nature, with little effort, it can be used in simple ML pipelines.

There are some limitations (eg. you don't want to use it with long-running ML tasks like exhaustive hyperparameter tuning), but in my opinion, it manages just fine for many ML scenarios. 

What's your ML workflow tool of choice?

What capabilities are missing in GitHub Actions as an ML workflow tool?

[Github link to the full Capstone Project](https://github.com/jaeyow/f1-predictor){:target="_blank"}

## Resources
- [What is MLOps — Everything You Must Know to Get Started](https://towardsdatascience.com/what-is-mlops-everything-you-must-know-to-get-started-523f2d0b8bd8){:target="_blank"}
- [GitHub Actions - Automate your workflow from idea to production](https://github.com/features/actions){:target="_blank"}
- [The Best Open-Source MLOps Tools You Should Know](https://neptune.ai/blog/best-open-source-mlops-tools){:target="_blank"}
