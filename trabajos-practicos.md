# Trabajos prácticos

# TP 1 - Procesador de imágenes de Pixabay

## Configuración del entorno

1. Desde una consola dentro del proyecto, ejecutar `pip3 install -r requirements.txt` para instalar las dependencias.
1. Crearse una cuenta en [Pixabay](https://pixabay.com/accounts/register).
1. Obtener el API key desde la [página de la documentación](https://pixabay.com/api/docs/#api_search_images).
1. Agregar la API key al código y ejecutarlo para verificar que funcione.

## Consignas

El objetivo del trabajo es construir un _script_ en Python que a partir de una _query_ realice las siguientes acciones:
* descargue imágenes de Pixabay relacionadas con los términos ingresados,
* aplique una serie de transformaciones (rotación, contraste, escala de colores, etc.),
* y finalmente genere trípticos con las imágenes ya modificadas.

En imágenes, sería algo así:

**Descargadas**

![](assets/tp/bolivia-1.jpg)
![](assets/tp/bolivia-2.jpg)
![](assets/tp/bolivia-3.jpg)

**Transformadas**

![](assets/tp/procesada-bolivia-1.jpg)
![](assets/tp/procesada-bolivia-2.jpg)
![](assets/tp/procesada-bolivia-3.jpg)

**Compilada**

![](assets/tp/triptico-bolivia.jpg)

Para hacer esto, obviamente deberán utilizar _threads_ y algún mecanismo de sincronización de los vistos hasta ahora: _locks_, semáforos y/o monitores.

A muy alto nivel, el programa debería comportarse así:
1. realizar una request a Pixabay para obtener las URLs de las imágenes,
1. descargar cada una de las imágenes (**en threads separados**),
1. mientras se van descargando las imágenes, aplicar las transformaciones (**en un thread por cada transformación**),
1. a medida que haya imágenes transformadas, armar los trípticos (**en un thread aparte**).

Si por ejemplo se van a descargar 30 imágenes y aplicar 3 efectos a cada una, debería haber al menos 34 threads corriendo: los 30 que descargan las imágenes + los 3 para los efectos + el que genera los trípticos. Si lo consideran necesario, podría haber más threads, pero no vale hacerlo con menos.

## Consejos para la implementación

Largarse a hacer todo de una puede ser un poco abrumante, les recomendamos dividir el problema en varias etapas que ataquen de a una complejidad a la vez. En esta línea, podrían ir haciendo el programa de manera incremental siguiendo los puntos descriptos en el apartado anterior: una primera versión que solo baje las imágenes, una segunda que además las transforme, una tercera que además las compile.

También podría servirles hacer todo _sin threads_ y luego ir incorporándolos para cada funcionalidad. Para que no tengan que reescribir todo el código después, es muy importante que modularicen su código usando funciones y/o clases (recuerden que fuimos sus profes de Objetos 1 y sabemos de qué son capaces).

## Bonus

Parametrizar:
* la cantidad de threads que aplica cada transformación,
* la cantidad de threads que arman los trípticos,
* la cantidad de imágenes que tiene cada tríptico (que, lógicamente, dejaría de ser un tríptico para pasar a ser un N-íptico :stuck_out_tongue:).

## Links útiles

* [Documentación de la API de Pixabay](https://pixabay.com/api/docs/#api_search_images)
* [Ejemplos de manipulaciones con scikit](https://scikit-image.org/docs/dev/auto_examples/)
