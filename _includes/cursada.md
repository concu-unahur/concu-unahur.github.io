{% assign semanas = cursada | sort %}
{% for semana_hash in semanas reversed %}
{% assign numero_semana = semana_hash[0] | plus:0 %}
{% assign semana = semana_hash[1] %}

## [Semana {{numero_semana}}](#semana-{{numero_semana}}){: .titulo-semana}
{{semana.descripcion}}

{% if semana.entrega %}

### Para entregar
{% assign fecha = semana.entrega.fecha %}
La fecha límite para la entrega de esta semana es el <strong>{% include fecha-formato-humano.md fecha=fecha %}</strong>.

{% assign ejercicios = semana.entrega.ejercicios %}
{% if ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}
{% endif %}

{% assign guias = semana.entrega.mumuki %}
{% if guias %}
**Mumuki**
{% include ejercicios-mumuki.md guias=guias %}
{% endif %}

{{semana.entrega.descripcion}}

{% endif %}

{% if semana.ejercicios %}

### Ejercicios para trabajar en clase
{% assign ejercicios = semana.ejercicios %}
{% include ejercicios-github.html ejercicios=ejercicios %}

{% if semana.textoEjercicios %}
{{semana.textoEjercicios}}
{% endif %}

{% endif %}

{% if semana.mumuki %}

### Mumuki

Te recomendamos resolver las guías:
{% assign guias = semana.mumuki %}
{% include ejercicios-mumuki.md guias=guias %}

{% endif %}

{% if forloop.last == false %}
<hr class="titulo-semana">
{% endif %}

{% endfor %}
