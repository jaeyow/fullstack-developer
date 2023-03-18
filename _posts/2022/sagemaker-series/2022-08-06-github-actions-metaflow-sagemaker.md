---
layout: posts
title: Going to Production with Github Actions, Metaflow and AWS SageMaker
excerpt: A scalable (and cost-effective) strategy to transition your Machine Learning project from prototype to production
modified: 2022-08-05
date: 2022-08-05
tags: [Machine Learning, SageMaker, ML algorithms, Metaflow]
header: 
  overlay_image: /images/sagemaker-series/kevin-ku-w7zyugynprq-unsplash.jpg
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

Fully working source code is freely [available here](https://github.com/jaeyow/sagemaker-linear-learner).

## Three is a crowd

[Github Actions](https://github.com/features/actions), [Metaflow](https://metaflow.org/) and [AWS SageMaker](https://aws.amazon.com/pm/sagemaker/) are awesome technologies by themselves however they are seldom used together in the same sentence, even less so in the same Machine Learning project.

<figure>
	<a href="../images/sagemaker-series/sagemaker-linear-learner.png"><img src="../images/sagemaker-series/sagemaker-linear-learner.png"></a><figcaption>Github Actions, Metaflow and AWS SageMaker</figcaption>
</figure> 


Github Actions is every software developer's favorite CI/CD tool, from the makers of Github. It is used by millions of developers around the globe, and is very popular among the Open Source community and is mostly free.

Metaflow, the Data Science framework developed in Netflix, is a very attractive proposition as it allows one to easily move from prototype stage to production, without the need for a separate specialist team of platform engineers, enabling your data science team to be more productive.

<figure>
	<img src="../images/metaflow-logo.png"><figcaption>Metaflow by Netflix</figcaption>
</figure> 


And lastly, AWS SageMaker has been in the ML game for a while, and AWS is still the leading Cloud provider (for Cloud services and ML workloads) in the world.

## But why use the three together?

It all boils down to the use of Metaflow and its inherent scalability. You can start using Metaflow even when you are still running your experiments on your laptop.

But when you want to move to the cloud, you will need a basic (and free/cheap) scheduler/orchestrator to kick-off your workflows - enter Github Actions. There are some limitations with using Github Actions as your workflow scheduler/orchestrator, but for simple projects, or in the case when you're leaning on SageMaker for your training and deployment workloads, it is more than sufficient.

And as to AWS SageMaker, teams that are already on the AWS ecosystem will appreciate the almost unlimited deployment possibilities in their fingertips. Typically SageMaker workflows are created and controlled through the AWS console, but to enable us to go to Production in this article, we will be using the AWS Python SDK, through Metaflow.


## What does *Going to Production* mean?

A typical Data Science project starts with the Prototyping stage, and the tool which is the perennial favorite among data professionals is **[Jupyter Notebooks](https://jupyter.org/)**. And this is also my personal playground when I start looking at DS and ML problems, and it's awesome for quick iterations.

It allows me to quickly play with the data, create visualizations, transform data, train and deploy them to an extent. It is awesome, and it has become my favorite too. However, when and if the project needs to progress to production, we need a better tool and work practice. Many teams still deploy to production with their laptop and Jupyter Notebook setup, and though you can, you really shouldn't.

> The main characteristic of production workflows is that they should run without a human operator: they should start, execute, and output results automatically. Note that automation doesn’t imply that they work in isolation. They can start as a result of some external event, such as new data becoming available. --Ville Tuulos, [Effective Data Science Infrastructure](https://www.manning.com/books/effective-data-science-infrastructure){:target="_blank"}

Because my background is in Software Engineering, I've been honed to the process of **continuous integration and deployment** for virtually all my software projects. That all projects should have the ability to be built and deployed at a click of a button, or as a result of a schedule or event, even multiple times a day if required.

Everything **automated**, everything typically **stress-free unremarkable events**.

This is exactly what we want to happen when we want to push ML projects to Production. We want it to be automated, and we want it to be a stress-free unremarkable process. 


## The Sample Project

As I'm currently studying towards the AWS ML Specialty certification, I wanted to play a bit more with the built-in algorithms that SageMaker has in its portfolio. One of the first algorithms I checked out was [Linear Learner](https://docs.aws.amazon.com/sagemaker/latest/dg/linear-learner.html). It's a type of supervised learning algorithm for solving classification and regression problems.

I did not create the notebook from scratch by myself, however I based it from the examples in AWS SageMaker - [An Introduction to Linear Learner with MNIST](https://sagemaker-examples.readthedocs.io/en/latest/introduction_to_amazon_algorithms/linear_learner_mnist/linear_learner_mnist.html). 

I basically ported it into Metaflow DAGs as seen in the flow image below:

<figure>
	<a href="../images/sagemaker-series/sagemaker-metaflow-dag.png"><img src="../images/sagemaker-series/sagemaker-metaflow-dag.png"></a><figcaption>SageMaker Linear Learner with Metaflow</figcaption>
</figure> 

I've leaned on Python for all my ML work, and Metaflow is based on Python (you can use R too), and AWS SageMaker has an extensive [SageMaker Python SDK](https://sagemaker.readthedocs.io/en/stable/) at your disposal.

Looking at the above flow, we are able to do an end to end ML workflow including model training on AWS SageMaker, leveraging on AWS ML instances for ML training workloads, to endpoint creation with your required AWS instance type.

For brevity, I have skipped the part of serving that endpoint to the public, but this can easily be done by serving the endpoint behind an API Gateway and a Lambda. Perhaps we can do this operation in a separate article. Also take note that we have deleted the endpoint, before we end the flow to avoid the dreaded AWS bill specially now as we are just checking out the service.

<script src="https://gist.github.com/jaeyow/aab705a405ebec15bc3de36e385bd822.js"></script>

In this sample project, I have also leveraged on Github Actions as our workflow scheduler/orchestrator, this is really to prove that Github Actions, even in the free tier can really be used in 'production', albeit in a very simple flow.

<figure>
	<a href="../images/sagemaker-series/github-actions-metaflow.png"><img src="../images/sagemaker-series/github-actions-metaflow.png"></a><figcaption>Github Actions, in action with Metaflow</figcaption>
</figure> 

Although it's worth mentioning that [AWS Step Functions](https://aws.amazon.com/step-functions/) is being pushed by Metaflow as the workflow orchestrator of choice if we really want one that that is robust and easy to use. [Metaflow has an official Step Functions integration available](https://docs.metaflow.org/going-to-production-with-metaflow/scheduling-metaflow-flows/scheduling-with-aws-step-functions). Yes this is also a topic that I'd like to cover in a future post. 

Metaflow performs the SageMaker operations - from model training, to model creation, to creating and testing the endpoint, all through the Python SDK, where we really have the power of SageMaker in our fingertips. 

<figure>
	<a href="../images/sagemaker-series/sagemaker-endpoint-inservice.png"><img src="../images/sagemaker-series/sagemaker-endpoint-inservice.png"></a><figcaption>SageMaker Endpoint deployed to production</figcaption>
</figure> 

## Summary

In this article we've ported the Python code from [the MNIST AWS example](https://sagemaker-examples.readthedocs.io/en/latest/introduction_to_amazon_algorithms/linear_learner_mnist/linear_learner_mnist.html), trained our ML model in AWS SageMaker, built, and deployed the model in a SageMaker endpoint in production. This is all automated by Github Actions (in this example the workflow gets triggered by a repository push), and brought all together and made possible by the awesome Metaflow.  

Thanks, I've made the source code freely [available here](https://github.com/jaeyow/sagemaker-linear-learner).

Let me know if you have any concerns, or any questions, or if you want to collaborate!

## Resources
- [Effective Data Science Infrastructure](https://www.manning.com/books/effective-data-science-infrastructure){:target="_blank"}
- [LinearLearner](https://sagemaker.readthedocs.io/en/stable/algorithms/linear_learner.html){:target="_blank"}
- [An Introduction to Linear Learner with MNIST](https://sagemaker-examples.readthedocs.io/en/latest/introduction_to_amazon_algorithms/linear_learner_mnist/linear_learner_mnist.html){:target="_blank"}
- [Deploying A Pre-Trained Sklearn Model on Amazon SageMaker](https://medium.com/towards-data-science/deploying-a-pre-trained-sklearn-model-on-amazon-sagemaker-826a2b5ac0b6){:target="_blank"}
- [Amazon SageMaker Documentation](https://docs.aws.amazon.com/sagemaker/index.html){:target="_blank"}
- [Deploy A Locally Trained ML Model In Cloud Using AWS SageMaker](https://medium.com/geekculture/84af8989d065){:target="_blank"}




