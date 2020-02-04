---
items:
  - nombre: Proceso
    descripcion: Es un programa en ejecución, tiene su propio estado independiente del estado de cualquier otro programa incluidos los del sistema operativo. Va acompañado de recursos como archivos, memoria, etc. 
  - nombre: Semáforo
    descripcion: (completar)
  - nombre: Monitor
    descripcion: (completar)
  - nombre: Deadlock
    descripcion: los procesos están esperando un evento que nunca ocurrirá.
  - nombre: Hilo o _thread_
    descripcion: (completar)
  - nombre: Sección crítica
    descripcion: (completar)
---

# Glosario

{% for item in page.items %}
* **{{item.nombre}}:** {{item.descripcion}}
{% endfor %}
