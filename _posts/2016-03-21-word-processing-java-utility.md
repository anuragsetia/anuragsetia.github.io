---
title: Word processing Java utility
author: Anurag Setia
layout: post
tags:
  - document conversion
  - java
  - text extraction
---
A while ago, I ran into a word processing requirement of converting documents to web pages and processing the document text to extract information. While working on this, I ended up wrapped a few APIs e.g. <span class="pl-smi">JODConverter into a small set of utility classes. I am not sure of the value of to a developer however, documenting this might just help someone reach the open source APIs I used and use this as sample code. So, here I go with some of the use cases &#8211;<br /> </span>

I was looking for a way to convert MS Word documents to HTML web pages and Rich Text Format documents and used <a href="https://github.com/mirkonasato/jodconverter" target="_blank" rel="noopener noreferrer">JODConverter </a>to accomplish this task. It utilizes an Open Office headless service to carry out the task. <a href="https://github.com/anuragsetia/document-processor/blob/master/src/main/java/in/setia/document/process/TextExtractor.java" target="_blank" rel="noopener noreferrer">TextExtractor</a> exposes two methods in this regards &#8211; one each to extract text and html markup from documents.

> public String extractTextFromFile(String inputfile);
> 
> public String <span class="pl-en">extractHtmlTextFromFile</span>(String inputfile);

The extraction process relies on document conversion operation provided by <a href="https://github.com/mirkonasato/jodconverter" target="_blank" rel="noopener noreferrer">JODConverter .</a> It requires a locally running Open Office process which can be run headless and the configuration of such process can be provided in config.properties in the classpath.

Another use case I ran into required me to persist an email body (html content) while processing incoming emails and <a href="https://github.com/mirkonasato/jodconverter" target="_blank" rel="noopener noreferrer">JODConverter </a>came to rescue again with its simple document conversion operation which is wrapped in another <a href="https://github.com/anuragsetia/document-processor/blob/master/src/main/java/in/setia/document/process/TextExtractor.java" target="_blank" rel="noopener noreferrer">TextExtractor</a> method.

At the time of writing this post, the code available at [Github repository](https://github.com/anuragsetia/document-processor) is being finished off.