# Resumen _BASH_
Pequeño Resumen BASH
(Perdón por las posibles erratas)

## [Shebang](https://es.wikipedia.org/wiki/Shebang).

El _shebang_ correcto sería:
```bash
#!/usr/bin/env bash

# Esto es un comentario
# Aquí debajo ya puede empezar el código

echo "Hoy es: $(date +%d-%m-%y)"
```

## Variables, listas y diccionarios.

Una _variable_ en _bash_ no es necesario declararla. Se declaran de la siguiente forma:

```bash
nombre='Maria'
```

Entre el nombre de la variable, el '=' y el valor que se le asigna no pueden haber espacios.
Para llamar a una variable se hace anteponiendo un _'$'_.
```bash
echo $nombre
```

Se puede usar la siguiente notación para llamar a una variable:
```bash
numero1=23
numero2=32

echo "${numero1}${numero2}"
```

Una _lista_ (vector, array o arreglo) se crea de la siguiente manera:
```bash
numero=12
milista=('primer valor' "${numero}" 'fin de lista')
```

Los valores de la lista se llaman como en casi todos los lenguajes:
```bash
echo ${milista[1]}
```
A diferencia de python, el primer valor es: _'${milista[1]}'_.

Forzosamente hay que encerrar ente llaves el nombre de la lista.

#### Ejemplo: Crear una lista con el contenido de un directorio
```bash
contenidodir=(*)
# Aunque funcione, esto está mal: 
#     contenidodir=($(ls))
echo ${contenido[2]}
```

Un _diccionario_ (array asociativo) se crea asi:
```bash
# Los diccionarios si son necesarios declararlos para poder usarlos
declare -A midiccionario
midiccionario['nombre']='Maria'
midiccionario['apellido']='Barranco'

echo ${midiccionario['apellido']}
```

## Sentencia _'for'_

Sintaxis:
```bash
for x in ${milista[@]}; do
    # esto mostrará cada elemento de la lista
    echo "$x"
done
```

_'for'_ para recorrer números:
```bash
for x in 20..30; do
    echo $x
done
```

_'for'_ al estilo _ansi C_:
```bash
# Esto imprime desde 10 hasta 20 en saltos de 1 en 1
for (( x=10; x <= 20; x++ )); do
    echo $x
done
```

_'for'_ para recorrer los ficheros de un directorio:
```bash
for x in *; do
    mv "$x" "${x}_old"
done
```

## Sentencia _'if'_

La sintaxis es:
```bash
if [[ condicion1 ]]; then_
    ejecución si condicion1
elif [[ condicion2 ]]; then
    ejecución si condicion2
elif ....
    ....
    ...
else
    ejecución si nada de lo anterior
fi
```
Solo son obligatorias las 2 primeras líneas y la úiltima

```bash
directorio='/home/maria/'
fichero='documento.doc'

if [[ -d "${directorio}" ]]; then
    echo "${directorio} existe y es un directorio"
else
    echo "${directorio} no existe"
fi

if [[ -f "${fichero}" ]]; then
    echo "${fichero} existe y es un fichero regular"
elif [[ -f "${directorio}${fichero}" ]]; then
    echo "${fichero} está en ${directorio}"
elif [[ "$(pwd)" != "${directorio}" ]]; then
    echo "No existe ${fichero} ni $(pwd), ni en ${directorio}."
else
    echo "no encuentro ${fichero}"
fi
```

[Más información sobre operadores aquí](http://mywiki.wooledge.org/BashGuide/TestsAndConditionals#Conditional_Blocks_.28if.2C_test_and_.5B.5B.29)

Para condiciones númericas se usa: _'(( numero1 == numero2 ))'_:
```bash
numero1=23
numero2="44"

if (( numero1 >= numero2 )); then
    echo "Esto no se ejecutará"
else
    echo "Esto sí"
fi
```

Nótese que las _variables numéricas_ cuando van entre (( )) no llevan _'$'_.


## Sentencias _'while'_ y _'until'_

- while [[ condición ]] --> Ejecuta _mientras_ se dé la condición.
- until [[ condición ]] --> Ejecuta _hasta_ que se da la condición.

```bash
contador=20
while (( contador > 1 )); do
    echo "Contador: ${contador} es mayor que 1"
    # aquí debajo se resta uno a contador
    ((contador--))
done
```

```bash
contador=20
until (( contador == 5 )); do
    echo "Contador no es 5"
    # aquí debajo se resta uno a contador
    contador=$((contador-1))
done
```
