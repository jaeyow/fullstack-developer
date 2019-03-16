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

In the past I've inherited, developed and maintained a microservice-based project and I would like to share some of the things I have learned with you. 

The frontend of this web application used ASP.NET MVC and ReactJS, the backend a mix of .NET Web APIs and Lambda APIs (we used AWS), about a dozen of them. It also used a few other 3rd party downstream services.

This project was developed by a small team, about from 2 to 4 fullstack developers working on it at a time. There were two client apps - a web application, which was actually a couple of web applications brought together by a proxy server front end. And a mobile application for both major platforms.

## Anything but typical
In a typical client application, like in a mobile app or a typical SPA, one directly calls the microservice endpoints. However as the application evolves, more information and functionality gets squeezed into each page, and it is not unusual to have to do multiple calls to different microservies and compose the page from the data from all these.
<figure>
	<a href="/images/direct-client-to-microservice.png"><img src="/images/direct-client-to-microservice.png"></a>
	<figcaption>Figure 1: Direct client to microservices</figcaption>
</figure>

However, in this hybrid ASP.NET MVC/ReactJS app, the pattern used to compose the page is a bit different, so lets examine the situation. 

<figure>
	<a href="/images/hybrid-client-to-microservice.png"><img src="/images/hybrid-client-to-microservice.png"></a>
	<figcaption>Figure 2: Hybrid ASP.NET MVC/React App to microservice</figcaption>
</figure>

In the course of initially loading a page the MVC App creates the Html skeleton including the bootstrap data that the page needs to achieve first paint as soon as possible. It also loads all the javascript, styling and images to make this possible. Now once the page is up in the client's browser, React takes over and takes care its interactivity helped by the presence of a separate Web API in turn talking to all the services. 

At first I was not quite clear why this separate Web API was required. Then after some research, I have stumbled upon the [BFF Pattern](https://samnewman.io/patterns/architectural/bff/) as masterfully explained by Sam Newman in the post. Actually it was [Phil Calcado](http://philcalcado.com/2015/09/18/the_back_end_for_front_end_pattern_bff.html) who was one of the first (if not the first) who came up with this pattern. 

The mobile application also followed a similar architecture - both the iOS and Android apps talked to the downstream services through a dedicated Web API in the middle. 

<figure>
	<a href="/images/mobile-client-to-microservice.png"><img src="/images/mobile-client-to-microservice.png"></a>
	<figcaption>Figure 3: Mobile App to microservice</figcaption>
</figure>

## BFF pattern is also known by many other names

- Single Purpose API Gateway
- Edge Layer
- API Gateway Pattern
- Single-purpose Edge Services
- Proxy Server Gateway API

But they all point to the same BFF Pattern. Without having to repeat the articles in the previous section, let me say that BFF pattern is to simply have a backend API for each client, in which the development is owned by the client development team (shown in the blue shaded box in Figure 3).

<figure>
	<a href="/images/bff-vs-dev-ownership.png"><img src="/images/bff-vs-dev-ownership.png"></a>
	<figcaption>Figure 3: API Gateway/BFF for each client application</figcaption>
</figure>

# Advantages of using the BFF Pattern
Using the BFF Pattern is more than just a data pass-through from data provider to the clients. These are the advantages for using this pattern:
- it can serve as a **gateway routing/proxy server**: where the client talks to one API gateway, which routes the calls to multiple downstream services. This insulates the clients from changes when downstream servces URL changes. 
  
- it can function as a **request aggregator**: reducing the chattiness of the client application. The client can send just one request to the API Gateway, which can send multiple requests to one or more downsteam services. It can also gather all the responses and send them back to the client application. This can lead to performance improvements as running multiple requests from remote browser or mobile apps are more expensive than running them from each API Gateway. 

- it can contain code that handles **cross-cutting concerns**: such as authentication and authorization, logging, caching, retry policies, load balancing, etc. This can help in making the downstream services' code much more simpler by not having to handle these concerns there.

- it can promote **consistent error handling**: many service providers return errors a bit differently, so we can handle and translate error fault codes from different downstream services in a consistent manner so that the client application can be simpler. 
  
- enebles development team's **autonomy and agility**: BFFs enables and empowers development teams to be more in control of their projects. Instead of waiting for the "backend" team to deliver the updated API, and be at the mercy of their delay, control goes back to the client application team to be more on top of their delivery schedule.  

# Disadvantages of using the BFF Pattern

# When to use it

# Alternatives to the BFF Pattern

# Summary
- service reuse, should we reuse the BFF for other similar features or products? NO, we don't want to ever support other products, cos that will mean we will have to support these use cases in the future
- Buffer aganst change - when both the clients and the BFF work with the agreed response format, then the clients can continue working and will be insulated from all the provider changes
- this will also ensure that the client development will move more faster because cliinet deveelopers can continue working with dumm data
- and then one day the real data will flow from the data proviers and things will just work
- the client devs know what they need, so huge upside when client devs make the BFF

## Resources

- [Backends for Frontends Pattern by Sam Newman](https://samnewman.io/patterns/architectural/bff/)
- [BFF at SoundCloud by Lukasz Plotnicki](https://www.thoughtworks.com/insights/blog/bff-soundcloud)
- [The Backend for Frontends Pattern by Phil Calcado](http://philcalcado.com/2015/09/18/the_back_end_for_front_end_pattern_bff.html)
- [The API gateway pattern versus the Direct client-to-microservice communication by .NET Guide](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/architect-microservice-container-applications/direct-client-to-microservice-communication-versus-the-api-gateway-pattern)
