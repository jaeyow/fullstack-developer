---
layout: posts
title: Website Performance Series - Part 2
excerpt: "Identifying performance gaps and formulating your performance budget"
modified: 2019-09-19
date: 2019-09-19
tags: [web performance, conversion rate, page load times, web optimization, SEO, page traffic]
header: 
  overlay_image: /images/website-performance-series/harley-davidson-bwxsi8tcxlk-unsplash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: false
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

## Improve Site Performance
In the previous article, [Website Performance Series - Part 1](https://jaeyow.github.io/fullstack-developer/website-performance-series-part-1/), we've seen how a slow-loading website can have an adverse effect on your page's conversions. This will lead to an increase in your visitor's frustration prompting them to abandon your site for your competitor's.

For the rest of this series, we will be talking about techniques to **improve website performance**, and **NOT** techniques for website optimization (using tools such as [Optimizely](https://www.optimizely.com), [Adobe Target](https://www.adobe.com/au/marketing/target.html) and [Google Optimize](https://optimize.google.com/optimize/home/)). These tools are mainly used by marketing teams for experimentation to increase page and site conversions. Typically, you will only start optimizing your website with these tools once you have maximized your site's loading speed. 

> Although these tools may ultimately improve page conversions, they may have a negative effect and can actually slow down your page to some extent, so it may be a counter-intuitive exercise, and best left to be discussed in more detail perhaps in a future post. 

## Discover your performance gaps
Google has produced several tools to help you discover gaps in your site performance. Because ultimately your site was designed with for an audience, and not just for one person, your site performance may be highly variable due to many factors and multitude of users.

<figure>
	<a href="../images/website-performance-series/tools-for-website-performance.png"><img src="../images/website-performance-series/tools-for-website-performance.png"></a><figcaption>Figure: Tools used for finding gaps in web performance</figcaption>
</figure>

Visitor's devices and network latency can affect your site performance however this might not be always obvious in a lab environment.

Google has tools that can collect both **lab data** for discovering fundamental performance issues and **field data** for identifying real-world performance. Here's a link to the following [Google Speed Tools](https://developers.google.com/web/fundamentals/performance/speed-tools/) which contains a guide on usage. 

Using a combination of these tools like Lighthouse and Test My Site can give you a pretty good idea of your site's performance. Lighthouse results contain important details about your site, and some suggestions on how you can improve.c  

- creating your performance budgets - time based, or size based or both, or easily based on computer metrics, like lighthouse scores, performance budgets make it possible to catch performance issues before shipping code, much like catching application issues with unit and/or integration tests.
- what can we do to optimize and in what order
- when to optimize - talk about more advanced website optimization tricks like A/B testing, personalization testing
- a/b testing tools can adversely affect page loading time
  
## Conclusion
This post is the first of a series discussing the topic of web performance optimization through conversion rate, page traffic, and SEO improvements which are all separate topics in their own rights, however best implemented together like in a symphony to achieve the best outcome. This will be the point of view of a full stack developer. See you later. 

## Resources
- [Website Performance Conversion Rates](https://www.cloudflare.com/learning/performance/more/website-performance-conversion-rates/)
- [Optimizing Web Performance](https://speckyboy.com/optimizing-web-performance/)
- [How speed affects website](https://hostingtribunal.com/blog/how-speed-affects-website/)

  
