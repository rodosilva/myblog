+++
date = '2025-02-04T19:55:05-05:00'
title = 'CheatSheet Bash'
+++

## 1. OBJETIVO
La idea de este Post es tener a la mano tanto comandos útiles de Linux como también mostrar la correcta sintaxis de scripts en Bash.

## 2. COMANDOS ÚTILES - EJEMPLOS

### - Comando: sed
**Filtrar y transformar texto**

En este ejemplo lo voy a combinar con el comando `cat` para así filtrar y transformar la salida o resultado del primer comando.

El objetivo es eliminar los números y quedarnos simplemente con las palabras.

Contenido del archivo `abc.txt`:
```bash
manzana roja
pera verde
plátano amarillo
3458452 8456325
zanahoria anaranjado
7542125 4785365
```
Ejecutamos:
```bash
cat abc.txt | sed -E 's/[0-9]+/''/g'
```
Resultado:
```bash
manzana roja
pera verde
plátano amarillo
 
zanahoria anaranjado

```
He utilizado el `-E` para poder añadir un `regex Extended` y así sustituir (`s/`) los números del `0 al 9` (Uno o más `+`) por un carácter vacío `''`. Con el `/g` le digo que abarque todo el archivo de texto `abc.txt`.

## - Comando: aws
**Escaneo y procesamiento de texto**
Voy a utilizar el mismo archivo `abc.txt` para así extraer la palabra o palabras basándome en filas y columnas.

Contenido del archivo `abc.txt`:
```bash
manzana roja
pera verde
plátano amarillo
3458452 8456325
zanahoria anaranjado
7542125 4785365
```
Ejecutamos:
```bash
cat abc.txt | awk 'FNR == 3 {print $1, $2}'
```
Resultado:
```bash
plátano amarillo
```
Con el `FNR` le digo que quiero dirigirme a la tercera `3` fila y deseo imprimir la columna `1` y `2`.
Nótese que luego de la `,` hay un espacio, es por eso que se respeta el espacio en blanco entre la palabra de la columna `1` y la de la columna `2`.

## Comando: perl
**Escanear y extraer información**

Algo sumamente útil que se puede realizar con el comando `perl` es extraer un octeto de una dirección `IPv4`.

Por ejemplo:
```bash
echo "192.168.1.100" | perl -pe 's/(\d+)\.(\d+)\.(\d+)\.(\d+)/$4/g'
```
Resultado:
```bash
100
```
Con el `p` le digo que haga un loop pero con un formato parecido al de `sed` y con el `e` simplemente es para que sea una línea de comando.

Una vez generado el patron en un formato `regex` le digo que extraiga el cuarto `4` basándose en ese mismo patrón.

