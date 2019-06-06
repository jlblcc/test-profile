---
title: Sample Custom Profile Definitions
layout: default
---

# {{ page.title }}
{: .text-success}

{% assign files = site.static_files | where: "extname", ".json" | group_by_exp: "item",
"item.path | remove_first: '/' | split: '/' | first" %}
<!-- {{ files | jsonify }} -->
<!-- {% for folder in files %}
  - {{ folder.name }}
  {% for file in folder.items %}
    - [{{ file.name }}]({{ file.path }}): {{ site.url }}{{ file.path }}
  {% endfor %}

{% endfor %} -->

{% for folder in files %}
<div class="card mb-3">
  <h4 class="card-header">{{ folder.name }}</h4>
  <ul class="list-group list-group-flush">
  {% for file in folder.items %}
    <li class="list-group-item">
    <h5 class="list-group-item-header">{{site.data[file.basename].title}}</h5>
    <div><a href="{{ file.path | relative_url }}">{{ site.url }}{{ file.path | relative_url }}</a></div>
    <div>{{site.data[file.basename].description}}</div>
    <div>Version: <span class="text-success">{{site.data[file.basename].version}}</span></div>
    </li>
  {% endfor %}
  </ul>
</div>
{% endfor %}
