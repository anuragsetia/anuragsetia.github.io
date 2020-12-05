---
title: 'Websphere Portal Server &#8211; some hacks'
author: Anurag Setia
layout: post
tags:
  - http server
  - internet applications
  - seo friendly url
  - WCM
  - web apps
  - websphere portal server
---
<span style="font-family:Trebuchet MS, sans-serif;">We recently worked on making URL&#8217;s of a WCM driven site SEO friendly. It has a couple of problems &#8211; the home page URL itself was not just the domain name but also had a trail of wps/wcm/connect/whatnot after it which was common for all the pages of the site as well.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">How we resolved this was using reverse proxy @ the web server to hide the common part of the URL. We subsequently ran into a couple of new issues.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span>**<span style="font-family:Trebuchet MS, sans-serif;">1. Generated links on pages were not relative</span>**  
<span style="font-family:Trebuchet MS, sans-serif;">We had to re-write URL&#8217;s using regular expressions in all the responses. We had created a bunch of proxy context for a lot of our site libraries. We had to handle them all in the re-writing</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span>**<span style="font-family:Trebuchet MS, sans-serif;">2. What to do about already ranked pages with old URL&#8217;s</span>**  
<span style="font-family:Trebuchet MS, sans-serif;">Since, we had used proxy, the old URL&#8217;s still worked. We didn&#8217;t use redirects as we were not sure how that could impact our page ranks. Setting canonical URL&#8217;s to the newer URL&#8217;s did the trick for us. Hence, page was accessible through both the URL&#8217;s for a while however, the search engine URL&#8217;s started reflecting the new URL&#8217;s within days.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">Here is a list of a few reference articles and discussions which we came across and were helpful.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><a href="http://stackoverflow.com/questions/5858563/seo-in-websphere-portal-page-title" rel="nofollow noopener noreferrer" target="_blank"><span style="font-family:Trebuchet MS, sans-serif;">Setting Page specific title</span></a>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;"><a href="http://www.ibm.com/developerworks/forums/thread.jspa?threadID=253212" target="_blank" rel="noopener noreferrer">Clean and SEO friendly URL&#8217;s</a></span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><a href="http://www-10.lotus.com/ldd/portalwiki.nsf/dx/Increasing_the_Search_Engine_Optimization_ranking_for_IBM_Web_Content_Manager_Web_sites" target="_blank" rel="noopener noreferrer"><span style="font-family:Trebuchet MS, sans-serif;">SEO friendly URL &#8211; 2</span></a>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><a href="http://www.symphonious.net/2008/07/08/creating-clean-urls-with-ibm-wcm/" target="_blank" rel="noopener noreferrer"><span style="font-family:Trebuchet MS, sans-serif;">Some more on SEO friendly URL&#8217;s</span></a>