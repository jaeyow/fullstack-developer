---
layout: posts
title: Remember the last time you created an Entity Relationship diagram? I can't. 
excerpt: (Re)Learning how to create conceptual models when building software
modified: 2023-01-14
date: 2023-01-14
tags: [SQL, Entity Relationship Diagram, DB Modelling, Master of Data Science]
header: 
  overlay_image: /images/master-of-data-science/jan-antonin-kolar-lrox0shwjuq-unsplash.jpg
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

## Database Systems
I started my [Master of Data Science coursework this month](../master-of-data-science-coursework/) and the first course in the program is all about **Database Systems**. Having been developing software as a full stack developer for many years now, there have been many instances where a feature I'm working on required a database to be designed and setup.

## Conceptual Design with ER Diagrams

The very first topic we covered is the use of **Entity Relationship Diagram (ER Diagram)** as part of the process of building the application after the requirements have been gathered.

Wait, when was the last time I had to make an ER diagram? I honestly cannot remember, maybe in my undergraduate course, but possibly not in my professional career? I discuss with my team in a meeting or a chat session, draw into a scrap piece of paper or exercise book, scan that and send through in an email. I'll have to admit that my development style have been light on documentation, and prefer my code and some comments to convey my intentions, as I go. 

## Am I alone with this thinking?
This exercise made me question if I'm a real developer at all? However, I know that I am not alone in this. Many, if not all of the developers I've worked with over the years would have the same experience as I have. 

## Why we are not using ER Diagram anymore

So what may be the reasons why we are not using ER diagrams to develop SQL databases as much as they used to? Here are my thoughts:

### Agile development methodologies

With the rise of agile development methodologies and the wane of the waterfall model, there has been a push to prioritize rapid development and iteration over detailed planning and design, where code is more important than documentation. 

### ORM frameworks

Object-relational mapping (ORM) frameworks have become more popular in recent years. These frameworks automatically map object-oriented code to relational databases (as in the code first approach), so we don't have to design the database schema manually.

### NoSQL databases

NoSQL databases have become increasingly popular and in some cases, they offer more scalability and flexibility than traditional relational databases. ER diagrams are primarily used for relational databases, and may not be as useful when working with NoSQL databases.

### Up to date documentation

ER Diagrams being a conceptual model of a database, it is the shared vision of you system made available to all stakeholders, regardless of technical ability. However, as the project matures, more and more changes will need to be implemented, which means that the ER Documentation will need to be maintained with these new changes. This definitely is a candidate for more documentation that will most likely will not get updated. 

## Designing Data Warehouses
With the advent of Data Warehouses where an increasingly complex web of data sources need to be intertwined together and the increase in the use of data for the creation of analytical reports, there has been a recent push to bring back data modelling, not just to help convey the shared data vision, but of equal importance for more practical and financial reasons.

### Good data modelling benefits
Having a good and correct data model means end users will have accurate data, the same data put in front of the decision makers. Correct data means correct and better decisions.

Good data models help in creating pipelines that use simpler queries, simpler queries that translate to cheaper compute. Good data models that avoid having to create duplicate pipelines that return the same data, and these will most definitely translate to savings in cloud compute costs.  

## Summary
As I review and re-learn the use of Entity Relationship diagrams in not only building databases, but also larger systems in Data Warehouses and Data Lakes, I have to remind myself that we do these not *just* for documentation:

- initially used for documentation and a vessel to disseminate the shared vision
- can be used to define the data architecture for an organization
- can aid in building systems that can use simpler and cheaper queries
- can avoid the creation of pipelines that will return duplicate data, translating to savings in compute costs

## Resources
- [Data modeling is back — at scale](https://medium.com/the-future-of-data/data-modeling-is-back-at-scale-3b574e974654){:target="_blank"}
- [The Future of Data Modeling](https://www.linkedin.com/video/event/urn:li:ugcPost:6986056970424262656/?isInternal=true){:target="_blank"}
- [Entity–relationship model](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model){:target="_blank"}

