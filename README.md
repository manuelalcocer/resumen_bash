# Resumen _BASH_
Pequeño Resumen BASH

## [Shebang](https://es.wikipedia.org/wiki/Shebang).

El _shebang_ correcto es:
```bash
#!/usr/bin/env bash
```

## Variables, listas y diccionarios.

Una variable en _bash_ no es necesario declararla. Se declaran de la siguiente forma:

```bash
nombre='Maria'
```

Entre el nombre de la variable, el '=' y el valor que se le asigna no pueden haber espacios.
Para llamar a una variable se hace anteponiendo un _'$'_.
```bash
echo $nombre
```


