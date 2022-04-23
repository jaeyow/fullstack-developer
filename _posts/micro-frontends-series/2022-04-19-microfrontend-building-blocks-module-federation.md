---
layout: posts
title: "Micro-frontends building blocks: Webpack Module Federation"
excerpt: What is Module Federation and why it's perfect for building your Micro-frontend project
modified: 2022-04-18
date: 2022-04-18
tags: [Micro-frontends building blocks, Webpack Module Federation, software engineering]
header: 
  overlay_image: /images/micro-frontends-series/rsz_teng-yuhong-qmehmiyaxvy-unsplash.jpg
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

### Part of the [Micro-frontends building blocks Series](../tags/#micro-frontends-building-blocks)

## Meet Module Federation
The next micro-frontends building block we will cover is Module Federation.

It was initially created to enable asynchronous loading of Javascript bundles, so one can easily share and consume code in the Javascript ecosystem, ie. any Javascript project, think browser, Node.js or Electron.

Later on, it was extended to support server-side rendering scenarios. Since the method I'm going to explore in building my micro-frontends is client-side composition using React.js, I've identified Module Federation as the perfect technology to use. 

Module Federation was created by Zack Jackson, a Webpack core maintainer himself, and was integrated as a flagship feature of Webpack 5 in [October 2020](https://webpack.js.org/blog/2020-10-10-webpack-5-release/#major-changes-development-support). 

<figure>
	<a href="../images/micro-frontends-series/module-federation-main-image.png"><img src="../images/micro-frontends-series/module-federation-main-image.png"></a><figcaption>Webpack Module Federation</figcaption>
</figure> 

## But, what seems to be the problem?
**Scalability** - its the problem that Module Federation tries to solve.

So that **large applications** can be split easily where each part can then be shared among other parts and may be developed by **separate teams**.

Module Federation is a game-changer in Javascript Architecture because before this, sharing code was clunky and just didn't feel smooth enough. The usual module sharing method that we have been using for years is using NPM packages, enabling developers to create build-time dependencies. Although NPM works, it cannot help us when we need to load dependencies at run-time.

As micro-frontends evolved, we now have a need to resolve Javascript modules at run-time. This is where Module Federation shines.

## Module Federation super powers

### Good build performance

Because Module Federation encourages you to arrange your application into separate projects so that you can build and deploy them independently (therefore in parallel), each project can be built and deployed in isolation and may be done by different teams.

### Good web performance

The problem with the usual NPM module composition is that it typically increases the application size as the number of dependencies increase. Module Federation provides you an option to lazy load bundles, to avoid loading them when your application loads, but only loading them on demand. This results in a better web performance as it avoids having to download modules before they are actually needed. 

### Good management for shared dependencies

And because Module Federation provides excellent dependency management, it efficiently resolves vendor and third-party dependencies so that only one version of a library is ever loaded by your application. How good is that?

### Import code from other builds, at runtime

Instead of sharing code and thinking of "libraries" when using NPM package approach, we can think of applications that use Module Federation not dissimilar to APIs. Now web applications can expose functionality to other applications, the same way that it can also consume from other applications.

### Deploy independent code, without needing to re-deploy consumers

The ability to have evergreen functionality is very appealing to the developer. There will be no need to redeploy the consumers anymore when exposed dependent functionality will have changed. I have to say that this in itself is a very powerful feature, which will need very careful consideration to avoid unintended results.

### Redundancy and self-healing capabilities

With shared dependencies, Module Federation maintains a dependency graph for your whole application, so that even though applications fail to declare a dependency or when there are network issues, it knows the needed dependencies so that it takes care of downloading it as required.

### Micro-frontends will work like a monolith

Bringing in shared functionality to your application is quite simple - either synchronous loading by importing the bundle as usual. Or asynchronous loading by using lazy loading, to only load the dependencies when required.

### Developer experience improved, maintaining customer experience

Using Module Federation will feel very familiar to any Javascript developer, since it is available as a Webpack plugin starting with Webpack 5. If we think about that for a bit, this is actually quite powerful and exciting.

Think about all the things that Webpack can bundle - scripts, assets, styles, images, markdowns, and more by using third party Webpack loaders. All these can be federated and shared though Module Federation, great, right?

## Caveat

However, as great as Module Federation is, it is important to remember that it is not a framework, and as such it does not handle any of the implementation details for you. For example, you could use awesome client-side composition libraries such as Single SPA, or Next.js and just leverage Module Federation to do the module loading over the wire for you.

## Conclusion

In this article we have introduced Module Federation as an excellent option for building your micro-frontend application. 

- It enables multiple teams to work on a single application by allowing applications to share and consume functionality at runtime. 

- It makes your applications more compact through the use of shareable dependencies.

- It enables evergreen functionality so that you won't need to build and deploy your consumers.

- Developer experience is great since many developers are familiar with the Webpack ecosystem

- Once configured, your application will work like a monolith which is awesome.

## Resources
- [Webpack 5: Module Federation](https://webpack.js.org/concepts/module-federation/){:target="_blank"}
- [Webpack 5 Module Federation: A game-changer in JavaScript architecture](https://medium.com/swlh/webpack-5-module-federation-a-game-changer-to-javascript-architecture-bcdd30e02669){:target="_blank"}
- [Module Federation Examples](https://github.com/module-federation/module-federation-examples){:target="_blank"}
- [Webpack 5 Module Federation - Zack Jackson - CityJS Conf 2020](https://www.youtube.com/watch?v=-ei6RqZilYI){:target="_blank"}
- [Microfrontends with Module Federation: What, Why, and How](https://levelup.gitconnected.com/microfrontends-with-module-federation-what-why-and-how-845f06020ee1){:target="_blank"}
