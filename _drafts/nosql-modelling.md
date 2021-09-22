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
This may sound very liberating however, this only takes data structure out of the equation so you can focus only on decisions around consumption i.e. identify your entities in the applications considering how they are accessed. 


### Relationships & embedding
A key aspect of this is to take decisions around how relationships are realized. Because NoSQL databases do not manage relationships between entitities i.e. no foreign keys, no constraints therefore they do not support JOINs.

Because NoSQL allows storing arrays of data within a record, any 1-n relationships from relational world is also realizable within the same entity in NoSQL world i.e. Embedding. However, its not a thumb rule to embed child entities into parent entities and multiple aspects of this de-normalization need to be considered, mostly around consumption -

- 1-1 and 1-n relationships are suitable for embedding but not n-n
- Will the entities be fetched together often? High cohesion means good for embedding
- Will the child entities be changed independant of the parent entity often? You are better of separating them if that is the case
- What is the number of child entities per parent? Embedding is only suitable when this is reasonably low

When not embedding and storing entities in different collections, you can still have attributes that carry reference to the document of another collection however, these are essentially soft links and there is no referential integrity provided by the NoSQL database. 

In case of n-n relationships, you may hold a reference attribute in both entities to allow navigation in both directions or implement an highly de-nomralized approach where data is embedded as well as stored separately. This will be based on the consumption pattern again.

Different entities which are not related directly but are usually required together - may share some of the attributes can also be stored together, without embedding, by introducing an attribute that tells them apart allow them to be fetched separately or together. This is very relevant for entities which are different classes or type of the same entity e.g. a bank can store saving accounts and credit cards in the same customer_accounts collection for an Online Internet Banking portal where some of the attributes can be common and others can be different and a Type attribute can carry the information whether a specific document is a Credit card or a Savings account.

## Data integrity / consistency
NoSQL database do not provide ACID transactions and the focus is on scaleablity more than data integrity. Not that data integrity is altogether ignored, its just that it takes a back seat in form of eventual consistency and priority of the system is to perform and scale and let the distribution engines ensure that EVENTUALLY the data is consistent all across.

Therefore it may not be suitable for all kind of systems and all type of data in a system. Systems which require realtime data integrity e.g. financial transactions should continue to store data in relational database for such data.

## Events