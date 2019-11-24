---
layout: posts
title: Website Performance Series - Part 4
excerpt: "Real world case studies on effects of improving website performance"
modified: 2019-11-02
date: 2019-11-02
tags: [case studies, real world, web performance, conversion rate, page load times]
header: 
  overlay_image: /images/website-performance-series/spacex-uj3hvdfquji-unsplash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: true
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
  <div id="drawer" markdown="1">
  *  Auto generated table of contents
  {:toc}
  </div>
</section>

## Part of the [Website Performance Series](../tags/#web-performance)

## Real-world case studies
In [Part 3](../website-performance-series-part-3/), we have looked into the metrics that make up Lighthouse, now we have a more complete idea of what they mean. Now let us step back from all those technical details, and visit case studies, and see for ourselves how an improvement in website and webpage performance affects the business.

There are a lot from [where these came from](https://wpostats.com/), however I have only picked a handful for our examples. 

### Case Study 1: Carousell increased their Performance rating by 64 points, resulting to an increase in Organic traffic by 63%
[Carousell](https://au.carousell.com/), a Singapore-based online selling platform, was widely regarded as a the eBay of Asia a couple of years ago , and when they wanted to spread to other parts of Asia like Indonesia and the Philippines. However the main issue they were having was that at that current state where their website took more than 15s to load, there was no way for them to acquire and retain new users as they plan to spread all throughout Asia. 

<figure>
	<a href="https://au.carousell.com/"><img src="../images/website-performance-series/carousell-performance-lighthouse.png" style="width:600px"/></a>
</figure>

Their team embarked on what the call `performance-first web experience`, because according to them good user experience is fast and delightful user experience. They improved their PWA performance by using a more effective cacheing system, streamlined their service worker usage, a better image compression, and CSS inlining. 

> As a result of all these changes, their page was able to load in 6 seconds, whereas before the changes, [it was more than 16 seconds](https://blog.searchmetrics.com/us/google-lighthouse-success-stories/), and increased their organic traffic by 63%!

### Case Study 2: When YouTube introduced a version of their pages that was 90% lighter, they saw a large increase in traffic.
This was an [older post](https://blog.chriszacharias.com/page-weight-matters), however the principles remain the same. Many years ago when YouTube was still not as pervasive as it is today, one of the engineers was complaining why the main view page has ballooned to 1.2MB and dozens of requests. And around that time someone was able to create a Quake clone in under 100KB, so there was no reason why it couldn't be done. So Youtube created that prototype and tested it with a percentage of their users. 

<figure>
	<a href="https://www.youtube.com/"><img src="../images/website-performance-series/youtube-logo.png" style="width:400px"/></a>
</figure>

At first the results were baffling, their loading time actually slowed down. But after more analysis, they found out that their results were skewed because now they had data from places around the world that had never been able to load Youtube before, places with poor mobile connectivity like Southeast Asia, South America, Africa and Siberia. 

> This goes to show that `page weight matters` and it is inversely proportional to the speed of page load. 

### Case Study 3: Radins.com improves Speed Index and reduces bounce rate by 25% and increases conversion rate by 12%
This next case study did not use my recommended tool of choice [Lighthouse](https://developers.google.com/web/tools/lighthouse), but a competitor product [Dareboost](https://www.dareboost.com/en). It doesn't really matter that much whatever tool you end up using, as long as you are consistent so that you can readily compare you past results and track your progress.

<figure>
	<a href="http://www.radins.com"><img src="../images/website-performance-series/radins-com-website.png" style="width:600px"/></a>
</figure>

So yeah, [Radins](https://www.radins.com/) used Dareboost to monitor their website performance progress. In [here,](https://blog.dareboost.com/en/2018/08/continuous-improvement-web-performance-dareboost-m6web/) you can track their progress as they improved their Speed Index reading to below the recommended 1000, which eventually improved their conversion rate up by 12%. And this is not even changing any UX for any of the pages, just basic page speedup activities.

 >Improving conversion rate by simply speeding up the page loading, wow, that seems like a cheap investment that anyone can do! 

## How do you do performance improvements?

### Performance is not just an Engineering Priority
Without achieving organizational alignment and getting the buy-in from the relevant stakeholders it is next to impossible to be able to prioritize performance improvement related projects.

<figure>
	<a href="http://www.1800flowers.com"><img src="../images/website-performance-series/1800flowers-logo.png" style="width:400px"/></a>
</figure>

For some companies, there is full support from the upper management. For online flower site 1800flowers.com, a technical savvy CMO leads a cross functional team made up of product experts, marketing, analytics, design and development, and treat the department as cross between marketing and technical development.

Having clear mandate from the big boss, everyone working in the team are in complete alignment, making their drive to better performance easier than if their organizational structure was different. And because everyone's all-in, the undertaking was not treated as a side project,
but rather resources and time was dedicated to it as the project was highly prioritized. 

<figure>
	<a href="http://www.justfly.com"><img src="../images/website-performance-series/justfly-logo.png" style="width:400px"/></a>
</figure>

For online flight booking provider justfly.com they don't have the luxury of the top-down approach that 1800flowers.com have, instead they took it upon themselves in the engineering team, and even without the mandate from the management, managed to convince them and relevant stakeholder on their side. How did they do that? By taking on bite-sized POCs and experiments, they used the data produced by such activity to enable that organizational alignment required to get the performance ball rolling in their favor. 

### Technical strategies for improvement
Once we have achieved buy-in from the stakeholders, we actually have to build the actual project. This section is not to detail the HOW of doing these performance improvements. Whenever you run tools like [Lighthouse](https://developers.google.com/web/tools/lighthouse) or [Dareboost](https://www.dareboost.com/en), it will present recommendations on the actions to take to fix the all the issues. And the required actions can be varied and depend on the technology being currently used. So we will skip discussing these technical details, as I will be covering some of them in future posts. 

### Measuring performance improvements
For Asian online marketplace Carousell.com, they started with an aggressive performance budget which they have integrated with their CI/CD with complete integration with notification system where the results are shared with everybody. Because it is all integrated and automated, it gives the team immediate feedback on what changes represent progress and what changes represent regressions.

<figure>
	<a href="../images/website-performance-series/carousell-performance-budget.png"><img src="../images/website-performance-series/carousell-performance-budget.png"></a><figcaption>Carousell Performance Budget</figcaption>
</figure>

As a result of this shared goal, automated and measurable process, Carousell were able to improve their website performance considerably.

<figure>
	<a href="../images/website-performance-series/carousell-perf-improvements.png"><img src="../images/website-performance-series/carousell-perf-improvements.png"></a><figcaption>Carousell Performance Improvements</figcaption>
</figure>
What's good about their results is that there is something in it for everyone who were part of the project. The product team cares about the page load time. The marketing team - increase the organic traffic and improved click through rates, and the sales team cared about how many buyers and sellers actually interact with the application. Because it is a shared goal, and there is a sense of ownership of that problem, it follows that everyone concerned will gladly to take part in the formulating the solution.  

## Conclusion
So there you have it, a few case studies that demonstrate the effect of an increased performance can have on your business. The results are undeniable. A fast website will improve user engagement, increase web traffic, and decrease bounce rates.

And as we know all these are a numbers game, if you increase your visitors, you will most definitely increase your conversions, and ultimately, more $$$ for your business.  

## Resources
- [Miscellaneous Tools for Web Performance Improvement (Perf Rocks)](https://perf.rocks/tools/)
- [Web Performance Optimization Stats](https://wpostats.com/)
- [Modern Websites for E-commerce in the Real World](https://www.youtube.com/watch?v=SJiKWwBtQaU)  
