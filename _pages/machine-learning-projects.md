---
title: "Machine Learning Projects"
permalink: /machine-learning-projects/
layout: single
author_profile: true
toc: true
---

This space is for my projects that are related to Data Science and Machine Learning.

### How to Build, Train and Deploy Your Own Recommender System – Part 1

In [my previous blog post](https://cevo.com.au/post/build-recommender-systems-the-easy-way-in-aws/), we explored Amazon Personalize, a high level AWS service that gives you a product recommender system without building and hosting one from scratch. While it is very effective in getting you from zero to production in a very short time, it can also be an expensive exercise, especially as your users, products or user-product interactions grow. With these high-level services, the pricing structures are tied to the size of your system. There might also be privacy requirements that prevent you from using these services.

In this article, we will be building a recommender system from the ground up using a popular machine learning algorithm, similar to the one used in popular sites like Facebook and Spotify.

- [How to Build, Train and Deploy Your Own Recommender System – Part 1](/build-train-deploy-your-own-recommender-system/#)
- [GitHub Repo - How to Build, Train and Deploy Your Own Recommender System – Part 1](https://github.com/cevoaustralia/matrix_factorization_recommender/tree/matrix-factorization-part-1)

### Build Recommender Systems the Easy Way in AWS

AWS provides users with the flexibility to build machine learning (ML) applications from scratch, but they also offer various high-level AI services that allow consumers to leverage the power of machine learning without any prior knowledge of the subject.

In this article, we will explore the fascinating world of recommender systems. As this is our first foray into this topic, let’s use an AWS service to speed up our ability to add recommendations into our product.

This AWS service is called [Amazon Personalize](https://aws.amazon.com/personalize/) - a fully managed and scalable AI service that simplifies the ability to add personalisation into your product.

- [Build Recommender Systems the Easy Way in AWS](/build-recommender-systems-the-easy-way-in-aws/#)
- [GitHub Repo - Build Recommender Systems the Easy Way in AWS](https://github.com/cevoaustralia/cevo-shopping-demo)

### AutoML with Amazon Rekognition

This project is to explore the use of Amazon Rekognition for image classification. Amazon Rekognition is a high level AI service that allows you to perform image classification, object detection, face detection, face recognition, and text detection. I have created an end-to-end application using [AWS Amplify](https://aws.amazon.com/amplify/), [Amazon Rekognition](https://aws.amazon.com/rekognition/), and Amazon S3. This was to play around with the capabilities of this AutoML service.

- [Trying AutoML with Amazon Rekognition](/accelerate-ml-application-development-in-aws/#)
- [GitHub Repo - using Amazon Rekognition (Private Repo)](https://github.com/cevoaustralia/poc1-with-rekognition)

### Image Classification for the MNIST Dataset
In this project, we tackle the MNIST dataset using [Amazon SageMaker's](https://aws.amazon.com/sagemaker/) Linear Learner algorithm. We will use [Metaflow](https://metaflow.org/) to orchestrate the training and deployment of the model. We will also use [Github Actions](https://github.com/features/actions) to automate the process of training and deploying the model.

- [Going to Production with Github Actions, Metaflow and AWS SageMaker](http://localhost:4000/github-actions-metaflow-sagemaker/#)
- [GitHub Repo - using Amazon SageMaker Linear Learner](https://github.com/jaeyow/sagemaker-linear-learner)

### Formula 1 Race Prediction

My capstone project for the 3 month [General Assembly Data Science Bootcamp](https://generalassemb.ly/education/data-science-immersive/sydney) where we work on a Data Science problem and go through a process to achieve the desired outcome of being able to predict the winner of a Formula 1 race.

Data Science processes such as Exploratory Data Analysis, Feature Engineering, Regression Approaches, Classification Approaches, Feature Importance, Feature Selection, Models Comparison, and Model Selection. 

Also went through [MLOps](https://en.wikipedia.org/wiki/MLOps) using an unlikely tool in Github Actions - in this case where only the basics are required, it was enough (barely!). 

- [Data Science Bootcamp - Formula 1 Race Prediction](/general-assembly-data-science-bootcamp-week-10/)
- [Using Github Actions as a poor man's MLOps Tool](/general-assembly-data-science-bootcamp-mlops/)
- [GitHub Repo - end-to-end using Jupyter Notebook](https://github.com/jaeyow/f1-predictor)
- [GitHub Repo - end-to-end using Metaflow](https://github.com/jaeyow/metaflow-f1-predictor)






