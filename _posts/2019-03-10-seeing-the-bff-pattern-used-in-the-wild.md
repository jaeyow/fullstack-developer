---
layout: posts
title: Seeing the BFF Pattern used in the wild
excerpt: "What is the BFF pattern and why you need it."
modified: 2018-03-10
published: true
tags: [intro, beginner, jekyll, tutorial]
comments: true
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->

I've recently inherited a microservice-based project and having no commercial experience with microservices myself, I have encountered a few learnings along the way. And I would like to share them here.

For the frontend, the web application uses ASP.NET MVC with some sprinkling of ReactJS (for some server-side goodness), while on the backend are .NET Web APIs, all about a dozen of them. We also call other 3rd party APIs here and there.

And to give you some context, the team has 6 developers, however at most 2 developers work on it at a time. We currently only have 1 client app - this web application. This means we have free reign in changing all the services, as there won't be other client aplications affected by the changes.



## Also known as the following:

- Reverse proxy for Front end
- Edge Layer
- API Gateway Pattern
- Single-purpose Edge Services

# Main takeaways

More than just a data pass-through from data provider to the clients...

## Domain Modeling
- combine data from multiple data providers into one (data aggreggation), some also call this "Hybrid Data Models"
- create a data model that is just right for your application
- create a data model composed of other data models
- 

## Performance
- we can add our caching layer to the BFF layer
- public cache vs private cache through HTTP response cache headers
- thorugh BFF we can reduce the chattiness of our comms
- using the Play Framework to send asynchronous requests to downstream services and allow the framework to stitch them dack together when response is received

## Consistent Error Handling
- the data providers we get data for may have a variety of error responses, the BFF allows us to normaiize them all for consistency


# Lessons learned
- service reuse, should we reuse the BFF for other similar features or products? NO, we don't want to ever support other products, cos that will mean we will have to support these use cases in the future
- Buffer aganst change - when both the clients and the BFF work with the agreed response format, then the clients can continue working and will be insulated from all the provider changes
- this will also ensure that the client development will move more faster because cliinet deveelopers can continue working with dumm data
- and then one day the real data will flow from the data proviers and things will just work
- the client devs know what they need, so huge upside when client devs make the BFF

## Resources

- [Backends for Frontends Pattern by Sam Newman](https://samnewman.io/patterns/architectural/bff/)
- [BFF at SoundCloud by Lukasz Plotnicki](https://www.thoughtworks.com/insights/blog/bff-soundcloud)
