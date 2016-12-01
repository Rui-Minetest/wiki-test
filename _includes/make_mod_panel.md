{% assign id = include.name | remove: " " | downcase | url_encode %}

<div class="panel-group">
  <div class="panel panel-default">
    {% if include.screenshot %}
    <div align="center" class="panel-body">
      <a href="{{ include.screenshot }}" rel="lightbox">
        <img src="{{ include.screenshot }}" border="0" style="max-height: 150px">
      </a>
    </div>
    {% endif %}

    <ul class="list-group">
      <li class="list-group-item" align="center">
        {% for link_data in include.links %}
        {% if forloop.first != true %}/{% endif %}
        <a href="{{ link_data.url }}" target="_blank">
          {{ link_data.text }}
        </a>
        {% endfor %}
      </li>
      <li class="list-group-item">{{ include.description }}</li>
      <li class="list-group-item">
        {% if include.develop_text %}
        {{ include.develop_text }}
        {% else %}
        開発:
        {% endif %}
        {{ include.developer }}
      </li>

      {% if include.depends %}
      <a data-toggle="collapse" href="#{{ id }}-required">
        <li class="list-group-item">依存Mod<span class="badge">{{ include.depends | size }}</span></li>
      </a>
      <div id="{{ id }}-required" class="panel-collapse collapse">
        <li class="list-group-item" style="background-color: rgb(245, 245, 245)">
          {% for depend in include.depends %}
          {% if depend.url %}
          <a href="{{ depend.url }}" target="_blank">"{{ depend.text }}"</a>
          {% else %}
          "{{ depend.text }}"
          {% endif %}
          {% endfor %}
        </li>
      </div>
      {% endif %}

      {% if include.depends_optional %}
      <a data-toggle="collapse" href="#{{ id }}-optional">
        <li class="list-group-item">依存Mod(任意)<span class="badge">{{ include.depends_optional | size }}</span></li>
      </a>
      <div id="{{ id }}-optional" class="panel-collapse collapse">
        <li class="list-group-item" style="background-color: rgb(245, 245, 245)">
          {% for depend in include.depends_optional %}
          {% if depend.url %}
          <a href="{{ depend.url }}" target="_blank">"{{ depend.text }}"</a>
          {% else %}
          "{{ depend.text }}"
          {% endif %}
          {% endfor %}
        </li>
      </div>
      {% endif %}
    </ul>
  </div>
</div>