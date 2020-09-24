---
layout: page
title: 写真目録
permalink: /photo/
---


<h1>{{ page.title }}</h1>

<p>Below are all the albums that are currently hosted on this website. </p>

{% assign count = 0 %}
{% assign align = "left" %}
{% for gallery in site.data.galleries.overview %}
{% if count == 0 %}<div class="row">{% endif %}
  <div class="half-width gallery-preview {{ align }}">
    <h1>{{ gallery.title }}</h1>
    <a href="/ShadowArchive/{{ gallery.postDirectory }}">
      <img alt="{{ gallery.title }}" src="/assets/photography/{{ gallery.preview.filename}}" />
    </a>
  </div>
{% if count == 1 %}</div>{% endif %}
{% assign count = count | plus: 1 %}
{% assign align = "right" %}
{% if count >= 2 %}
{% assign align = "left" %}
{% assign count = 0 %}
{% endif %}
{% endfor %}

{% if count != 1 %}
</div>
{% endif %}