---
layout: posts
title: Website Performance Series - Part 3
excerpt: "Speeding up your site is easy if you know what to focus on. Follow along as I show you how it's done, plus find 3 awesome tips inside!"
modified: 2019-10-08
date: 2019-10-08
tags: [web performance, conversion rate, page load times, web optimization, SEO, page traffic]
header: 
  overlay_image: /images/website-performance-series/everaldo-coelho-kpascpklczw-unsplash.jpg
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

## Part of the Website Performance Series
[Part 1 - Why web performance matters and what that means to your bottom line](https://jaeyow.github.io/fullstack-developer/website-performance-series-part-1/)

[Part 2 - Tools for identifying performance gaps and formulating your performance budget](https://jaeyow.github.io/fullstack-developer/website-performance-series-part-2/)

[Part 3 - Speeding up your site is easy if you know what to focus on](https://jaeyow.github.io/fullstack-developer/website-performance-series-part-2/)

## Lighthouse Metrics (in weighted order of importance)
<figure>
	<a href="../images/website-performance-series/pwa-lighthouse.png"><img src="../images/website-performance-series/pwa-lighthouse.png"></a><figcaption>Tool: Lighthouse by Google</figcaption>
</figure>
To help web developers in their quest for a speedy site, Google brought us Lighthouse. You will at least need Chrome installed in your machine, and is available in a few workflows that suit you best. 

- *In Chrome DevTools.* Easily audit pages that require authentication, and read your reports in a user-friendly format.
- *From the command line.* Automate your Lighthouse runs via shell scripts.
- *As a Node module.* Integrate Lighthouse into your continuous integration systems.
- *From a web UI.* Run Lighthouse and link to reports without installing a thing.

Lighthouse has 5 important metrics that contribute to the final performance score. Each metric has different weights, as a result, those that have a heavier weight contribute more. The following describes each and their corresponding weights:

**Time to Interactive (TTI)** (weight 33.3%)
- Time to interactive is the amount of time it takes for the page to become fully interactive. Interactivity is the point where:
    
    1) the page has started displaying some content,

    2) the visible page elements' event handlers have been registered, and

    3) the page can now respond quickly to user actions. 

- Techniques to improve TTI include [improving your Javascript startup](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization/), [Tree Shaking to eliminate dead code](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/),and [Code Splitting ](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/code-splitting/) to serve the most important chunk first, and lazy load the rest as needed.

**Speed Index** (weight 26.7%)
- Speed Index shows how quickly the contents of a page are visibly populated, for this metric, the lower the number the better. 
- Techniques to improve Speed index are similar to ones for TTI, but a couple of good articles are [Optimizing Content Efficiency](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/) and [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/).

**First Contentful Paint** (weight  20%)
- Blah

**First CPU Idle** (weight 13.3%)
- Blah

**First Meaningful Paint** (weight 6.7%)
- Blah

> **Tip #1 - The secret Lighthouse Calculator** - Well it's not really secret, but not many know about it's existence.
> 
> The [Lighthouse](https://developers.google.com/web/tools/lighthouse) team created a spreadsheet that can guide you in measuring and planning your speed improvements. The [Lighthouse v5 Score Weighting worksheet](https://docs.google.com/spreadsheets/d/1up5rxd4EMCoMaxH8cppcK1x76n6HLx0e7jxb0e0FXvc/edit#gid=283330180) (image below) is a tool that helps one understand the numbers to be aiming for to achieve a particular Lighthouse performance score.
> 
> To achieve a particular performance score, play with the values in the `Potential value` column (in milliseconds), and it will calculate the performance score taking into account the 5 metrics and its corresponding weights.
> 
> This is the same calculation that Lighthouse uses, so yeah it will prove handy in your mission to improve your site, and get the performance score you want, without guesswork. 
> 
> <figure>
> 	<a href="../images/website-performance-series/lighthouse-score-weighting.png"><img src="../images/website-performance-series/lighthouse-score-weighting.png"></a>
> 	<figcaption>Figure: Lighthouse v5 Score Weighting Worksheet</figcaption>
> </figure> 


A webpage (and the website it belongs to) is created to serve a particular purpose for the business.

For example a product page that sells digital cameras has the primary purpose of getting the visitor to click on the **add to cart** button, and eventually buying it.
[Lighthouse Score Weighting](https://docs.google.com/spreadsheets/d/1up5rxd4EMCoMaxH8cppcK1x76n6HLx0e7jxb0e0FXvc/edit#gid=1567011065)
<figure>
	<a href="../images/website-performance-series/screen-amazon-product-listing-900x600.jpg"><img src="../images/website-performance-series/screen-amazon-product-listing-900x600.jpg"></a><figcaption>Figure: Amazon product detail page</figcaption>
</figure>
A contact page is designed to direct the visitor how to get in contact with customer support to solve issues they are facing. 
<figure>
	<a href="../images/website-performance-series/sample-contact-us-page.png"><img src="../images/website-performance-series/sample-contact-us-page.png"></a><figcaption>Figure: HubSpot contact page</figcaption>
</figure>

Slower page response times results in a decrease in conversion rate and increase in page abandonment. The longer it takes for the page to load, the more chance for the visitor to abandon the page and possibly visit the competitor's offering. This means that without changing anything in the site other than improving page response times, we could potentially improve the conversion rate, and thus your bottom line. 

There are many factors affecting page load speed, and we will discuss these in more detail in future posts, however, according to the following infographic here is what a slow loading site might mean to your business.

<figure>
	<a href="../images/website-performance-series/loading-time-sml.jpg"><img src="../images/website-performance-series/loading-time-sml.jpg"></a><figcaption>Figure: How loading time affects your bottom line</figcaption>
</figure>

-  A 1 second delay in page response can result in a 7% reduction in conversions.
-  A 1 second delay decreases customer satisfaction by 16%
-  A 1 second page delay could potentially cost you $2.5 million in lost sales every year for a $100,000 per day site

## Conversion Rate and Page Traffic (and SEO)
**Web page conversion** is when the visitor takes the target action that the developer wanted them to take. It's not really always getting the visitor to buy something as web pages can serve different purposes.

For example, a product detail page from Amazon's definition of a conversion may be a customer purchase. A dentist's book-an-appointment page's conversion is defined as the successful booking on an appointment through the page. Conversion rate is the percentage of successful conversion out of 100 visitors. Say for example out of 100 page visits, if there are 2 clicks to Amazon's buy now button, then the page's conversion rate is 2%.

This is really simple maths, if we increase **page traffic** to 200, then we will have 4 potential buys. The problem is that we cannot infinitely increase the page traffic. It is more realistic to increase the conversion rate and given the same page traffic, have more successful conversions. So in this example, given the same 100 visitors, if we improved the conversion rate to 4%, we will now have 4 successful purchases, an increase compared to when our conversion rate was at 2%.

Now we haven't even mentioned **SEO** yet. To optimize a website for Search engines, you can improve your page traffic as the search engines will want to serve your pages more, thus increasing your bottom line. If you have sound SEO practices, your conversion rates will also increase as these practices tend to improve your site organization making the page simpler and more favorable to navigate. 

## This is interesting stuff
Having been developing software for a while, most of my projects in the past have never been public facing pages with emphasis on optimizing conversion rates (come to think of it, they have not been websites at all).

However, it would be awesome to be in a position to be able to positively influence the business' bottom line through their webpages. Because page metrics are easy to collect and understand, it is not that hard to have a go at conversion improvements, and receive timely feedback from them. It is imperative to setup these metrics before undergoing any attempts at improvement. Otherwise, it will be almost impossible to know if the introduced changes are having any positive effect.
  
## Conclusion
This post is the first of a series discussing the topic of web performance optimization through conversion rate, page traffic, and SEO improvements which are all separate topics in their own rights, however best implemented together like in a symphony to achieve the best outcome. This will be the point of view of a full stack developer. See you later. 

## Resources
- [Website Performance Conversion Rates](https://www.cloudflare.com/learning/performance/more/website-performance-conversion-rates/)
- [Optimizing Web Performance](https://speckyboy.com/optimizing-web-performance/)
- [How speed affects website](https://hostingtribunal.com/blog/how-speed-affects-website/)

  
