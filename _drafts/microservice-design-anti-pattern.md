---
title: Microservices Design Anti-pattern
author: Anurag
layout: post
---
With the emergance of cloud and cloud-native technologies, Microservices Architecture has surfaced as the default architecture for custom applications including enterprise as well as web applications. One of the keys to realizing microservices architecture is Domain Driven Design to identify microservices for your application domain. While there are plenty of content out there providing guidance as to how to break down your domain into sub-domains and identify your microservices, I try to touch upon a couple of anti-patterns often observed during domain driven design.

## Layering microservices

The idea of microservices was to move away from layered architecture to a mesh where the logical component structures have evolved to accomodate fluidity and flexibility. However, I have still observed quite a few teams adapting microservices trying to find microservices for each layer. This stems from the old habits of separating concerns - especially the responsibility of presentation, business logic and entity model.

![Microservices Layers](/resources/blog-microservices.png)

This introduces unnecessary network communication between the microservices therefore impacting performance and resilience of the features.

## Business Entity driven microservices
In domain-driven design approach, though its recommended to identify and use domain entities to identify microservices in a sub domain however, attempting to build a “single enterprise-wide entity model” and using that to drive microservices identification is an anti-pattern. Its called Anemic Domain Model.

Its advised to instead pursue a bounded context based design approach to identify and build microservices and data model respectively which allows you to minimize the impact of a change – in terms of number of microservices requiring a change for a new feature etc.

Its advised to instead identify sub-domains and pursue a bounded context based design approach for each sub-domain to identify and build microservices and data model respectively which allows you to minimize the impact of a change – in terms of number of microservices requiring a change for a new feature etc.

## Deployment model
Deploy each microservice as individual application in the container platform to allow independent scaling and operation of the service as well as isolation of faults. One microservice per process; one process per container (or VM)
