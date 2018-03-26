---
layout: post
title:  "Deteccion llamadas como módulo con __name__"
date:   2018-03-20 13:21:18 +0200
categories: jekyll update
tags: modulos deteccion __main__
---

Un tema interesante en python es el valor de la variable global `__name__`

A cada archivo se le asigna un valor a la variable global `__name__`

{% highlight python %}
if __name__ == '__main__':
	print('This program is being run by itself')
else:
	print('I am being imported from another module')
{% endhighlight %}


Si el archivo se llama directamente adquiere el valor `__main__`, si no adquiere otro valor

***test.py***
![My helpful screenshot]({{ "/assets/2018-03-20-deteccion-modulo-__name__/name-main.png" | absolute_url }})

Con esta lógica podemos detectar si un archivo se ha llamado directamente o como módulo

<div class="myvideo">
   <video  style="display:block; width:100%; height:auto;" autoplay controls loop="loop">
       <source src='{{ "/assets/2018-03-20-deteccion-modulo-__name__/python-main.mp4" | absolute_url }}' type="video/mp4" />
   </video>
</div>
  
<br/>
### Recursos

- <http://ibiblio.org/g2swap/byteofpython/read/module-name.html>
- <https://docs.python.org/3/library/__main__.html>