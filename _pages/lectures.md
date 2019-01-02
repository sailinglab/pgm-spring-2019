---
layout: schedule
permalink: /lectures/
title: Schedule
---

{% assign current_module = 0 %}
{% assign skip_classes = 0 %}
{% for item in site.data.lectures %}
{% if item.date %}
{% assign lecture = item %}
<tr>
    <th scope="row">{{ lecture.date }}</th>
    {% if lecture.title contains 'No class' or forloop.last %}
    {% assign skip_classes = skip_classes | plus: 1 %}
    <td colspan="3" align="center">{{ lecture.title }}</td>
    {% else %}
    <td>
        Lecture #{{ forloop.index | minus: current_module | minus: skip_classes }}
        {% if lecture.lecturer %}({{ lecture.lecturer }}){% endif %}:
        <br />
        {{ lecture.title }}
        <br />
        [
            {% if lecture.slides %}
              <a href="{{ lecture.slides }}" target="_blank">slides</a>
            {% else %}
              slides
            {% endif %}
            {% if lecture.video %}
            | <a href="{{ lecture.video }}" target="_blank">video</a>
            {% else %}
            | video
            {% endif %}
            {% if lecture.notes %}
            | <a href="{{ lecture.notes }}" target="_blank">notes</a>
            {% else %}
            | notes
            {% endif %}
        ]
    </td>
    <td>
        {% if lecture.readings %}
        <ul>
        {% for reading in lecture.readings %}
            <li>{{ reading }}</li>
        {% endfor %}
        </ul>
        {% endif %}
    </td>
    {% endif %}
</tr>
{% else %}
{% assign current_module = current_module | plus: 1 %}
{% assign module = item %}
<tr class="info">
    <td colspan="4" align="center">{{ module.title }}</td>
</tr>
{% endif %}
{% endfor %}
