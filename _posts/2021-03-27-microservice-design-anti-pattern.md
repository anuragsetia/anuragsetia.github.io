---
title: Microservices Design Anti-pattern
author: Anurag
layout: post
---
With the emergance of cloud and cloud-native technologies, Microservices Architecture has surfaced as the default architecture for custom applications including enterprise as well as web applications. One of the keys to realizing microservices architecture is Domain Driven Design to identify microservices for your application domain. While there are plenty of content out there providing guidance as to how to break down your domain into sub-domains and identify your microservices, I try to touch upon a couple of anti-patterns often observed during domain driven design.

![Microservices](/resources/microservices-logical.png) 
Source - [Microsoft Azure documentation](https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices)

## Layering microservices

The idea of microservices was to move away from layered architecture to a mesh where the logical component structures have evolved to accomodate fluidity and flexibility. However, I have still observed quite a few teams adapting microservices trying to find microservices for each layer. This stems from the old habits of separating concerns - especially the responsibility of presentation, business logic and entity model.

![Microservices Layers](/resources/blog-microservices.png)

The core principle of microservices architecture is to separate concerns by sub-domains and functions instead of whether the piece of code relates to dealing with data or dealing with logic. More often than not, you cannot separate the understanding of the data and the business logic and have different developers code that; microservices scales the application domain down to a level where a developer can and should write both the aspects of the application anyways. You could still choose to separate source files that do data operations and that execute business logic within the microservice code.

The reason this isn't a good idea is because it introduces unnecessary network communication between the microservices therefore impacting performance and resilience of the features. 

## Business Entity driven microservices
In domain-driven design approach, though its recommended to identify and use domain entities to identify microservices in a sub domain however, attempting to build a “single enterprise-wide entity model” and using that to drive microservices identification is an anti-pattern. Its common enough to have a name for itself - Anemic Domain Model. 

It stems from the fact that when translating business processes and business entity model to application architecture, we often overlay the business processes across the business entities i.e. treat business entities as swimlanes in a cross-functional flow diagram format. This automatically leads to entity-bound function mapping. 

![Entity driven model](/resources/blog-process.png)

On the contrary, domain-driven design breaks down domain into sub-domains and attempts to identify and form microservices for the sub-domain with their relevant view of the closely related business entities. This is called bounded context based design approach which creates business function focused boundaries between microservices and also minimize the impact of a change – in terms of number of microservices requiring a change for a new feature etc. Of course, you can still have adapter and BFF microservices where source-specific protocol or data transformation and user journey specific API are needed however, consuming all these as layers should not be the thumb rule but a need based approach only.

## Deployment model
Last of all, the funniest of observation is about how microservices are deployed in various organizations. In spite of decent aware of the "One microservice per process; one process per container (or VM)" thumb rule, I come across instances with multiple processes in a container image far too many times for my liking. This is typically driven by the need to share external infrastructure resources e.g. storage volumes. The trade off is surely the ability to scale and operate the microservices independently as well as the ability to isolate faults.

I welcome comments on these anti-patterns and inputs for any more patterns being observed that I can explore and add to this or a later post.