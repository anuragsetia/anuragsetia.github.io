---
title: Effective web performance testing
author: Anurag
layout: post
image: ../resources/2020/05/Untitled.png
tags:
  - internet applications
  - performance engineering
  - performance testing
  - pitfalls
  - tps
  - transactions per second
  - web apps
  - web page load
---
 

<p class="has-drop-cap">
  There are quite a few reasons for teams to entirely circumvent performance test in a web project however, the two biggest reasons for such organization behavior are Lack of skilled performance engineers & performance testers and Lack of robust understanding of performance test results of an application therefore project teams faced with numerous questions around it.
</p>

However, when project do carry out performance testing of their applications &#8211; particularly internet facing web application, there are quite few pitfalls that prevent that exercise to be effective. Most of these mistakes are made during planning of the performance testing itself. Anecdotal performance objectives are frequently specified by project sponsors and other stakeholders which leads to either nonsensical or far too ambitious performance goals. Performance test planning needs to ensure that all performance tests are conducted against realistic data-driven goals. Projections based on historic user load with explicable extrapolation parameters need to be applied to arrive at future user load. 

This post intends to provide a guide to doing performance testing effectively by way of identifying some of these pitfalls and doesn&#8217;t cover basic hygiene issues around parity of environment and application version. These are written keeping in mind a typical web application with web pages being served back to the user along with a bunch of supported resources and API request however, most of these are applicable for web applications which only serve API requests.

#### 1. Obsessing over TPS

Almost every project starts by identifying the current transaction rate in form of TPS (transaction per second) or something similar. Like so many other project subjects, this also falls prey to the fact that transaction itself is interpreted differently by various stakeholders involved. While it stands for a &#8220;business transaction&#8221; for project sponsors and product owners like orders, add to cart, online payments, viewing invoice etc, its often interpreted as web requests by web developers and a whole another operating system parameter by administrators.

TPS is surely a key outcome expected from a performance test exercise however, its often confused as an input into the performance run instead and a sole input into the performance test planning. What needs to be understood is the fact that targeted TPS needs to be accompanied by other key inputs for adequate performance test planning. This includes metrics like user or consumer concurrency, user session duration, page views per session. These act as key inputs for setting up a performance run which simulates adequate number of concurrent users transacting on the application. In absence of these, by simply varying the number of concurrent users, you can impact the transaction rate. To help understand this a bit better, imagine if 1 user requesting 10 pages one after the other and 10 users requesting 1 page at the same time will have the same workload profile? Will both these workloads consume the resources in the exact same manner? Need I say more.

#### 2. Most popular transactions only

Another one is when project teams focus on one or few of the business transactions which attract most traffic. This leads to inaccurately simulating the conditions which will occur in production systems and may lead to different results. Imagine leaving out a business transaction which is infrequently used however when used, can eat up lot of your resources thereby leaving other requests struggling to be served at all or be served in time.

Therefore, its important to cover as much of the functional scope of the application as possible and do it in the right transaction mix as well. Historic data can provide great insights into the ratio of various business transactions and same mix of workloads can be simulated during performance testing.

#### 3. Not eliminating the noise

Quite often the application environment being used as target environment for performance testing is catering to other workloads at the same time as well which usually wont be present in the application&#8217;s production environment. This could be other traffic on the same application or another application sharing the environment. Such factors can introduce noise in your results by taking away crucial processing time or processing space therefore, negatively impacting your performance OR accessing common data or storage areas hence, making it available quicker. Ideally, such workloads should be eliminated from the environment while conducting performance run.

Another kind of noise observed frequently is enabled debuggers or log levels or monitoring of the application over the network which may not be there in production environment taking away processing time as well as network resources of the server. Make sure to eliminate such configurations too.

Yet another one is the inclusion of requests to resources from other servers or applications in the test scripts. Web pages typically include image or script resources from 3rd parties for various reasons and including them in the script will only inaccurate reflect on the response time and throughput of the target application and servers. This could become an issue if one of those transactions has a response time related SLA.

#### 4. The-mad-user simulation

How many times I have seen testers writing performance test scripts with no lag between consecutive web requests. Even though they have worked out all the transactions in the right mix, just didn&#8217;t space them out. Behave like a user, take time between web requests, if its meant to be there e.g. page requests. Randomize the lag to reflect varying user behavior.

An easy way to identify range of such lag is by looking at the average session time of a user and average number of pages visited. E.g. if a user is visiting 3 pages in a 1 minute session, the user must have taken 30 seconds between a page request and the next. Based on the source of your information for session time, the number may be inflated because of latency and technology involved which can be offset by reducing it somewhat.

#### 5. Not having a baseline

Suppose you are working with an application which isn&#8217;t in production yet therefore, there is no information available about its current performance. You run a few performance run with x concurrent users &#8211; per your projected load and wonder whether the recording response time of various transaction reflects accurately the performance of those transactions. Even worse could be a scenario where the recorded response time of some transactions varies dramatically every run though providing you with a better than expected transaction rate overall. This necessitates the need for a baseline performance. 

To address this, you should always start by conducting a performance test with a single user simulated across the transaction mix for a decent amount of time. This will give you readings where the transaction had practically all the resources available to itself and no outside aspect affected its performance in any way. There might be application profiling required to be carried out if such reading itself isn&#8217;t acceptable for performance requirement reasons or against available performance baseline from history. However, in absence of that, you now have a baseline which should be monitored with systematically increasing the number of concurrent users to see if this baseline holds.

![User tipping point](/resources/user-tipping.png)

Ideally, you would expect it to stay flat. If it holds up-to a certain concurrency beyond which there&#8217;s a tipping point where it starts to go upwards, this is a typical sign of bottleneck in the system which needs to be investigated and addressed, as illustrated above. This could typically be a thread or object pool in the application server or a limit specified in another layer e.g. load balancer, database max connections etc.

If, on the other hand, the execution time linearly rises with the increase in number of users. That is also a sign of design flaws within the application (or the server, if its not a proven system). This could also be a sign of something else for which you need to read the next one.

#### 6. Not considering test machine&#8217;s resources

While we pay attention to sizing of the application infrastructure for the project volumetric, sometimes the same attention isn&#8217;t given to allocating ample resources to the test machines. For any web application, your performance is equally dependent on the processing power and the network conditions of the consumer/client. For example, the CPU of a single test PC simulating 5000 users for a large-scale internet portal will surely be choked by simply managing those 5000 threads. Such a scenario will not generate the workload in line with the required workload profile in the first place. Therefore, appropriate number of test machines with sufficient resources need to be allocated in a suitable network location to execute performance tests. 

You also need to consider the network bandwidth consumption of the test machine when working out how many such test machines will be needed because you may see a linear increase in execution time across various transaction with time, if you have a network choked at the test machine.

#### 7. Not running it long enough

Lastly, running performance runs briefly may give you desired results pretty quickly which can statistically be extrapolated to make you feel that the performance goals have been or can be met. However, there are more applications out there that fall over time, periodically than there are ones which do not perform well regularly. This is for a simple reason of poor resource management which is a slow poison therefore, you need to be at it for some time to see it take effect. Though these issues can be captured with application profiling as well yet, there are some which do not show up in that environment and concurrent steady load is the only way to weed them out. For an internet-facing application with external users, consider performance testing it for a whole 12 or 24 hours and capture resource consumption from the servers in that duration. This should give you good indication of whether you will be fixing one of these in near future.

#### Conclusion

Don't mess up. If you have taken up to performance test an application, do it with conviction of a scientific mind.

If you are interested in optimizing web page performance in the browser, read my post on it as well - [Web page performance & external Javascripts](/2016/05/25/what-external-scripts-gotta-do-with-page-performance/)