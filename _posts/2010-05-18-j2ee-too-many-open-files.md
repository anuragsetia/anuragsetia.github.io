---
title: 'J2EE: Too many open files'
author: Anurag Setia
layout: post
tags:
  - java
  - too many open files
---
<span style="font-family:Trebuchet MS, sans-serif;">Now this thing is eating my head since yesterday, and I have done all i could to stop it from coming up again on my server.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">The issue is with Checkpoint production server where the following error keeps popping up twice a day and the server is literally held up till you restart it &#8211;</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">May 18, 2010 3:03:34 PM org.apache.tomcat.util.net.PoolTcpEndpoint acceptSocket</span>  
<span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">SEVERE: Endpoint ServerSocket[addr=0.0.0.0/0.0.0.0,port=0,localport=19638] </span>  
<span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">ignored exception: java.net.SocketException: Too many open filesjava.net.SocketException: Too many open files </span>  
    <span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">at java.net.PlainSocketImpl.socketAccept(Native Method) </span>  
    <span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">at java.net.PlainSocketImpl.accept(PlainSocketImpl.java:384) </span>  
    <span style="color:red;font-family:Courier New, Courier, monospace;font-size:78%;">at java.net.ServerSocket.implAccept(ServerSocket.java:453)</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">Having Googled enough, we reviewed all the jars for reloading itself through out the application, reviewed the whole code for closing all File streams blah blah blah. Nothing worked.</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">Finally, working on getting all the open files in a shell file passing a process id to lsof, found a properties file open a bunch of time. On checking further, realized the ResourceBundle was an instance variable in a frequently used utility class. Changed to static variable, problem solved. The unix/linux commands required to check the no. of open files that can be opened by a user are typically in ulimit and the hard limit can be checked by&nbsp;</span>  
<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;"></span>  
<span style="font-family:Trebuchet MS, sans-serif;">ulimit -aH</span>

<div>
  <span style="font-family:Trebuchet MS, sans-serif;"><br /></span>
</div>

<div>
  <span style="font-family:Trebuchet MS, sans-serif;">On the other hand, the command to check the no. of open files per process for any user is actually somewhere else i.e. limits.h and can be checked by</span>
</div>

<div>
  <span style="font-family:Trebuchet MS, sans-serif;"><br /></span>
</div>

<div>
  <div>
    <span style="font-family:Trebuchet MS, sans-serif;">grep OPEN_MAX /usr/include/sys/limits.h</span>
  </div>
</div>

<div>
  <span style="font-family:Trebuchet MS, sans-serif;"><br /></span>
</div>

<span style="font-family:Trebuchet MS, sans-serif;"><br /></span><span style="font-family:Trebuchet MS, sans-serif;">This <a href="http://www-01.ibm.com/support/docview.wss?uid=swg21067352" rel="nofollow noopener noreferrer" target="_blank">IBM technote</a>, though is handy with commands to get to the open file quickly.</span>