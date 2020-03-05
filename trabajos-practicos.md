# Trabajos prácticos

# TP 1 - Procesador de imágenes de Pixabay

## Condiciones y formato de entrega

Deberán formar sus grupos de 2 personas, clonarse [este repositorio](https://classroom.github.com/g/Qk8S9HgH) y trabajar allí. 

Se tomará como entrega el código que esté allí el día **Viernes 6 de Marzo a las 23:59 horas**, sin excepciones. Luego de la entrega habrá una defensa individual en clase para validar que todas las personas del grupo hayan aportado al trabajo.

## Criterios de evaluación y calificación

Para **aprobar**, deben cumplir _todos_ los siguientes requisitos:
* que el script cumpla su función (descargue imágenes relacionadas a la query, las transforme y arme los trípticos);
* las descargas deben realizarse en threads diferentes (uno por imagen, excepto que implementen el último bonus);
* las transformaciones deben estar implementadas en threads diferentes (al menos uno por transformación);
* la generación de trípticos debe realizarse en (al menos) un thread diferente;
* sincronizar los threads mediante semáforos y/o monitores;
* no usar `sleep` ni `join`. 

Para **poder promocionar**, deben además implementar correctamente la mayor cantidad de bonus. Ojo con esto: preferimos un programa que funciona y hace menos cosas a uno que pretende hacer un montón de cosas pero no funciona ninguna.

Además, tendremos en cuenta estos criterios de calidad para la construcción de la nota final:
* correcta división en subtareas, ya sea usando funciones o usando clases;
* código repetido;
* legibilidad del código (nombres de variables, funciones, etc.);
* prolijidad;
* puntualidad en la fecha de entrega.

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

Para hacer esto, obviamente deberán utilizar _threads_ y algún mecanismo de sincronización de los vistos hasta ahora: _locks_, semáforos y/o monitores. Las transformaciones pueden ser las que ustedes quieran, lo único que les pedimos es que sean al menos dos.

A muy alto nivel, el programa debería comportarse así:
1. realizar una request a Pixabay para obtener las URLs de las imágenes,
1. descargar cada una de las imágenes (**en threads separados**),
1. mientras se van descargando las imágenes, aplicar las transformaciones (**en un thread por cada transformación**),
1. a medida que haya imágenes transformadas, armar los trípticos (**en un thread aparte**).

Si por ejemplo se van a descargar 30 imágenes y aplicar 3 efectos a cada una, debería haber al menos 34 threads corriendo: los 30 que descargan las imágenes + los 3 para los efectos + el que genera los trípticos. Si lo consideran necesario, podría haber más threads, pero no vale hacerlo con menos.

## Consejos para la implementación

Largarse a hacer todo de una puede ser un poco abrumante, les recomendamos dividir el problema en varias etapas que ataquen de a una complejidad a la vez. En esta línea, podrían ir haciendo el programa de manera incremental siguiendo los puntos descriptos en el apartado anterior: una primera versión que solo baje las imágenes, una segunda que además las transforme, una tercera que además las compile.

También podría servirles hacer todo _sin threads_ y luego ir incorporándolos para cada funcionalidad. Para que no tengan que reescribir todo el código después, es muy importante que modularicen su código usando funciones y/o clases (recuerden que fuimos sus profes de Objetos 1 y sabemos de qué son capaces).

En cuanto a la sincronización, una forma posible de encararla es utilizando una lista (o cola) para cada paso del algoritmo. Lo que debería hacer cada etapa es:
* esperar a que haya elementos en su lista de trabajo,
* procesar el/los elementos,
* meter el resultado en la lista de trabajo de la siguiente etapa.

**Ojo :eye::** los efectos trabajan de a una imagen a la vez, pero la generación de trípticos necesita que haya al menos tres elementos para poder procesar. Tienen que contemplar esto en el mecanismo de sincronización que implementen.

## Bonus

### Parametrizaciones

Agregarle al script la capacidad de parametrizar:

1. la cantidad de threads que aplica cada transformación,
1. la cantidad de threads que arman los trípticos,
1. la cantidad de imágenes que tiene cada tríptico (que, lógicamente, dejaría de ser un tríptico para pasar a ser un N-íptico :stuck_out_tongue:).
1. más difícil: qué transformaciones se van a aplicar, eligiendo de una lista de transformaciones que ustedes hayan implementado. Por ejemplo, la entrada podría ser "rotacion,contraste,escala_grises" y ustedes deberían aplicar esos tres efectos,
1. más más difícil: la cantidad de threads que se encargan de bajar las imágenes. El máximo va a coincidir con la cantidad de imágenes que se van a descargar, pero podría elegirse un valor menor (por ejemplo: usar 5 threads para bajar 30 imágenes).

Esto pueden lograrlo de tres maneras:
* pasando los parámetros por consola y leyéndolos con [`sys.argv`](https://www.tutorialspoint.com/python/python_command_line_arguments.htm);
* usando [`input`](https://docs.python.org/3.5/library/functions.html#input) y pidiendo los parámetros una vez que se ejecuta el programa;
* mucho más sofisticado, usando [`argparse`](https://docs.python.org/3.3/library/argparse.html).

Elijan la que les de mayor satisfacción. :smiley:

### Optimización de performance

Una vez resueltos los puntos 1 y 2 del apartado anterior, ir variando la cantidad de threads y medir el tiempo que tarda en ejecutar con cada una de las combinaciones. Registrar estos datos en el repositorio - podría ser con una tabla en el `README.md` o algún `tiempos.txt` en la raíz (por favor no usen Excel ni Word ni nada de eso, que no se puede ver directamente desde GitHub).

Con las mediciones en mano, buscar la combinación de threads que parezca más óptima.

## Repositorios de ejemplo

* [Manipulación de imágenes](https://github.com/concu-unahur/python-manipulacion-imagenes): algunos ejemplos de transformaciones, incluida la concatenación que necesitan hacer para armar los trípticos. :wink: Presten especial atención a la forma en que leemos y escribimos las imágenes, deben hacerlo de esa manera para que no les salten errores extraños de formato.
* [Manipulación de listas](https://github.com/concu-unahur/python-listas): ejemplitos de cómo recorrer, filtrar, hacer `map` sobre listas. Vean también el link que está más abajo que tiene más ejemplos.

## Links útiles

* [Documentación de la API de Pixabay](https://pixabay.com/api/docs/#api_search_images)
* [Ejemplos de manipulaciones con scikit](https://scikit-image.org/docs/dev/auto_examples/)
* [Explicación de varios métodos de las listas](https://likegeeks.com/python-list-functions/)
* [Listas por comprensión (o _list comprehension_)](https://www.programiz.com/python-programming/list-comprehension)
