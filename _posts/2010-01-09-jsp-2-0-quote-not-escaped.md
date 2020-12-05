---
title: 'JSP 2.0 &#8211; Quote not escaped'
author: Anurag Setia
layout: post
tags:
  - Jsp
---
<span style="font-family:verdana;">Encountered a weird problem today, a running application on Linux/Tomcat 5.5 starting crashing at various places after re deployment without much code issues.</span>  
<span style="font-family:verdana;">Issue came up in all the JSP pages which had request.getParameter call within value attribute of any tag. Logs showed the following JasperException</span>  
<span style="font-family:verdana;"></span>  
<span style="font-family:verdana;color:#ff0000;">Attribute value request.getParameter(&#8220;XXX&#8221;) is quoted with &#8221; which must be escaped when used within the value</span>  
<span style="font-family:verdana;"></span>  
<span style="font-family:verdana;">Simple fix, append the following to JAVA_OPTS variable in catalina.sh</span>  
<span style="font-family:Verdana;"></span>  
<span style="font-family:courier new;color:#000099;">-Dorg.apache.jasper.compiler.Parser.STRICT_QUOTE_ESCAPING=false</span>  
<span style="font-family:verdana;"></span>  
<span style="font-family:verdana;">Works !!!</span>