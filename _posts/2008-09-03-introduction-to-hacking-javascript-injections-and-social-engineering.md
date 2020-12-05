---
title: 'Introduction to Hacking &#8211; Javascript Injections and Social Engineering'
author: Anurag Setia
layout: post

tags:
  - internet applications
  - web apps
---
<p align="justify">
  <span style="font-size:85%;">One of the very commonly used techniques for hacking, when it comes to web sites, is Javascript injections. Javascript Injections are a technique in which, using javascript, we change the content of a page without having to navigate away from it or saving it offline. The most popular example you would find online would be of altering the admin email address which is stored in a hidden field in the page.</span>
</p>

<span style="font-size:85%;"><strong>When to use it</strong><br />I had a situation once where I was filling in a registration form, after it was filled, they showed a confirmation page with all the values that I had filled in as read only labels and on submit, the same information was used to register me. There was this corporate email address field which was validated for not inputting any of the popular public email sites&#8217; domains and I was really apprehensive to give away my satyam id. Thats when I used this technique where i had input my satyam id on the form, and using javascript injection, altered it on the confirmation page to my personal id. So, basically this technique is very handy in lot of situations like this and others.</span>

<span style="font-size:85%;"><strong>How is it done</strong><br />Internet Explorer address bar acts as a shell or a command line for you. So, just view the source of the page, figure out the field you would like to alter and issue the command &#8211;</span>

<span style="font-family:courier new, courier, mono;font-size:85%;">javascript:void(document.form[0].fieldname=value)</span>

<span style="font-size:85%;">This thing works simple as this. To view the cookie stored by the site or to set its values use &#8211;</span>

<span style="font-family:courier new, courier, mono;font-size:85%;">javascript:alert(document.cookie)</span>

<span style="font-size:85%;">I guess this should be enough to show you the way.</span>

<span style="font-size:85%;"><strong>Social Engineering</strong><br />This is an less mentioned commonly used hacking technique. The funda is simple, if you know a person, you know his password. Its a simple discipline which tells you the human behaviour patterns. Eg. people keep passwords which they can easily remember, in office they would keep passwords which would be somewhat relevant to the organization name or the project and at home they would use their personal favorites for the same. Other than the passwords, other information related to a target machine or network or Problem turns out to be really helpful. In one of the hacking stories I read, our guy wanted to get through a university web site. He somehow managed to get through the router and the firewall on the way into the network and managed to get to the database server. Now, he needed the password to get into the database for the sa account (<em><span style="color:#990000;">popular default account in SQL Server</span></em>). So, the dude called up the university webmaster, just to take a chance and told him that he was calling from Microsoft and needed to know the version of SQL server they were using and whether or not they need a certain patch. The webmaster told him to hold on for a second, logged into the database and told him the version. Dude just said thanks and hung up, thought for a minute and entered a couple of passwords which worked. Guess what could have given him the password ? He just listened to the keystrokes carefully and figured out a pattern which told him that the password could be <em>admin </em>followed by a 3 digit number, as it was. So, sometimes, when you need a password, just ask for it 🙂 and thats social engineering.</span>

<span style="font-size:85%;">More on hacking next time.</span>