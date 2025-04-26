---
layout: page
title: work
permalink: /work/
description: Some highlights related to my work
nav: true
nav_order: 2
display_categories: [work, fun]
horizontal: false
---
### Company Badges
---
{% if site.data.companies.companies %}

<div class="companies" style="display:grid; grid-template-columns: auto auto auto auto auto;">
  {% for company in site.data.companies.companies %}
    {% include companies/companies.html company=company%}
  {% endfor %}
</div>
{% endif %}

<br>


### Repositories
---
{% if site.data.repositories.github_repos %}

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}

<br>

<!-- ### Live Projects -->
<!-- pages/projects.md -->
<div class="projects">
<br>
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}

<!-- Display projects without categories -->

{%- assign sorted_projects = site.projects | sort: "importance" -%}

  <!-- Generate cards for each project -->

{% if page.horizontal -%}

  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>


### Certifications
---
{% if site.data.certifications.certifications %}

<div class="repositories">
  {% for certificate in site.data.certifications.certifications %}
    {% include certifications/certificate.html certificate=certificate%}
  {% endfor %}
</div>
{% endif %}

<br>

### OSS Contributions
---

{% if site.data.contributions.contributions %}

<div class="repositories">
  {% for contribution in site.data.contributions.contributions %}
    {% include contributions/contribution.html contribution=contribution%}
  {% endfor %}
</div>
{% endif %}
<a style="color:#2F80ED;  text-decoration: underline; padding-left:8px; padding-top:20px;" href="https://github.com/bijaykumarpun">Click for more</a>

---