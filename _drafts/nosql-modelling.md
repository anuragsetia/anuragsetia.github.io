---
title: Going NoSQL
author: Anurag Setia
layout: post
---
NoSQL database offer great power to developers and organizations in form of fluidity of data definition and data structure. However like any other transition, moving from relational databases to NoSQL also requires a mindset shift and if you do not stop thinking relational, you may land in more problems than the one you are trying to solve by using NoSQL. This post tries to provide some pointers to catalyze such transition.

## What's different?

### No more Design-before-use
The default way of designing data models in relational world is by thinking about how you will store all of your application entities. This involves identifying all of its attributes with a full definition of the type & size, their relationships to other entities and some more. Once designed, it does not change often - almost never on the fly. In the NoSQL world, this constraint is lifted. Absolutely nothing needs to be defined ahead of time and you can add a new field for a data entity on-the-fly or store multiple type of data into the same field like its nobody's business or an entirely new entity altogether.

### Support for complex data types
Relational databases only support tabular data however NoSQL has no such limitation and allows you to design or store complex data structures with the same entity. This also includes the ability to store an array within the record. This provides a lot power to design entities and relationship however  you need - both in terms of depth and structure, without spanning it across a number of tables with a bunch of foreign key relationships.

## What does this mean?
This may sound very liberating however, this only takes data structure out of the equation so you can focus only on decisions around consumption i.e. identify your entities in the applications considering how they are accessed. A key aspect of this is to take decisions around Embedding and how relationships are realized.


Embed child entities into parent entities.

with respect to "child" entities e.g. Person and Contact - should these be separate collections or should Contact records be embedded within the Person record. Because NoSQL allows storing arrays of data within a record, any 1-n relationships from relational world is realizable within the same entity in NoSQL world and the decision is purely down to how the data will be consumed.

### Relationships

## De-normalize

## Data integrity / consistency

## Events