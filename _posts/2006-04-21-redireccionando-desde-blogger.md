---
id: 112
title: Redireccionando desde blogger
date: 2006-04-21T21:04:00+00:00
author: Linkita
layout: post
guid: http://qukiyegi.dns-privadas.es/?p=112
permalink: /2006/04/redireccionando-desde-blogger/
blogger_blog:
  - sonnei.blogspot.com
blogger_author:
  - Linkitahttp://www.blogger.com/profile/08969869659383343445noreply@blogger.com
blogger_permalink:
  - /2006/04/redireccionando-desde-blogger.html
categories:
  - Blog
  - Curiosidades
---
<div style="text-align: center;">
  <img title="Blogger forward" alt="Blogger forward" src="http://www.alvarezperea.com/alberto/weblog/wp-content/imagenes/blogger_0.jpg" style="text-align: center;" border="0" height="169" width="172" />
</div>

La verdad es que lo peor de <span style="font-weight: bold;">mudarse de blogger a otro cms</span> son las visitas que dejas atrás. Y no perder a los perezosos que aún no se han enterado de que tienes otra dirección.

Pues bien, hay un método para hacer que al teclear una dirección de blogger te lleve a otro dominio que prefieras (woooo redirección). Yo lo he probado y funciona: <a style="font-weight: bold;" href="http://linkitab.blogspot.com/">linkitab.blospot.com</a>.

Me quedé bastante sorprendida cuando lo ví. No se me había ocurrido que se podría hacer eso&#8230;

Hay que crear el blog (si ya esta creado, pues ná) y en la plantilla poner el siguiente código:  


> <!DOCTYPE HTML PUBLIC &#8220;-//W3C//DTD HTML 4.01 Transitional//EN&#8221;  
> &#8220;http://www.w3.org/TR/html4/loose.dtd&#8221;>  
> <html>  
> <head>  
> <title>Redireccionando…</title>  
> <meta http-equiv=&#8221;Content-Type&#8221; content=&#8221;text/html; charset=iso-8859-1&#8243;>  
> <META HTTP-EQUIV=&#8221;Refresh&#8221;  
> CONTENT=&#8221;1; URL=http://www.ladireccion.com/delaweb/alaquequieres/redireccionar&#8221;>  
> </head>  
>  __  
> <body>  
> <div align=&#8221;center&#8221;>Redireccionando… Si tarda, <a  
> href=&#8221;http://www.ladireccion.com/delaweb/alaquequieres/redireccionar&#8221;  
> title=&#8221;Impugnaciones MIR&#8221; target=&#8221;_self&#8221;>pulsa aqu&iacute;</a>._  _</div>  
> </body>  
> </html>_</p> 
> 
>  __

Ojo, es conveniente deshacerse de la barra de blogger  
<span style="font-style: italic;"></span>  


> <span style="font-style: italic;">#b-navbar {</span>  
>  <span style="font-style: italic;">visibility:hidden;</span>  
>  <span style="font-style: italic;">height:0px;</span>  
>  <span style="font-style: italic;">}</span><span style="font-style: italic;"></span></p>
Con bitácoras también [funciona](http://linkita.bitacoras.com/), pero hay que poner el código en el fichero <span style="font-weight: bold;">index.bit</span> y en lugar de hacer desaparecer la barra de blogger, hacer desaparecer la publicidad. Para ello, este código justo antes de la etiqueta <body>:  


> <noframes><body>.</body></noframes></p>
Fácil, rápido e indoloro.

Visto en [moonshadow](http://http//www.alvarezperea.com/alberto/weblog/?p=532).