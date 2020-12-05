---
title: Basic Java Tips and Tricks
author: Anurag Setia
layout: post
---
<span style="font-family:verdana;"></span>  
<span style="font-family:verdana;">Following are just a few tips and tricks around java technologies &#8211;</span>

  * <span style="font-family:verdana;">When writing JDBC code, use PreparedStatement inspite of Statement as far as possible coz of more than one reasons. Its not only precompiled (which means if you are using the same object to fire the query multiple times on the db, its compiles only once and makes execution faster) but also it safeguards you from SQL Injections. To avoid SQL Injections, always used a parameterized query instead of concatenating the parameters to the query string. </span>
  * <span style="font-family:verdana;">When writing database queries, always prefer joins to in queries. They are more efficient and respond quicker. Also, when firing a SELECT query on IBM DB2, always suffix WITH UR to the query to prevent any locks on the database. </span>
  * <span style="font-family:verdana;">Whenever invoking a static method, invoke it on the class wherever possible and not on object. </span>
  * <span style="font-family:verdana;">When designing an application and stuck in deciding where to put a certain method, always go by noun and verb theory (thats what I call it), entities are nouns and operations are verbs. Eg. Accountants transfer salaries, therefore, the operation or method trasferSalary() should be declared in Accountant class. If all the classes dont represent entities, which typically would be the case, then, just see what all data would be involved and which class should have access to it and who all would that class be exposed to and whose responsibility this operation is. </span>
  * <span style="font-family:verdana;">Avoid using replace method in String class, it has a probability of failing you at some point. Use StringBuffer class instead. </span>
  * <span style="font-family:verdana;">To get a formatted Date object, use SimpleDateFormat class instead of playing around with the Date string. </span>
  * <span style="font-family:verdana;">Always have a null check before invoking an operation on an object whenever you are not sure if the object would be available. </span>
  * <span style="font-family:verdana;">Catching all exceptions where they occur is not always the best way, for example, if there is an operation doesnt return anything, takes a value object and updates a row in the database, if there is an exception occuring due to the value object not being consistent shouldnt be handled in this method but should be thrown back to the calling method. </span>
  * <span style="font-family:verdana;">When comparing a String object to a String literal for equalness, always use STRING_LITERAL.equals(STRING_OBJ), saves you from a Null check and gives you the same result anyways. </span>
  * <span style="font-family:verdana;">When computing some value from the data coming from the same row of a database query, prefer computing it in the query itself if a db function is available. Normally, database functions are more efficient than computing in the code later.</span>

<span style="font-family:verdana;">Will be back with more now and then.</span>