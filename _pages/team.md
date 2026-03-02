---
title: "Team | SynThera Group"
layout: gridlay
excerpt: "Team | SynThera Group"
sitemap: false
permalink: /team/
---

<h3><strong>Group Members</strong></h3>

<h4><strong>Current Members</strong></h4>

<style>
  .row {
    margin-bottom: 0px !important; /* Increased specificity with class and !important */
  }
</style>

{% assign number_printed = 0 %}
{% for member in site.data.current_members %}

{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}

<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" class="img-responsive" width="25%" style="float: left" />
  <h5><strong>{{ member.name }}</strong></h5>
  <i><strong>{{ member.current_position }}</strong></i>
  <ul>
    {% for item in member.education %}
      <li>{{ item }}</li>
    {% endfor %}
  </ul>
  <i>Email: {{ member.email }}</i><br>
  <p align = 'justify'>{{ member.bio }}</p>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}

</div>
{% endif %}

{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}

</div>
{% endif %}


<h4><strong>Alumni</strong></h4>

<!-- alumni grad -->
<h5><strong>Graduate Students</strong></h5>

{% assign number_printed = 0 %}
{% for member in site.data.alumni_grad %}

{% assign mod_three = number_printed | modulo: 3 %}

{% if mod_three == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-4 clearfix">
  <h5>{{ member.name }}</h5>
  <i>years: {{ member.years }}</i><br>
  <!-- <i>current position: {{ member.current_position }}</i> -->
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if mod_three == 2 %}
</div>
{% endif %}

{% endfor %}

{% assign mod_three = number_printed | modulo: 3 %}
{% if mod_three != 0 %}
</div>
{% endif %}

<!-- alumni postdocs -->
<!-- 
<h5><strong>Postdocs</strong></h5>
{% assign number_printed = 0 %}
{% for member in site.data.alumni_postdoc %}

{% assign mod_three = number_printed | modulo: 3 %}

{% if mod_three == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-4 clearfix">
  <h5>{{ member.name }}</h5>
  <i>years: {{ member.years }}</i><br>
  <i>current position: {{ member.current_position }}</i>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if mod_three == 2 %}
</div>
{% endif %}

{% endfor %}

{% assign mod_three = number_printed | modulo: 3 %}
{% if mod_three != 0 %}
</div>
{% endif %} -->

<!-- alumni visitors/assistants -->
<!-- 
<h5><strong>Visitors/Assistants</strong></h5>
{% assign number_printed = 0 %}
{% for member in site.data.alumni_msc %}

{% assign mod_three = number_printed | modulo: 3 %}

{% if mod_three == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-4 clearfix">
  <h5>{{ member.name }}</h5>
  <i>years: {{ member.years }}</i><br>
  <i>current position: {{ member.current_position }}</i>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if mod_three == 2 %}
</div>
{% endif %}

{% endfor %}

{% assign mod_three = number_printed | modulo: 3 %}
{% if mod_three != 0 %}
</div>
{% endif %} -->

