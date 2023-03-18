---
layout: posts
title: Website Performance Series - Part 5
excerpt: "Running Lighthouse on this blog to identify opportunities for improvement"
modified: 2019-11-23
date: 2019-11-23
tags: [web performance, lighthouse]
header: 
  overlay_image: /images/website-performance-series/marc-olivier-jodoin-nqoinj-ttqm-unsplash.jpg
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

## Part of the [Website Performance Series](../tags/#web-performance)

## Running Lighthouse against this blog 
We're back to continue the [Website Performance Series](../tags/#web-performance), after discussing a [leadership topic](../website-performance-series-part-4/) in the last update. I received good feedback from that, getting some readership from people who normally would not spend time in a technical blog like this.

In this installment, we will be running Lighthouse against this blog, and see if we can implement some improvements identified by the tool. I know that this is a pretty tiny website, however the principles will remain the same. It is good that I can demonstrate this in a much smaller scale, small baby steps that will increase our familiarity with the tool, and of course our confidence as we apply these learnings in our own projects. 
<figure>
	<a href="../../images/website-performance-series/lighthouse-fullstack-developer-tips.png"><img src="../../images/website-performance-series/lighthouse-fullstack-developer-tips.png"></a><figcaption>Figure: Fullstack Developer Tips Lighthouse results</figcaption>
</figure>

We didn't really do too bad, with a Performance score of 77, which positions us in the orange rating, however green is better, right?. Also we have scored favorably with the other categories - Accessibility, Best Practices and SEO. If you recall the [Lighthouse metric weights](../website-performance-series-part-3/) that we covered in Part 3, the highest weight at 5x is Time to Interactive (TTI). It is not immediately obvious what exactly is required to better our TTI results, however, Lighthouse has given us some tips in the next section of the report.

## Opportunities for improvement according to Lighthouse
For this simple site, there is just one major issue category really. All the opportunities for improvement is related to the site images. Obviously our use the [Minimal Mistakes Jekyll](https://mmistakes.github.io/minimal-mistakes/) theme helped a lot in us scoring highly in the other categories. These minor image issues are caused by no other than yours truly, but they were quite easy to rectify<sup>*</sup>.

<figure>
	<a href="../../images/website-performance-series/lighthouse-results-opportunities.png"><img src="../../images/website-performance-series/lighthouse-results-opportunities.png"></a><figcaption>Figure: Lighthouse opportunities for improvement</figcaption>
</figure>

There is a long list of improvement suggestions from Lighthouse, but the following are noteworthy:

### Serve images in next-gen formats
In our case I have chosen to use [Google's WebP format](https://developers.google.com/speed/webp) instead of the usual PNG and JPG formats. For the same quality, WebP typically achieves about 25% to 35% smaller files than PNG and JPG for the same visible image quality. However the only problem against this clearly more superior data format is that [not all browsers support it](https://caniuse.com/#search=webp), even though WebP has been around since 2010.

<figure>
	<a href="../../images/website-performance-series/use-google-webp.png"><img src="../../images/website-performance-series/use-google-webp.png"></a><figcaption>For Html, use the picture tag but take care to still use jpg as a fallback for browsers that do not support it</figcaption>
</figure>

Using WebP is straightforward when using the Html `picture` tag. It is not that obvious when you need to support WebP in CSS, such as when you need to set the background of an html element. Unfortunately, this website uses Jekyll and that generates a static site at build time, we could not do it in CSS, because we need to check WebP support of the browser at runtime, and that just would not work here. [Here is a guide on how you can achieve support for WebP for both Html and CSS](https://css-tricks.com/using-webp-images/).

<figure>
	<a href="../../images/serverless-image-handler-architecture.png"><img src="../../images/serverless-image-handler-architecture.png"></a><figcaption>AWS Serverless Image handler has support for runtime generation of WebP images</figcaption>
</figure>

If you have thousands of images, and if you did not want the overhead of running a script at build time to generate WebP versions of your images (you would still need the jpg versions created for fallback), you can use an image handler that supports runtime conversion to WebP format. [In a previous post](/serverless-image-handler/), I discussed how to create an AWS image handler quite easily. We can use AWS Serverless Image Handler - either v3 or v4 has support for runtime WebP format generation. It even has CloudFront in front of it to provide cached access to the API. 

### Properly size and encode images
The images that you host on your website should be the optimal quality for the page it is in. Ideally you should not serve images that are larger than required for the user's screen. This means that using a single image to serve your multiple page breakpoints to support responsiveness is probably not the best way to do it. You can have as many versions of the image as you have breakpoints, I know this is more work however, there are tools that can assist in automating the generation of these multiple formats. More detailed suggestions can be found [direct from the source](https://developers.google.com/web/tools/lighthouse/audits/oversized-images?utm_source=lighthouse&utm_medium=devtools).

### Consider using gzip compression
Ask for gzip compression from your server. And if your server supports it, it will respond with compressed payload. Of course because Github pages used [Nginx](https://www.nginx.com/) under the covers, it supports gzip compression and we get that by default.  

### Serve static assets with an efficient cache policy
To instruct the browser to cache your static pages, you can change the [Cache-Control header](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#defining-optimal-cache-control-policy) to have a longer time. For this site, Github Pages fixed the `max-age` to 600 seconds or 10 minutes, after which it will need to fetch from the server again. Lighthouse complains that 600 seconds is not enough, so you could try 86400 seconds which I know it is fine with. 

<figure>
	<a href="../../images/website-performance-series/use-efficient-cache-policy.png"><img src="../../images/website-performance-series/use-efficient-cache-policy.png"></a><figcaption>Figure: Static assets that Lighthouse is complaining about</figcaption>
</figure>

A big gotcha here is that you cannot change your response headers in Github pages so you will be stuck with 10 minutes, which will not make Lighthouse happy. However, check out the use of [this method](https://www.rzegocki.pl/blog/custom-http-headers-with-github-pages/), or use [Netlify](https://www.netlify.com/) to enable you to change headers and more.

Another option is to use resources in CDN. For example for the FontAwesome file `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.7.1/js/all.min.js`, instead of hosting it myself, and be limited by the max-age of 600 seconds imposed by Github pages, I decided to use FontAwesome CDNs which have a max-age of 86400 seconds. Plus you get the advantage of the multiple edge locations that the CNDs can give you. 

Finally we have achieved all green! If this was an important page to you, then this is the perfect time to run your experiments with the many packages like [Optimizely](https://www.optimizely.com/anz/), or [Freshmarketer](https://www.freshworks.com/marketing-automation/).

**It is counterproductive to start split testing activities until you have high scores in Lighthouse.** 

<figure>
	<a href="../../images/website-performance-series/lighthouse-improvement.png"><img src="../../images/website-performance-series//lighthouse-improvement.png"></a><figcaption>Figure: Lighthouse improvements</figcaption>
</figure>
  
## My Picks
From this post onwards, I plan list down a couple of my choice picks, which doesn't have to be software related, it just needs to have had an impact to me in the past couple of weeks:

- [Bullet Journal](https://bulletjournal.com/) - The Analog Method for the Digital Age 
- [Kayaking in Sydney](https://www.sydney.com/things-to-do/beach-lifestyle/kayaking?gclid=CjwKCAiA_f3uBRAmEiwAzPuaMzkxjf1dVBST0GdKyaM_bOHCfNGYuFZkadCgBNv7WMCLLsYgntba2BoC0QYQAvD_BwE&gclsrc=aw.ds) - Experience the best of Sydney's waterways
- [Dance Monkey](https://www.youtube.com/watch?v=q0hyYWKXF0Q) by Tones and I

## Resources
- [Let's build the future of the web](https://web.dev/)
- [Javascript Performance Optimizations](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization/)
- [HTTP Caching](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching#defining-optimal-cache-control-policy)
- [Loading 3rd Party Javascript](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript)

  
