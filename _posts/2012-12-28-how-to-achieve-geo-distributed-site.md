---
title: How to achieve geo-distributed site
author: Anurag Setia
layout: post
tags:
  - internet applications
  - web apps
---
<span style="font-family: Trebuchet MS, sans-serif;"><b>Why do I need a Geo-distributed site?</b></span>  
<span style="font-family: Trebuchet MS, sans-serif;">If you are serving to a global audience (or even an audience across geographies), it is very desirable to have your site geo-distributed to enable you to serve your site to users from closer to their location. So, instead of a site being hosted in a set of servers in one location, you host a set of servers in a set of locations which are geographically distant and strategically chosen to be closer to the biggest user clusters&#8217; locations. </span>  
<span style="font-family: Trebuchet MS, sans-serif;"><br /> </span><span style="font-family: Trebuchet MS, sans-serif;">Typically, these are known as mirrors. </span><span style="font-family: 'Trebuchet MS', sans-serif;">Mirrors are used by all global sites, especially all sites enabling file transfers/downloads. In fact, these sites let you choose your mirror for download to rule out any error while automatically selecting a mirror for you when you first visit.</span><!--more-->

<span style="font-family: 'Trebuchet MS', sans-serif;"><b>What does it mean for my user?</b></span>  
<span style="font-family: 'Trebuchet MS', sans-serif;">It is entirely invisible to a normal user and he doesn&#8217;t normally figures out which mirror is he/she being served the site from. He/she still gets pages served on the same domain name and the same URL&#8217;s. Technically, someone would basic computer science and networking know-how would know or be in a position to find out the difference in mirrors.</span>

<span style="font-family: 'Trebuchet MS', sans-serif;"><b>How would this work?</b></span>  
<span style="font-family: Trebuchet MS, sans-serif;">A typical process of first-time requesting a page from a website includes the following steps &#8211;</span>

  1. <span style="font-family: Trebuchet MS, sans-serif;">User&#8217;s machine requests its ISP&#8217;s DNS servers for the location of the site</span>
  2. <span style="font-family: Trebuchet MS, sans-serif;">User&#8217;s ISP&#8217;s DNS server sends out a request to site&#8217;s DNS server for the location of the site</span>
  3. <span style="font-family: Trebuchet MS, sans-serif;">Site&#8217;s DNS server provides to the location of the site (in form of an IP Address)</span>
  4. <span style="font-family: Trebuchet MS, sans-serif;">User&#8217;s machine requests the site location for the page</span>

<span style="font-family: Trebuchet MS, sans-serif;">The trick here, in geo-distributing this site, lies in 2nd step. This is enabled by a </span><a style="font-family: 'Trebuchet MS', sans-serif;" href="http://en.wikipedia.org/wiki/Anycast" target="_blank" rel="nofollow noopener noreferrer">Anycast</a> <span style="font-family: Trebuchet MS, sans-serif;">DNS service. What that means is &#8211;  a set of identical DNS servers therefore, when a nslookup (the basic networking request to resolve a domain name) is done on a domain name, the user&#8217;s </span><span style="font-family: 'Trebuchet MS', sans-serif;">ISP&#8217;s DNS server would send back the location it receives from the site&#8217;s DNS server which responds before the others &#8211; typically the closest DNS server. </span>

![DNS](/resources/dns-resolution-gslb.gif)

<span style="font-family: 'Trebuchet MS', sans-serif;">All the site&#8217;s DNS servers carry different locations of the site hence, based on which DNS server does a user get the domain name resolved from, the mirror he/she would end up being served from would vary. These DNS servers also cache this information with themselves for other users in their networks who might request for the same domain name some time later.</span>  
<span style="font-family: 'Trebuchet MS', sans-serif;"><br /> </span><span style="font-family: 'Trebuchet MS', sans-serif;"><span style="font-size: xx-small;">PS &#8211; I did get lose in how I was writing this post many a times therefore, if you find any flaws in the post, do post a comment and I would edit it accordingly.</span></span>