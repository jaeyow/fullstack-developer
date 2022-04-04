---
layout: posts
title: "Micro-frontends building blocks: Monorepos"
excerpt: What you always wanted to know about Monorepos but were too afraid to ask
modified: 2022-04-05
date: 2022-04-05
tags: [Micro-frontends building blocks, Monorepo, software engineering]
header: 
  overlay_image: /images/micro-frontends-series/rsz_75_dustin-humes-gwim_hpiswi-unsplash.jpg
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

## A monorepo, what's that?
A while back I was finishing work with an employer and was due to join my new team. I remember feeling excited when I heard that the new project will be using monorepos. I did not have a clue what monorepos were, only I've heard that that's what the big boys were using.

Definitely not mainstream (still not these days) they were supposed to promote better collaboration, and give the teams using it full autonomy and are perfect for when you're anticipating the project to scale. 

>Yeah, OK that sounds good, however, I just didn't understand how just by co-locating all your sub-projects into a single repository will magically give you all the advantages mentioned. 

## Monorepo is code co-location
Yes, Monorepo is code co-location, but there is more to it than that.

Just putting several projects in one repo does not make it a monorepo. In fact, if that's the only thing that we do, we are creating a monolith. A good monorepo enables you to create distinct and separate projects, that have well defined relationships and dependencies.

This is a very common misconception in software engineering, where as far as I can remember, we have been conditioned to put everything in its own repository to encourage team autonomy. But it also promotes isolation that creates silos within the team and that essentially kills collaboration.

## Monorepo promotes dependencies and relationships
Monorepos excel with dependency management now that all the code is co-located in one spot. Because a monorepo can contain many disparate projects that may have deep and non-trivial relationships, monorepo tooling are optimized for build speed.

It can cache previously performed operations, so that running them again will skip the work that has already been done to produce substantial time savings.

The **node_modules** folder needs no introduction, its that deep dark place where all project dependencies end up in. Current monorepo tooling can save a substantial amount of disk space by hoisting common dependencies to the top level, so that all lower level dependencies there instead.

## Monorepo is one version for all
With monorepos, version configuration is simple, there is only one version, and this essentially is a snapshot of the system removing the need to manage the multiple different versions of your application and its dependencies. 

## Monorepo is atomic
Imagine all your system in one repo. Web frontend, IOS and Android mobile app, shared libraries, APIs, Lambdas, IaC, scripts, etc. The ability to be able to work on a task and do everything in the same commit, that is possible with monorepos.

## Monorepo is intelligent tooling
Many of the monorepo benefits are not possible without the advancements in current monorepo tools.

Tools like [Lerna](https://github.com/lerna/lerna){:target="_blank"}, [Bazel](https://github.com/bazelbuild/bazel){:target="_blank"}, [Nx](https://github.com/nrwl/nx){:target="_blank"}, [Rush](https://github.com/microsoft/rushstack){:target="_blank"}, [Turborepo](https://github.com/vercel/turborepo){:target="_blank"}, to name a few. [Lerna](https://github.com/lerna/lerna){:target="_blank"} is probably the grand daddy of all monorepo tools. [CRA](https://github.com/facebook/create-react-app){:target="_blank"}, [Babel](https://github.com/babel/babel){:target="_blank"}, [Jest](https://github.com/facebook/jest){:target="_blank"} are a few projects that use it. [Bazel](https://github.com/bazelbuild/bazel){:target="_blank"} has been refined and tested for years at Google to build heavy-duty, mission-critical infrastructure, services, and applications. [Turborepo](https://github.com/vercel/turborepo){:target="_blank"} is the monorepo for [Vercel](https://vercel.com/){:target="_blank"}, the leading platform for frontend frameworks. These tools can help keep your monorepo workspaces fast, understandable and manageable.

[Monorepo.tools](https://monorepo.tools/) is an excellent resource detailing the many intelligent features of these tools that help manage your monorepo projects.

## Monorepo is collaboration
Because all the team's code (maybe even the whole organization's) in the same repository, monorepos encourage code sharing, transparency and cross team collaboration. This does not come for free, though. There will be more noise, but with good management and the help of efficient tooling, this is all possible.

## Monorepo is people
Software engineering is as much technical as it is people. Yes monorepo is a technical strategy to structure your project and workspace.

However, it is actually much more than that. Because is encourages people to collaborate effectively and work efficiently together, it represents the change that probably many software teams need today.

## Conclusion
Moving to monorepos represents a paradigm shift in software engineering. There are reason's why many organizations have made the shift. There are obviously many gains with using monorepos that made these organizations move. But because it represents a fundamental change and shift in thinking, there are also many detractors.

Because on the surface what may look like a simple change in project and workspace structure, is actually an organizational change, and that can be hard in any industry.

## Resources
- [Building Micro-Frontends by Luca Mezzalira](https://www.oreilly.com/library/view/building-micro-frontends/9781492082989/){:target="_blank"}
- [Monorepo.tools](https://monorepo.tools/){:target="_blank"}
- [Misconceptions about Monorepos: Monorepo != Monolith](https://blog.nrwl.io/misconceptions-about-monorepos-monorepo-monolith-df1250d4b03c){:target="_blank"}
- [Guide to Monorepos for Front-end Code](https://www.toptal.com/front-end/guide-to-monorepos){:target="_blank"}
