---
layout: post
title:  "Ruta y Directorio del archivo actual"
date:   2018-03-24 13:21:18 +0200
categories: jekyll update
tags: join dirname abspath realpath __file__
---
Utilizando la variable global `__file__` podemos averiguar para cada archivo tanto el nombre del archivo en cuestion como el directorio en el que se encuentra (y su directorio padre)

Para ello el modulo [`os`](https://docs.python.org/2/library/os.html) nos ofrece el método [`path`](https://docs.python.org/2/library/os.path.html#module-os.path) con una serie de métodos muy útiles para este objetivo:

-  [`join()`](https://docs.python.org/2/library/os.path.html#os.path.join) → Junta trozos de rutas para generar una ruta final de manera inteligente

-  [`dirname()`](https://docs.python.org/2/library/os.path.html#os.path.dirname) → Devuelve el directorio del path dado
    `os.path.dirname('/Users/juanma/PROJECTS/PYTHON/demos/test.py')` → `/Users/juanma/PROJECTS/PYTHON/demos`

-  [`abspath()`](https://docs.python.org/2/library/os.path.html#os.path.abspath) → Devuelve la ruta absoluta y normalizada del path dado
    `os.path.abspath(__file__)` → `/Users/juanma/PROJECTS/PYTHON/demos/test.py`

-  [`realpath()`](https://docs.python.org/2/library/os.path.html#os.path.realpath) → Devuelve la ruta canonica del archivo dado
    `os.path.realpath(__file__)` → `/Users/juanma/PROJECTS/PYTHON/demos/test.py`


¿Qué diferencia hay entre `abspath` y `realpath` si parece que producen el mismo resultado? No mucha, pero [aquí](https://stackoverflow.com/questions/37863476/why-use-both-os-path-abspath-and-os-path-realpath#40311142) teneis una respuesta 

Así, este ejemplo
{% highlight python %}
import os

FILE = __file__
REALPATH = os.path.realpath(__file__)
ABSPATH = os.path.abspath(__file__)
DIRNAME = os.path.dirname(os.path.realpath(__file__))

print("{} \t\t\t\t\t\t ← __file__".format(FILE))
print("{} \t ← os.path.realpath(__file__)".format(REALPATH))
print("{} \t ← os.path.abspath(__file__)".format(ABSPATH))

print("{} \t\t ← os.path.dirname(os.path.realpath(__file__))".format(DIRNAME))
{% endhighlight %}

Nos devolverá algo asi...


{% highlight bash %}
test.py 					 ← __file__
/Users/juanma/PROJECTS/PYTHON/demos/test.py 	 ← os.path.realpath(__file__)
/Users/juanma/PROJECTS/PYTHON/demos/test.py 	 ← os.path.abspath(__file__)
/Users/juanma/PROJECTS/PYTHON/demos 		 ← os.path.dirname(os.path.realpath(__file__))
{% endhighlight %}