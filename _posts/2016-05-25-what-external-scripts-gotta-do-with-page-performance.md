---
title: What external scripts gotta do with page performance?
author: Anurag Setia
layout: post
tags:
  - external scripts
  - faster websites
  - internet applications
  - page performance
  - web apps
  - web page load
  - web page performance
---
Any modern website or mobile site heavily relies on scripting to make its pages more interactive and neat to provide an overall good user experience. All these scripts are usually included as external scripts in the page. Not only this, 3rd party external scripts are also included for a bunch of purposes including marketing, click tracking, web analytics, social integration and the like. Where these bring considerable value to the table however, the value generated can very well be offset by the drop in traffic or transactions if user experience is damaged by poor page performance. And hence, this post.<!--more-->To begin with, let&#8217;s understand the seven key factors which impact page response time &#8211;

  * How Fast to Receive? – Network Bandwidth
  * What Delay? – Network Latency
  * How Much? – Page Size
  * How Many? – Number of Requests
  * How Many at Once? – Concurrency
  * How Fast to Process? – Server Time
  * How Fast to Display – Browser Render Time

Other factors not included here are connection overhead e.g. SSL, server load, DNS lookup, general network issues, browser cache & client machine performance.

![Page Speed](/resources/page-speed.png)

###### Source: Web Paper “Analyzing Long Distance Web Page Performance”  
Written by Performance Teams, IBM

Now, few of these factors may or may not be controllable for all webpage designers however, you could always have ways to mitigate it. A constraint on Network Bandwidth can always be mitigated by reducing page size, Network Latency with fewer items per page etc. Page size can be optimized by keeping stuff small, compression & caching. Although I get selective about what to compress e.g. if the images are already using a compressed file format like JPEG and further using a web server compression on doesn&#8217;t reduce much, I&#8217;d rather not do it as it would only mean more CPU cycles on the server without achieving much on the page performance front. Number of requests can be reduced by usage of CSS sprites, combining scripts/styles wherever possible and again caching. How fast your server responds is dealing with server-side performance (which is a topic for another time perhaps). About the browser paradigm factors, Browser render time refers to the time taken by rendering engine of the browser to render a page after it has received the necessary resources and Concurrency refers to the # of threads a browser uses concurrently to fetch resources for a page. Usually, there is a per host limit set by browsers during a request which ranges from 2 to a dozen threads in various modern browsers. **External Scripts** play a major role in both these factors as these scripts are blocking in nature and prevent concurrency.

How this really works is that browsers usually load resources in the order of which they are encountered when parsing a page. The page first becomes visible when all the elements till the end of body tag are loaded and the rendering engine has parsed the response and starts to paint it. Every time a script is encountered, a browser willingly stop loading any more resources from the same host until the encountered script is downloaded and interpreted/executed that&#8217;s blocking the rendering initialization of the page. This is pretty much as per a browser&#8217;s contract with a developer since a browser expects that the scripts have been placed in the order of execution expected by the developer and a script could very well be initializing variables used by the following markup or scripts. If, hypothetically, a browser allowed other resources in the following code of the page to be loaded and executed, there would be no guarantee of order of execution for the developer and coding for an internet application could very well have been a nightmare. Hence, if you this behavior as an evil, its a necessary evil (only that it&#8217;s not &#8211; an evil, that is).

What this means is as a web developer, we need to understand this behavior and place our external scripts well in the page and perhaps the best page to place an external script, then, would be at the bottom of the page so that it blocks absolutely nothing. All included external CSS, conversely, should be in the HEAD tag at the top of the page itself. It all sounds simple and dandy except that its not. And that&#8217;s because a lot of times we use scripts to render good UI elements which would not be possible (or as simple) in absence of these scripts. Having the script load after such UI elements are already rendered would mean that they might not look what they are supposed to look like and might even look distorted for a fair amount before things come together which gives another jittery experience to the user. Therefore, an exception to the thumb rule of placing all external scripts on the bottom of the page would be the scripts which are needed to render the page itself. Such scripts should be placed before the element and if needed, in the HEAD tag itself.

I have tried using ASYNC and DEFER attributes of script elements to deal with these issues however, I don&#8217;t see real value in either of these from page load perspective because of two reasons &#8211;

  1. Any script element which is at the bottom of the page isn&#8217;t blocking the page load as it is and downloading later (ASYNC) or interpreting later (DEFER) of a render essential script would defeat the purpose or putting is anywhere else
  2. Both these attributes have buggy implementation on certain popular browsers and certain mobile browsers like Opera Mini do not even support these

Moving external scripts to bottom also can have other undesired effects when it comes to 3rd party marketing and analytics scripts e.g.it could prevent capturing accurate page load time in the web analytics tool however, the trade off is really between having a good page load time and reporting page load time. Apart from this, it would also prevent direct DOM manipulation operations (e.g. document.write, inner HTML etc) to execute successfully which only work till before the DOM Content Loaded event is fired. However, this one has a viable alternative of using standard DOM manipulation operations exposed (e.g. createElement etc).

Lastly, use tools instead of instincts to monitor load order and script profiling. Whether you use Firebug in Firefox of Chrome&#8217;s Developer tools, it doesn&#8217;t matter as long as you monitor carefully the load order and sign off each element which is being loaded before the DOM Content Loaded event is fired.

There are going to be scenarios when this would not be enough and you truly need to load a bunch of external scripts beforehand for the page the function properly and provide an amazing user experience that you do not want to fall short of. In such scenarios, you just have to get innovative and use one of so many design techniques to keep the user engaged or distracted so the user &#8211; either doesn&#8217;t notice the delay or makes peace with it. On demand loading is one such technique which we see frequently on social media platforms. Content below the fold is not loaded unless you scroll down. Similarly, we could keep the scripts and content on stuff below the fold on hold till user actually scrolls down and load the page fragment including the external script dynamically at the event. Another one is Lazy loading which is loading the bare minimal page elements important to the user first and keep enriching the page while user has a chance to interact with it to some extent.

####  Summary

In summary,

  * Move scripts to the bottom
  * Only keep render essential scripts above the body markup
  * Use standard DOM manipulation operations instead of direct ones
  * Trade off load time vs load time reporting
  * Use tools to monitor the DOM content loaded event
  * Use design techniques to work around page load delays

Feedback&#8217;s welcome and I hope this helps some of you.

This <a href="https://youtu.be/a2_6bGNZ7bA" target="_blank" rel="noopener noreferrer">Google Tech Talk </a>talk about the way browsers works (well, one of them) and gives a fairly good idea on things you should do and things you shouldn&#8217;t.