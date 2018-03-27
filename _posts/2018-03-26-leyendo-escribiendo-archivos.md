---
layout: post
comments: true
title:  "Leyendo y Escribiendo archivos"
date:   2018-03-25 13:21:18 +0200
categories: jekyll update
tags: read write open readline writelines
---

Para leer o escribir archivos en python tenemos que abrir archivos en diferentes modos según la acción que queramos (lectura, escritura...)

Para abrir archivos utilizamos el método [`open()`](https://docs.python.org/3.5/library/functions.html#open)

El método `open()` devuelve un `file object` (llamado _file handle_) que dependerá del modo utilizado para abrir el archivo

- Cuando abrimos un archivo en **modo texto**  (`w`, `r`, `wt`, `rt`, etc...) devuelve una instancia de una subclase de [**`io.TextIOBase`**](https://docs.python.org/3.5/library/io.html#io.TextIOBase) (clase base para streams de texto). 

- Cuando abrimos un archivo en **modo binario** devuelve una instancia de una subclase de [`io.BufferedIOBase`](https://docs.python.org/3.5/library/io.html#io.BufferedIOBase) 

## Leer Archivos 

 Al abrir un archivo en modo lectura, se nos devuelve un objeto con acceso a métodos tales como:
- [`read(size)`](https://docs.python.org/3.5/library/io.html#io.BufferedIOBase) → Lee el archivo y devuelve un _string_ ([`str`](https://docs.python.org/3.5/library/stdtypes.html#str)) del stream con un máximo de `size` caracteres. Si `size` está vacio devuelve hasta `EOF` (end of file)
- [`readline(size)`](https://docs.python.org/3.5/library/io.html#io.TextIOBase.readline) → Lee el archivo hasta un final de linea o de archivo y devuelve un _string_ ([`str`](https://docs.python.org/3.5/library/stdtypes.html#str)). Con `size` fijamos el máximo de caracteres devueltos
- [`readlines(hint)`](https://docs.python.org/3.5/library/io.html#io.IOBase.readlines) → Devuelve una lista de lineas desde el stream

``` python
f = open("data.txt", "r")
lines = f.read()
line = f.readline()
```

``` python
f = open('/home/ubuntu/workspace/files/relative_data.txt', 'r')
content = f.read()
f.close()
print(content)
```

Para obtener las lineas de un archivo podemos hacer
``` python
f = open('/home/ubuntu/workspace/files/relative_data.txt', 'r')
lines = f.readlines()
print(lines)
# ['This is my first file\n', 'This file\n', 'contains three lines\n']
```

Aunque tambien podemos hacer... 
```
f = open('data.txt', 'r')
for line in f:
    print(line)
```

Cuando abrimos un archivo en modo, se genera un cursor que va cambiando su posición a medida que operamos con el archivo 

``` python
f = open("test.txt",'r',encoding = 'utf-8')
f.read(4)    # read the first 4 data → 'This'
f.read(4)    # read the next 4 data → ' is '
f.read()     # read in the rest till end of file → 'my first file\nThis file\ncontains three lines\n'
f.read()  # further reading returns empty sting
```

Podemos cambiar la posición del cursor con el método [`seek()`](https://docs.python.org/3.5/library/io.html#io.IOBase.seek) o averiguar su posición con el método [`tell()`](https://docs.python.org/3.5/library/io.html#io.IOBase.tell) 


## Escribir Archivos 

Al abrir un archivo en modo lectura, se nos devuelve un objeto con acceso a métodos tales como:
- [`write(s)`](https://docs.python.org/3.5/library/io.html#io.TextIOBase.write) → Escribe el string `s` en el stream y devuelve el número de caracteres escritos
- [`writelines(lines)`](https://docs.python.org/3.5/library/io.html#io.IOBase.writelines) → Escribe una lista de lineas (separadas por `\n`) en el stream

``` python
f = open('newfile.txt', 'a')
lines = ['Hello','World','Welcome','To','File IO']
text = '\n'.join(lines)
f.writelines(text)
f.close()
```

## Modos de apertura de archivos

### Modos Básicos
- `r` → (por defecto) Abre un archivo para lectura
- `w` → Abre un archivo para escritura. Crear un nuevo archivo si no existe o lo sobrescribe si ya existe
- `a` → Abre un archivo para añadir texto al final del archivo si ya existe. Si no existe lo crea.

### Modos Extra
- `x`	→ Abre un archivo para creación exclusiva. Si el archivo ya existe la operación falla.
- `t`	→ Abre un archivo en modo texto. (default)

### Modos Combinados
- `b` (`rb`, `wb`, `ab`) → Abre archivo en modo binario
- `+` → Abre archivo para actualización (lectura y escritura)
    - `r+` → lectura/escritura (si el archivo no existe, lanzará un error. Si existe sobrescribe el archivo)
    - `w+` → lectura/escritura (si el archivo no existe, se crea. Si existe sobrescribe el archivo)
    - `a+` → lectura/añadir (si el archivo no existe, se crea. Si existe añade el contenido al final)

## Recursos

- <https://www.programiz.com/python-programming/file-operation>