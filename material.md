---
guias:
  - name: objetos
  - name: objetos
  - name: objetos
  - name: colecciones
  - name: clases
  - name: herencia
  - name: herencia
  - name: adicionales-1er-parcial
  - name: integradores
  - name: extras
---

# Material

## Git

En esta materia utilizamos [Git](https://git-scm.com/) como herramienta para el control de versiones del código que vas a ir produciendo. El manejo que necesitás es básico, y está explicado en la guía rápida que te ofrecemos más abajo. El resto de los recursos pueden serte útiles si querés profundizar en el conocimiento de la herramienta.

* [Guía rápida de cómo usar Git](https://github.com/obj1-unahur-2018s2/docs/wiki/Guia-r%C3%A1pida-de-GIT). Lo mínimo que tenés que saber para poder trabajar.
* [Otro apunte sobre Git](https://docs.google.com/document/d/1ozqfYCwt-37stynmgAd5wJlNOFKWYQeIZoeqXpAEs0I/edit). Un poco más extenso que el anterior, explica con más detalle algunos comandos.
* [Tutorial interactivo de Git](https://github.com/jlord/git-it-electron). Mucho más completo que los anteriores (y que lo que necesitamos para la materia). Funciona offline, hay que instalarlo e incluye una primera parte que explica cómo bajarse Git. Por defecto viene en inglés pero se puede poner en español.

## Wollok

En principio recomendamos los apuntes [publicados en el sitio de Wollok](http://www.wollok.org/documentacion/apuntes/) y las explicaciones que hay en nuestra instancia de Mumuki. Además, tenemos estos recursos:

* [Machete de sintaxis Wollok](https://docs.google.com/document/d/11BEzE5o-0wRyvidwV-NV6JTQbf0s00ZLYNkjn_G8fio/edit?usp=sharing). Resumen de la sintaxis de Wollok.
* [Guía sobre colecciones y closures](https://objetos1wollokunq.gitlab.io/material/guia-colecciones-basicas.pdf). _El_ recurso para tener a mano cuando empecemos a trabajar con colecciones. Sobre todo las últimas páginas que sirven de machete para recordar qué operaciones existen.

## Guías de ejercicios adicionales

Ejercicios en formato "tradicional", que (aún) no tienen un proyecto en GitHub listo para clonar y empezar a trabajar.

{% for guia in page.guias %}
* [Guía {{forloop.index}} - {{guia.name}}](../guias/guia{{forloop.index}}-{{guia.name}}.pdf)
{% endfor %}
