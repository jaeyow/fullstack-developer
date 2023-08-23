---
layout: posts
title: How to Build, Train and Deploy Your Own Recommender System – Part 2
excerpt: We build a recommender system from the ground up with matrix factorization for implicit feedback systems. We then deploy the model to production in AWS. 
modified: 2023-08-22
date: 2023-08-22
tags: [AI, AWS Lambda, AWS SAM, Comet, Implicit Feedback, Matrix Factorisation, Metaflow, ML, MLOps, recommender system]
header: 
  overlay_image: /images/matrix-factorization-recommender/rsz_anton-maksimov-5642-su-qm37iptlcny-unsplash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: true
canonical_url: https://cevo.com.au/post/how-to-build-train-and-deploy-your-own-recommender-system-part-2/
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

[In part 1 of this series](https://cevo.com.au/post/build-train-deploy-your-own-recommender-system/), we introduced how to build a recommender system (RecSys) using matrix factorisation for implicit feedback systems. We implemented a simple MLOps workflow using third-party tools [Metaflow](https://metaflow.org/) and [Comet](https://www.comet.com/docs/v2/), where we built up our RecSys through the parallel training of multiple models, tracking all experiment metrics, selecting the best model and finally pushing our best model to a model registry. 

In this article, we will:

- Introduce [Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/) as a way to deploy our Machine Learning model to production
- Learn about [Lambda](https://aws.amazon.com/lambda/) as a serverless option in AWS for many workloads including this RecSys. We immediately encounter a problem typical with Lambda and non-trivial systems like this RecSys, and a solution on how to overcome it
- Expose our backend machine learning model as a REST API using SAM
- Integrate our newly created RecSys to [the e-Commerce frontend](https://cevo.com.au/post/build-recommender-systems-the-easy-way-in-aws/) we developed in a previous blog post
- Bring all the things that we have learned from the start of this series, in a unified MLOps workflow with Metaflow, including the deployment to production
- Source code for the [Frontend](https://github.com/cevoaustralia/cevo-shopping-demo/tree/mf-rec) and [MLOps](https://github.com/cevoaustralia/matrix_factorization_recommender/tree/matrix-factorization-part-2) for this article is also available for you to follow.

## Model Registry

In part 1, after we trained the model, we performed a model evaluation to check the model’s correctness. That produced a metric that we can use to compare each build. We used [Comet’s python SDK](https://www.comet.com/docs/v2/api-and-sdk/python-sdk/getting-started/) to log the model, which we have pickled in an S3 destination. Once the model is logged in the experiment (please see line 20 below), it will now be part of the experiment together with all the metadata that it is made of. Please see [this Comet link](https://www.comet.com/docs/v2/guides/model-management/using-model-registry/) to read more details on how to use the model registry.

<figure>
	<a href="../images/matrix-factorization-recommender/log-model-with-comet.png"><img src="../images/matrix-factorization-recommender/log-model-with-comet.png"></a>
</figure>

Once a model has been logged into an experiment, it can then be registered into the model registry so that it can be shared with your team. This will then be easier to track your models, retrieve the model binaries, either through the Comet web interface, or further integrated into your team’s MLOps automation through the python SDK.

<figure>
	<a href="../images/matrix-factorization-recommender/inspect-registered-model.png"><img src="../images/matrix-factorization-recommender/inspect-registered-model.png"></a>
</figure>

## Serverless Application Model

I have decided to utilise [AWS Lambda](https://www.comet.com/docs/v2/guides/model-management/using-model-registry/) as our serverless solution for hosting our recommender system, opting to steer clear of managing servers, whether they are https://aws.amazon.com/ec2/ or docker containers in the cloud. Dealing with servers would be cumbersome for our small-scale system. While we could have taken the easy route and built our Lambda function and REST API using the AWS Console’s clickOps method, given the simplicity of our system, I wanted to challenge myself and delve into Infrastructure as Code (IAC), ensuring that our solution is maintained in source control.

<figure>
	<a href="../images/matrix-factorization-recommender/AWS-Serverless-Application-Model.jpg"><img src="../images/matrix-factorization-recommender/AWS-Serverless-Application-Model.jpg"></a>
</figure>

Initially, I considered using [Amplify](https://aws.amazon.com/amplify/), which had been successful for building our e-commerce application. However, configuring Amplify with single sign-on (SSO) posed some difficulties, prompting me to explore an alternative approach: the [Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/) – a framework for building serverless applications. I had been intrigued by SAM for some time, and now seemed like the perfect opportunity to give it a try.

To my surprise, SAM turned out to be open-source. I was impressed by its user-friendliness, a characteristic often found in well-supported open-source projects.

<figure>
	<a href="../images/matrix-factorization-recommender/sam-init-start.png"><img src="../images/matrix-factorization-recommender/sam-init-start.png"></a>
</figure>

## Houston, We Have a Problem!

AWS Lambda is often a compelling choice for building serverless applications, thanks to the built-in conveniences that eliminate the need for setting up and managing servers. When working with Python, AWS Lambda provides a runtime environment that we can leverage in our recommender system. However, as we built the project, we encountered some challenges:

While Lambda offers an extensive list of Python modules, essential libraries like numpy, scikit-learn, and [pandas](), commonly used in machine learning systems (some of which we use here), are notably absent.

Furthermore, Lambda has an uncompressed size limit of 250MB for function packages. These missing libraries that we needed, such as [numpy]() (108MB), [scipy](https://scipy.org/) (156MB), and [pandas](https://numpy.org/) (151MB), already exceed this limit. Considering we haven’t even accounted for the Implicit library yet, crucial for our matrix factorisation recommender, the size constraints become even more restrictive.

<figure>
	<a href="../images/matrix-factorization-recommender/lambda-layers-image.png"><img src="../images/matrix-factorization-recommender/lambda-layers-image.png" style="width:500px"></a>
</figure>

Adding these external libraries as [Lambda Layers](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-layer) is one option to bring them in. However, Lambdas are limited to five layers and exact size restrictions, which falls short of what we require for our recommender system.

At this point, it became evident that using Lambda Layers for our RecSys was not feasible. Luckily, AWS offers an alternative solution – Lambda Container Images!

## Enter Lambda Container Images

By adopting Lambda Container Images, which currently has a container size limit of 10GB, we gain the flexibility to package our application and all necessary dependencies into a custom container image. This way, we can include all the required libraries and modules, which will easily fit our required Python dependencies without any Lambda layer limitations. Container-Based Lambdas open up new possibilities for deploying our recommender system with ease and efficiency.

And because container-based Lambdas are supported in SAM, we now have a potential solution to try out! So I built such a lambda based mainly on an AWS tutorial. However, we’ve immediately hit a snag. 

Upon running a get request with [Postman](https://www.postman.com/), I got a runtime error:

> ImportError: libgomp.so.1: cannot open shared object file: No such file or directory…

This error came from our import of Implicit Library, and it was not happy with the dependencies included in the Lambda image.

<figure>
	<a href="../images/matrix-factorization-recommender/lambda-library-error.png"><img src="../images/matrix-factorization-recommender/lambda-library-error.png"></a>
</figure>

Asking the [Cevo Hive Mind](https://cevo.com.au/about-us/), I got my answer within a few minutes. All I needed to do was to yum install this dependency into our container, and that should resolve the error. And what do you know? It works! See line 4 in the Dockerfile below:

<figure>
	<a href="../images/matrix-factorization-recommender/matrix-factorization-dockerfile-1536x443.webp"><img src="../images/matrix-factorization-recommender/matrix-factorization-dockerfile-1536x443.webp"></a>
</figure>

## Deploying Matrix Factorisation Recommender in AWS Lambda

Now that we have successfully built our Lambda using SAM, it’s time to integrate it into our MLOps workflow. To achieve this, we revisit our Metaflow script and pinpoint the exact moment in the flow where we need to invoke SAM to deploy the model with the highest MAP@K score, as determined during the model evaluation.

<figure>
	<a href="../images/matrix-factorization-recommender/deploy-model-with-sam.png"><img src="../images/matrix-factorization-recommender/deploy-model-with-sam.png"></a>
</figure>

Before proceeding further, we must locate the winning model’s file and path. This information is crucial as we will use SAM to deploy this model onto our Lambda, making it accessible through a REST API. Fortunately, we can leverage Metaflow’s global variables, particularly the ‘self’ variable, along with dynamic parameters passed to SAM during stack deployment to accomplish this task. Line 12 below shows how to invoke SAM from a Metaflow script and pass the Lambda environment variable.

<figure>
	<a href="../images/matrix-factorization-recommender/deploy-best-model-sam-metaflow-2.png"><img src="../images/matrix-factorization-recommender/deploy-best-model-sam-metaflow-2.png"></a>
</figure>

Once we have obtained the path and location of our best model (we can also check the model registry for this information), the next step is to set our Lambda’s environment variable as described above, ensuring it’s readily available when the Lambda requires it. With these preparations complete, we can run our updated Metaflow script, which will run everything, including seamlessly deploying the best model onto AWS! Our next milestone is integrating this model with our front end, bringing us one step closer to achieving our mission of replacing AWS Personalize with our custom solution.

## Integrate Recommender with Frontend

At last, we have concluded our experiment’s culmination in building our very own recommender system. Looking back, it has been quite a journey. We began by acquainting ourselves with recommender systems, taking our first steps with Amazon Personalize. [In the prequel](https://fullstackdeveloper.tips/build-recommender-systems-the-easy-way-in-aws/), we even crafted a sample e-commerce web application to test it out. This initial experience provided a smooth entry into recommender systems, but we craved more.

[In Part 1](https://fullstackdeveloper.tips/build-train-deploy-your-own-recommender-system/), we decided to delve deeper and experiment with building our system. We opted for a simple matrix factorisation method, a simple embedding method, which, while not cutting-edge, offered valuable insight into how popular sites tackle this challenge.

In this final instalment, Part 2, we took the model we constructed in Part 1 and deployed it to a serverless infrastructure on AWS, using the open-source [Serverless Application Model](https://aws.amazon.com/serverless/sam/). This final leg of the journey brought us full circle as we integrated our recommender system into the original e-commerce web application we built in the first article.

<figure>
	<a href="../images/matrix-factorization-recommender/rsz_1floral-beauty-jewelry.png"><img src="../images/matrix-factorization-recommender/rsz_1floral-beauty-jewelry.png"></a>
</figure>

If you want to go and look back at the articles and source code for the whole series, here are some handy links:

[Build Recommender Systems the Easy Way in AWS](https://fullstackdeveloper.tips/build-recommender-systems-the-easy-way-in-aws/)
- [source code](https://github.com/cevoaustralia/cevo-shopping-demo/tree/main)

[How to Build, Train and Deploy Your Own Recommender System – Part 1](https://fullstackdeveloper.tips/build-train-deploy-your-own-recommender-system/)
- [source code – frontend](https://github.com/cevoaustralia/cevo-shopping-demo)
- [source code – MLOps](https://github.com/cevoaustralia/matrix_factorization_recommender/tree/matrix-factorization-part-1)

[How to Build, Train and Deploy Your Own Recommender System – Part 2](https://fullstackdeveloper.tips/build-train-deploy-your-own-recommender-system-part-2)
- [source code – frontend](https://github.com/cevoaustralia/cevo-shopping-demo/tree/mf-rec)
- [source code – MLOps](https://github.com/cevoaustralia/matrix_factorization_recommender/tree/matrix-factorization-part-2)

Note: This article was originally published on [Cevo Australia's website](https://cevo.com.au/post/how-to-build-train-and-deploy-your-own-recommender-system-part-2/)



