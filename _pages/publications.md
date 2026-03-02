---
title: "Publications | SynThera Group"
layout: gridlay
excerpt: "Publications | SynThera Group"
sitemap: false
permalink: /publications/
---
> **For a full list go to [Google Scholar](https://scholar.google.com/citations?user=pG_kpHUAAAAJ&hl=zh-CN&oi=ao).**


{% assign pubs = site.data.publist.references %}

{% assign all_groups = pubs | group_by_exp: 'p', 'p.issued.first.year | default: 0' | sort: 'name' | reverse %}

{% assign latest_year = null %}
{% for g in all_groups %}
  {% assign y = g.name | plus: 0 %}
  {% if y >= 2020 %}
    {% assign latest_year = y %}
    {% break %}
  {% endif %}
{% endfor %}

<div class="panel-group" id="pub-accordion" role="tablist" aria-multiselectable="true" markdown="0">
  {% for g in all_groups %}
    {% assign y = g.name | plus: 0 %}
    {% if y >= 2020 %}
      {% if y == latest_year %}
        {% assign is_open = 'true' %}
      {% else %}
        {% assign is_open = 'false' %}
      {% endif %}

      <div class="panel panel-default">
        <div class="panel-heading" role="tab" id="heading-{{ y }}">
          <h4 class="panel-title">
            <a
              role="button"
              data-toggle="collapse"
              href="#collapse-{{ y }}"
              aria-expanded="{{ is_open }}"
              aria-controls="collapse-{{ y }}"
            >
              {{ y }}
            </a>
          </h4>
        </div>

        <div
          id="collapse-{{ y }}"
          class="panel-collapse collapse {% if is_open == 'true' %}in{% endif %}"
          role="tabpanel"
          aria-labelledby="heading-{{ y }}"
        >
          <div class="panel-body">
            {% for publi in g.items %}
              {% assign names = '' | split: '' %}
              {% if publi.author %}
                {% for a in publi.author %}
                  {% assign fam = a.family | to_s %}
                  {% assign giv = a.given | to_s %}
                  {% assign initial = '' %}
                  {% if giv != '' %}
                    {% assign first_char = giv | strip | slice: 0, 1 | upcase %}
                    {% assign initial = first_char | append: '.' %}
                  {% endif %}
                  {% assign formatted = fam %}
                  {% if initial != '' %}
                    {% assign formatted = formatted | append: ', ' | append: initial %}
                  {% endif %}
                  {% if formatted != '' %}
                    {% assign names = names | push: formatted %}
                  {% endif %}
                {% endfor %}
              {% endif %}

              {% assign journal = publi['container-title'] | default: publi['container-title-short'] %}
              {% assign year = publi.issued.first.year | default: '' %}

              {% assign vol_str = publi.volume | to_s | strip %}
              {% assign issue_str = publi.issue | to_s | strip %}
              {% assign page_str = publi.page | to_s | strip %}

              {% assign vol_issue = null %}
              {% if vol_str != '' and issue_str != '' %}
                {% assign vol_issue = vol_str | append: '(' | append: issue_str | append: ')' %}
              {% elsif vol_str != '' %}
                {% assign vol_issue = vol_str %}
              {% elsif issue_str != '' %}
                {% assign vol_issue = '(' | append: issue_str | append: ')' %}
              {% endif %}

              {% assign parts = '' | split: '' %}
              {% if journal %}{% assign parts = parts | push: journal %}{% endif %}
              {% if year %}{% assign parts = parts | push: year %}{% endif %}
              {% if vol_issue %}{% assign parts = parts | push: vol_issue %}{% endif %}
              {% if page_str != '' %}{% assign parts = parts | push: page_str %}{% endif %}

              {% assign link_href = null %}
              {% if publi.URL %}
                {% assign link_href = publi.URL %}
              {% elsif publi.DOI %}
                {% assign link_href = 'https://doi.org/' | append: publi.DOI %}
              {% endif %}

              <p class="pub-item">
                {% if link_href %}
                  <strong
                    ><a class="title-link" href="{{ link_href }}" target="_blank" rel="noopener">
                      {{- publi.title | markdownify | strip_newlines
                 | replace: '<p>', '' | replace: '</p>', '' -}}
                    </a></strong
                  ><br>
                {% else %}
                  <strong>{{ publi.title | markdownify | strip_newlines
                 | replace: '<p>', '' | replace: '</p>', '' }}</strong><br>
                {% endif %}
                {% if names.size > 0 %}
                  {{ names | join: ', ' -}}
                  <br>
                {% endif %}
                {{ parts | join: ', ' }}.
              </p>
            {% endfor %}
          </div>
        </div>
      </div>
    {% endif %}
  {% endfor %}

  <div class="panel panel-default">
    <div class="panel-heading" role="tab" id="heading-prior">
      <h4 class="panel-title">
        <a
          role="button"
          data-toggle="collapse"
          href="#collapse-prior"
          aria-expanded="false"
          aria-controls="collapse-prior"
        >
          Prior Publications
        </a>
      </h4>
    </div>

    <div id="collapse-prior" class="panel-collapse collapse" role="tabpanel" aria-labelledby="heading-prior">
      <div class="panel-body">
        {% for g in all_groups %}
          {% assign y = g.name | plus: 0 %}
          {% if y < 2020 %}
            {% for publi in g.items %}
              {% assign names = '' | split: '' %}
              {% if publi.author %}
                {% for a in publi.author %}
                  {% assign fam = a.family | to_s %}
                  {% assign giv = a.given | to_s %}
                  {% assign initial = '' %}
                  {% if giv != '' %}
                    {% assign first_char = giv | strip | slice: 0, 1 | upcase %}
                    {% assign initial = first_char | append: '.' %}
                  {% endif %}
                  {% assign formatted = fam %}
                  {% if initial != '' %}
                    {% assign formatted = formatted | append: ', ' | append: initial %}
                  {% endif %}
                  {% if formatted != '' %}
                    {% assign names = names | push: formatted %}
                  {% endif %}
                {% endfor %}
              {% endif %}
              {% assign journal = publi['container-title'] | default: publi['container-title-short'] %}
              {% assign year = publi.issued.first.year | default: '' %}
              {% assign vol_str = publi.volume | to_s | strip %}
              {% assign issue_str = publi.issue | to_s | strip %}
              {% assign page_str = publi.page | to_s | strip %}
              {% assign vol_issue = null %}
              {% if vol_str != '' and issue_str != '' %}
                {% assign vol_issue = vol_str | append: '(' | append: issue_str | append: ')' %}
              {% elsif vol_str != '' %}
                {% assign vol_issue = vol_str %}
              {% elsif issue_str != '' %}
                {% assign vol_issue = '(' | append: issue_str | append: ')' %}
              {% endif %}
              {% assign parts = '' | split: '' %}
              {% if journal -%}
                {%- assign parts = parts | push: journal -%}
              {%- endif %}
              {% if year %}{% assign parts = parts | push: year %}{% endif %}
              {% if vol_issue -%}
                {%- assign parts = parts | push: vol_issue -%}
              {%- endif %}
              {% if page_str != '' %}{% assign parts = parts | push: page_str %}{% endif %}
              {% assign link_href = null %}
              {% if publi.URL %}
                {% assign link_href = publi.URL %}
              {% elsif publi.DOI %}
                {% assign link_href = 'https://doi.org/' | append: publi.DOI %}
              {% endif %}
              <p class="pub-item">
                {% if link_href %}
                  <strong>
                    <a class="title-link" href="{{ link_href }}" target="_blank" rel="noopener">
                      {{- publi.title | markdownify | strip_newlines
                 | replace: '<p>', '' | replace: '</p>', '' -}}
                    </a></strong>
                  <br>
                {% else %}
                  <strong>{{ publi.title | markdownify | strip_newlines
                 | replace: '<p>', '' | replace: '</p>', '' }}</strong><br>
                {% endif %}
                {% if names.size > 0 %}
                  {{ names | join: ', ' -}}
                  <br>
                {% endif %}
                {{ parts | join: ', ' }}.
              </p>
            {% endfor %}
          {% endif %}
        {% endfor %}
      </div>
    </div>
  </div>
</div>

<style>
  #pub-accordion .pub-item {
    margin-bottom: 0.85em;
  }

  #pub-accordion .pub-item a.title-link {
    color: inherit;
    text-decoration: none;
  }

  #pub-accordion .pub-item a.title-link:hover,
  #pub-accordion .pub-item a.title-link:focus {
    color: inherit;
    text-decoration: none;
  }
</style>
