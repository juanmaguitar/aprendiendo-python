---
layout: post
title:  "Mostrando el contenido de globals() y locals()"
date:   2018-03-22 13:21:18 +0200
categories: jekyll update
tags: locals globals
---

Para mostrar el contenido de `locals()` y `globals()` podemos hacer

{% highlight python %}
a = 5

def show_globals():
  print("## GLOBALS ##")
  for key, value in list(globals().items()):
    print("{0} → {1}".format(key, value))

def show_locals():
  a = 5
  print()
  print("## LOCALS ##")
  for key, value in list(locals().items()):
    print("{0} → {1}".format(key, value))
  assert locals() != globals()

show_globals()
show_locals()

assert globals() == locals()
{% endhighlight %}
 
Lo que nos devolverá la lista de valores de ambos `namespaces`
{% highlight bash %}
## GLOBALS ##
__name__ → __main__
__doc__ → None
__package__ → None
__loader__ → <_frozen_importlib_external.SourceFileLoader object at 0x1084ff390>
__spec__ → None
__annotations__ → {}
__builtins__ → <module 'builtins' (built-in)>
__file__ → test5.py
__cached__ → None
a → 5
show_globals → <function show_globals at 0x108483f28>
show_locals → <function show_locals at 0x108ae1b70>

## LOCALS ##
a → 5
{% endhighlight %}

Algunos de estos valores del namespace global tienen usos interesantes como comento en otros posts

<br/>
### Recursos

- <https://stackoverflow.com/a/47996201>