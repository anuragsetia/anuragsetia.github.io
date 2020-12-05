---
title: 'Introduction to Hacking &#8211; SQL Injections'
author: Anurag Setia
layout: post
tags:
  - hacking
  - coding
---
<p align="justify">
  <span style="font-size:78%;color:#ff0000;">Disclaimer &#8211; All the post of this series are meant to discuss the basics behind the art of hacking and not to provide exploits, irrespective of the fact whether I am aware of any or not. Assure you that the stuff provided is surely more than sufficient for any intelligent person to come up with a good hack.</span>
</p>

SQL Injections, this is one of a well known techniques to bypass authentication where there is a backend database involved.

**<span style="color:#0000ff;">Idea behind it</span>** &#8211; On a normal login page, username and password entered by the user are stored in a database and when anyone tries to login, a query is fired on the database to check if the credentials entered are correct or not. The query fired would be something like this

<span style="font-family:courier new, courier, mono;color:#0000ff;">SELECT * FROM USER_TABLE WHERE USERNAME=&#8217;<em><span style="color:#990000;">WAT_I_ENTERED</span></em>&#8216; AND PASSWORD=&#8217;<em><span style="color:#990000;">WHAT_I_DONT_KNOW</span></em>&#8216;</span>

Now, in most of the cases, developers just take input on the page and concatenate it in a query which is then fired on the database. If the query returns any results, its a valid user who is then proceeded to the next page; if it doesnt, the user is thrown out back to the login page, typically. In a situation like this, its not very difficult for anyone to login to the site even without knowing a password. All it requires is some basic knowledge of writing SQL queries. You can tailor your input to malform the SQL query being fired on the database and help yourself get in.

**<span style="color:#0000ff;">How its done</span>** &#8211; The first step would be to check if the site we are trying to get into is a suitable candidate for SQL Injection i.e. there is a database behind and the query being fired is being built using concatinating the inputs in a static string as shown above. To check this, all that needs to be done is input a single quote (&#8216;) in any of the fields and a possible valid value in the other one. What a quote does it, it malforms the SQL and the application would get error from the database when the query is not well formed. If you see an error page, or application error msg in any of the corners of the page, you are on. If you dont see any of this stuff and get back to the login page which is not showing any error anywhere as well, dont get disheartened, you still have a chance &#8211; it really depends on the error handling of the application what you see.

Once this is done, we need to tailor the input values we would need to input to get through the login. This would require inputting something that would not only, when concatenated to the query string, form a valid SQL Query but also return some result. So, basically I am targetting to fire something like this to the database.

<span style="font-family:courier new, courier, mono;color:#0000ff;">SELECT * FROM USER_TABLE WHERE USERNAME=&#8221; OR 1=1 <span style="color:#00ff00;">&#8211;&#8216; AND PASSWORD=&#8217;ANYTHING&#8217;</span></span>

<span style="font-family:courier new, courier, mono;color:#0000ff;">or</span>

<span style="font-family:courier new, courier, mono;color:#0000ff;">SELECT * FROM USER_TABLE WHERE USERNAME=&#8217;<em><span style="color:#990000;">WAT_I_ENTERED</span></em>&#8216; AND PASSWORD=&#8221; OR 1=1 <span style="color:#00ff00;">&#8211;&#8216;</span></span>

As is obvious from the above queries, in one example I have entered **<span style="background-color:#ffff00;">&#8216; OR 1=1 &#8212;</span>** as username and &#8216;ANYTHING&#8217; as a password which wouldnt matter as it gets commented in the query and in the second example, when I knew a valid username, I entered a valid username and password as <span style="background-color:#ffff00;"><strong>&#8216; or 1=1 &#8212;</strong></span><span style="background-color:#ffffff;">. Now both these queries would return the whole table in the result set and would surely take me through the login hassle. Simple, aint it.</span>

**<span style="color:#0000ff;">Why we talking this</span>** &#8211; The objective of discussing this is to make all the developers aware of the possible consequencies of un-elegent programming. Usage of concatenation of strings to form an SQL Query is one of the bad programming techniques and SQL Injects are one of the possible techniques used to exploit it. **<span style="color:#0000ff;">How we can prevent SQL Injections </span>**is by using parameterized queries as far as possible, which prevents us from SQL Injections because then, any tailored input would act as a parameter for a database column in the query and would NOT be able to malform the query in any form.

Keep coding !!!!!!!!