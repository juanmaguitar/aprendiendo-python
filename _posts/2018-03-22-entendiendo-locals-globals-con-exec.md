---
layout: post
title:  "Variables locales y globales"
date:   2018-03-22 13:21:18 +0200
categories: jekyll update
tags: locals globals variables scope namespace
---

Em Python cada archivo es un modulo que puede ser importado
Cada modulo tendrá sus variables globales y locles 
- Las variables globales seran accesibles desde cualquier función.
- Las variables locales sólo seran accesibles desde el módulo o función donde estén definidos.  

La función [`globals()`](https://docs.python.org/3.5/library/functions.html#globals) devuelve el _namespace_ global, que es la relación de elementos globales (variables y funciones) definidas para cada módulo (cada archivo) y accesible para las funciones definidas en él

La función [`locals()`](https://docs.python.org/3.5/library/functions.html#locals) devuelve el _namespace_ local, que es la relación de elementos globales (variables y funciones) definidas para una función en concreto

## Ejemplo1

{% highlight python %}
def f(): 
    print(msg) 

msg = "I love Paris in the summer!"
f()
{% endhighlight  %}

La variable global `msg` se define fuera (global). Al ejecutar `f()` busca un `msg` local y como no lo encuentra utiliza el `msg` global  (`I love Paris in the summer!`)

## Ejemplo2

{% highlight python %}
def f(): 
    msg = "I love London!"
    print(msg)

msg = "I love Paris!" 
f()
{% endhighlight  %}

La variable global `msg` se define fuera (global). Al ejecutar `f()` busca un `msg` local y como lo encuentra utiliza el valor del `msg` local (`I love London!`)

## Ejemplo3

{% highlight python %}
def f():
	global msg
	print(msg)
	msg = "Only in spring, but London is great as well!"
	print(msg)

msg = "I am looking for a course in Paris!"
{% endhighlight  %}

Tambien podemos especificar (con `global`) dentro de la función `f` que queremos utilizar la variable global `msg`. Al ejecutar `f()` utilizará la variable global `msg`, tanto para imprimir su valor como para asignarle nuevos valores

## Ejemplo4

{% highlight python %}
def f():
	print(msg)
{% endhighlight  %}

Las variables globales se limitan a cada modulo. Aunque en otro modulo hayamos definido la variable global `msg`, ésta variable no existe para el resto. Si intentamos utilizar esta variable sin haberla definido, python lanzará un error

## Ejemplo5

**example5.py**
{% highlight python %}
msg = "Hello World!"

from example51 import f
{% endhighlight  %}

**example51.py**
{% highlight python %}
def f():
	print(msg)
{% endhighlight  %}

Las variables globales se limitan a cada modulo. Esto se aplica tambien para cuando importamos una función. Si esta función importada no tiene definida la variable en su archivo, dará error

## Ejemplo6

**example6.py**
{% highlight python %}
from example61 import f
f()
{% endhighlight  %}

**example61.py**
{% highlight python %}
from example62 import msg

def f():
  print(msg)
{% endhighlight  %}

**example62.py**
{% highlight python %}
msg = "Hello World!"
{% endhighlight %}

Sin embargo, si que podemos importar sin problema variables y funciones definidas en otros archivos para ejecutarlos en otro lugar

----
<br/>
Aqui se pueden todos estos ejemplos testeados...

<iframe height="400px" width="100%" src="https://repl.it/repls/ImperturbableDisloyalRule?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<br/>
### Recursos

- <https://gist.github.com/dean0x7d/df5ce97e4a1a05be4d56d1378726ff92>