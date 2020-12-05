---
title: Jersey on WebSphere issue
author: Anurag Setia
layout: post
tags:
  - jersey
  - REST
  - websphere
---
I was just starting creating Jersey RESTful services on WebSphere 8.5 and came across an error.

> [3/31/15 14:27:01:231 IST] 00000065 webapp        E com.ibm.ws.webcontainer.webapp.WebApp logServletError SRVE0293E: [Servlet Error]-[app.FirstRestApplication]: java.lang.NullPointerException  
> at org.apache.wink.common.internal.http.Accept.valueOf(Accept.java:139)  
> at org.apache.wink.server.internal.contexts.HttpHeadersImpl.getAcceptHeader(HttpHeadersImpl.java:151)  
> at org.apache.wink.server.internal.contexts.HttpHeadersImpl.getAcceptableMediaTypes(HttpHeadersImpl.java:105)

The issue arises out of the fact that WebSphere ships with Apache Wink as default implementation of JAX-RS and your application picks up Wink from the class path instead of routing to Jersey causing this unexpected behavior.

**The solution**

Just apply Fix Pack 4 (or 5) and you&#8217;re done which detects the applications shipping with other JAX-RS implementations and allows it. A link to IBM note on this is http://www-01.ibm.com/support/docview.wss?uid=swg1PI27070