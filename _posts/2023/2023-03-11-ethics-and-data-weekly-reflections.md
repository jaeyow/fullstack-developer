---
layout: posts
title: Ethics in Data, Weekly Reflections 
excerpt: Provided in 6 weekly installments, we will cover current and relevant topics relating to ethics in data 
modified: 2023-03-10
date: 2023-03-10
tags: [AI, ML, Data, Ethics, Data Ethics, Fairness]
header: 
  overlay_image: /images/ethics-and-data-weekly-reflections/piret-ilver-98MbUldcDJY-unsplash.jpg
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

## Introduction
In the next 6 weeks, I will be writing about relevant topics pertaining to ethics in data. Being a software developer, AI and ML practitioner, I need to exert more effort to understand the ethical implications of the industry that I belong to and the work that I do.

## Week 1: Code Completion Tooling

In June 2021, [GitHub released Copilot](https://github.com/features/copilot), a code completion tool that uses machine learning to write code for you. Marketed as an **AI Pair Programmer**, it's intended to help developers write code faster. Copilot has been trained on billions of lines of code from various sources, including public Open Source projects in GitHub and other public repositories.

<figure>
	<a href="../images/ethics-and-data-weekly-reflections/blog_image_copilot.png"><img src="../images/ethics-and-data-weekly-reflections/blog_image_copilot.png"></a><figcaption>Amazon CodeWhisperer and Google Copilot</figcaption>
</figure>

Nearly a year to the date, Amazon released a preview of **[Amazon Code Whisperer](https://aws.amazon.com/codewhisperer/)**, a similar tool to Copilot.  

As a software developer, I am excited about the possibilities of these tools. I am always on the lookout for tools that can help me write better code. As awesome as these tools are, I am also concerned about their ethical implications. Being trained on [Open Source code](https://en.wikipedia.org/wiki/Open_source), what will this mean to the source code that it has generated?

From the point of view of [GitHub](https://github.com/) and [Amazon](https://aws.amazon.com/), it makes great business sense, as it uses open source code freely available on the web. It's akin to a Mining company that mines and exploits resources for free, then selling it for a huge profit. 

I am almost certain that the original authors did not intend their code to be used in this manner. There is a [class action](https://githubcopilotlitigation.com/) filed against Copilot on behalf of the millions of GitHub users whose code was used to train the tool. The outcome of this litigation could have significant implications for the these **products**, the millions of **developers** already using them, and the source code **authors** of code used to train these products.

## Week 2: Surveillance technology to spy on workers?

Let's start this second week reflection by [watching this short video](https://www.facebook.com/TheEconomist/videos/1305206572937997/). It's about a company called [Humanyze](https://humanyze.com/), where they use digital badges to track the movements of employees in the workplace. Calling their technology `People Analytics`, they claim that it can help companies improve productivity and employee engagement. The device hears and knows everything you are doing, for every second one spends in the office.

<figure>
	<a href="../images/ethics-and-data-weekly-reflections/ethics-surveillance-workers.png"><img src="../images/ethics-and-data-weekly-reflections/ethics-surveillance-workers.png"></a><figcaption>People Analytics using digital badges</figcaption>
</figure>

It is an older video, however this technology is still being used by thousands of organisations today. It begs the question, is this ethical? There are few ways to dissect this question, but in this instance let's use a simple framework to help us come up with an answer.

The framework to help us answer this ethical dilemma is called [Deontological Framework](https://ethicsunwrapped.utexas.edu/glossary/deontology). It is actually quite straightforward to apply as it only requires people to follow the rules and simply do their duty. With this framework, we don't even have to think about the consequences of our decisions.  

For example, in this scenario, as long as the company can prove that they have consent of the workers using the device, and not against anything illegal, then it is ethical. Humanyze claims that all the data collected are not `listened` for content, but rather only for looking in patterns of interaction, and no identifiable information is collected at all. As to the organisations using these badges in their offices, they come from a good place, of not putting their employees under `surveillance`, but rather helping them enjoy their work more. 

All the data collected is 100% anonymous. It helps identify and diagnose issues in the workplace, those that can affect performance and employee engagement. It can then quantify all the costs, opportunities and risks, so that the company can understand the impact of the changes and their decisions.  

Thousands of organisations have reported significant increases in productivity and employee retention across the board, so they must be doing something right.

What do you think, do you think it is ethical? 

# Week 3: PredPol: predictive analytics to forecast crime

In this third week, we will be looking at AI and ML away from the context of the tech industry. Let's see how AI and ML are being used in the public sector, specifically in the field of policing. In LA, the police department has been using a predictive policing tool called [PredPol](https://www.predpol.com/). The tool uses machine learning to predict where and when crimes are likely to occur. [This video](https://youtu.be/4ycC0DJqrpc?t=783) explains how it works.

<figure>
	<a href="https://youtu.be/4ycC0DJqrpc?t=783"><img src="../images/ethics-and-data-weekly-reflections/predictive_policing.png"></a><figcaption>PredPol: predictive analytics to forecast crime</figcaption>
</figure>

On the surface, it looks like the is a very good practical application of AI and ML. It helps the police department allocate their resources more efficiently, and in turn, help reduce crime. However, the reality is the situation is much more complex that that, as it involves several stakeholders and we need to be mindful of their rights and interests.

The **City of LA** is a vibrant multicultural city, however there is a large population of homeless as well as low-income residents. **LAPD** has been using **PredPol** daily to help them effectively allocate their resources. PredPol has been used to predict the likely location where crimes will occur, and the police department has been using this information to allocate their resources to areas where they are most needed. 

However, a group of **citizen activists** have been protesting against it's use, as they have identified that there is a tendency to misuse this information and target the **low income and homeless**. People like **Anthony, an ex-offender**, is complaining that he is being unfairly targeted by the police. Even though he has done his time, and is now a productive member of the community, the algorithms are still flagging him as a potential criminal and still being added to the crime watch bulletin. However, we also need to remember why this was done in the first place, there are **criminals** all over the city that the police department needs to keep an eye on.

In the context of **Care Ethics**, we need to practice our moral imagination and put ourselves in the shoes of the care givers (**LAPD**, **PredPol**) and the care receivers (**the homeless**, **low income residents**, **Anthony**). The **care givers** I'm sure are coming from a good place of wanting to help the community and make it a safe place for everyone, and the **care receivers** simply want to live a normal life, of course we can't deny that many criminals roam the city and its a balancing act to keep everyone safe. But having said that, there needs to be a way to **police the police**, to ensure that they don't overstep their authority, and this is where the **citizen activists** come in, to ensure that the police are not abusing their power.


# Week 4: Do data practitioners need professional standards?

Being part of the **tech industry**, I have seen the benefits that data can contribute to the advancement of society. I also understand that this industry changes so fast, and that it is difficult to keep up with the latest developments. So I understand the reluctance of many in my industry to have a program for **formal professional registration** like what you see in industries like medicine and engineering.

Having said that, there are standards like **data stewardship and governance**, which are typically vendor agnostic, so they are somewhat insulated from the rapid changes in the tech industry. Having a national program around this capability will ensure that there are standards and the people registered professionally in these programs are up to date with the latest developments and best practices. This also means that they are accountable to the industry and the public, and will be held to a higher standard of **ethics and professionalism**.

<figure>
	<a href="../images/ethics-and-data-weekly-reflections/1thisisengineering-raeng-i8_uhiniu1y-unsplash.jpg"><img src="../images/ethics-and-data-weekly-reflections/1thisisengineering-raeng-i8_uhiniu1y-unsplash.jpg"></a><figcaption>Do data practitioners need professional standards?</figcaption>
</figure>

In a past project we needed to clone data in a production database for testing purposes, there wasn't really a violation of the [Ethics for Data Projects principles](https://siddarth.design/ethics-for-data-projects-5af0af333e71), however, the situation would have benefited from more rigour in the process. After the cloning was done and the test environment was stood up, there were no checks from the customer to ensure that everything was in order.

However reflecting back on **Principle number 4** - "Practice responsible transparency as the default where possible, throughout the entire data life cycle.", we could have been more **transparent** and **socialised the process** and the effort we went through to make sure that the data was **anonymised** and **de-identified**. This would have helped the customer to understand the effort we took to ensure that the **data was safe and secure**. 

# Week 5: Criminalise the re-identification of de-identified data

*Now that this [new law](https://www.kwm.com/au/en/insights/latest-thinking/data-availability-and-transparency-act-passes-parliament.html) to criminalise certain types of re-identification of data has been passed, how will this affect you in your professional or personal context? This is relation to an incident in this [Department of Health case](https://www.itnews.com.au/news/health-pulls-medicare-dataset-after-breach-of-doctor-details-438463) where de-identified Medicare data was relatively easily re-identified.*

Working in software development, I'm used to used to working with application **requirements specifications** as a means to communicate the requirements of a project to the development team. I've had experience on both sides of the fence, as a developer and as a customer working with a sub-contractor to develop a software solution.

As a software developer, I will have to get used to seeing these requirements relating to this bill, and will need to take into account the extra effort that will be required to ensure that if we have de-identified data, we will need to ensure that it cannot re-identified. And my clients will rest assured that it will now be a **criminal offence** for a third party to re-identify and transmit this data. Because this is now criminalised, then malicious actors will be discouraged to re-identify data or risk hefty fines or even jail time.

# Week 6: What three (3) changes can you make in your own data or analytics practice to become an agent of positive change?

There are several things that I can do to become an **agent of positive change**, even if I am not in a leadership position. People in a similar position as myself often underestimate our influential power. In these instances, you don’t really need to be a manager or in a leadership position to affect positive change into your team or even the company you are part of. 

I can start with ethical awareness activities such as when building case studies or proof of concepts as is common in my consulting practice, I could make ethical and regulatory data concepts **more prominent**. I did several of such activities in the past, without any regard to these topics. I have the power to shape the environment I live in and the world around me. 

Continuing with the educational endeavour, and working with clients and building the projects for them, I have noticed that my clients may need some hand holding and guidance on the way forward. **Ethical intelligence** is not often a strong characteristic for companies and they will need someone to help them understand their responsibility for building a better world, together with their aspirations of increasing profits. 

Lastly, if I want to impart more positive impact to my company and to the world around me, I may need to push myself and go for a higher level position than where I am right now, one that will have more leadership opportunities. Becoming a great and **ethically-aware leader** will undoubtedly help others rise and the company and the community around me will positively benefit from it. 

