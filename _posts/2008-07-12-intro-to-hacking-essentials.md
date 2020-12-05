---
title: 'Intro to hacking &#8211; Essentials'
author: Anurag Setia
layout: post
---
<p align="justify">
  <span style="font-size:78%;color:#ff0000;">* Just couldnt sleep thinking that I might be leaving a few souls disappointed with my previous post, so just had to write this one.</p> 
  
  <hr />
  
  <p>
    </span>
  </p>
  
  <p>
    <span style="color:#000000;">A hacker is anyone who has to skills of a hacker and understands the spirit. Skills of a hacker include the following, in my opinion &#8211;</span>
  </p>
  
  <ul>
    <li>
      Atleast one programming language or scripting language.
    </li>
    <li>
      Knowledge of HTML and Javascript.
    </li>
    <li>
      Basic database skills and PL/SQL.
    </li>
    <li>
      Basics of Operating System and networks.
    </li>
    <li>
      Very good troubleshooting skills and logical thinking.
    </li>
    <li>
      Ability to quick-read and understand code patterns.
    </li>
    <li>
      Social Engineering
    </li>
  </ul>
  
  <p>
    Some of these things are neccessary, however, traits like troubleshooting and recognizing code patterns is something one can learn over a period. Anything beyond this would make it easier for the guy to accomplish whatever he wants to just by providing more options. Knowing atleast one high level programming language thoroughly and one scripting language is a real must as is knowledge of Operating systems and HTML.
  </p>
  
  <p>
    Just to give you a small example of how things work while hacking and you can use one of these skills to accomplish a task. Imagine a website which required a password to get through, which of course you dont have. There are multiple ways to find out the password &#8211; ask the site admin(<em><span style="color:#990000;">dont laugh guys, its A way and is really an option</span></em>) OR find out the way authentication would be done by the site and figure out a way to crack it. In a hypothetical situation, suppose the site admin has server side scripting to authenticate his password from some encrypted source to which you have no access to, however, there is a forget password button which sends an email to the site admin with the password in it. Now, in most of the static sites, there is not backend database to store info so most of the information is stored within the web content, either in files other than the pages being served or in the pages as hidden fields <strong>which </strong>can easily be looked up by viewing source for a web page.
  </p>
  
  <p>
    In such a case, we use Java Script Injections. Java Script injections is a technique by which using the browser&#8217;s address bar, we issue java script commands to the browser to dynamically change values of the web page form including the ones which are hidden or read only. So, you know what to do.
  </p>
  
  <p>
    Now, this teaches us a few important lessons as a hacker and as a developer &#8211;
  </p>
  
  <ul>
    <li>
      All hacks are in some way exploiting a loophole left by one of the developers or admins.
    </li>
    <li>
      There is a lot of logical thinking involved in trying to figure out what all are the possible hacks that could be used for a certain target. And of course, common sense.
    </li>
    <li>
      Address bar of Internet Explorer is a powerful tool.
    </li>
    <li>
      Its not a good idea to leave important information in any form in the HTML at all.
    </li>
  </ul>
  
  <p>
    Think the hacking way, understand the hacking spirit and you would develop application that would defy security threats.
  </p>
  
  <p>
    <span style="color:#0000ff;"><em>🙂 If you thought you just learnt a big trick on how to get into a site without authenticate, you are mistaken. This isnt something that would work on most of the sites you land on. It would take a lot more thinking and application than this to use Java Script injection to really accomplish anything at all.</em></span>
  </p>