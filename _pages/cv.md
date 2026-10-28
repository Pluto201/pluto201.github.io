---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

{% include cv-download.html %}

A short web version of my CV is below. The PDF version, when available, is the authoritative document.

## Education

* **Master's degree in Computer Science and Technology**, Wuhan University of Science and Technology, China, 2021–2024
  * Research: evolutionary computation, constrained multi-objective optimization
  * First-Class Academic Scholarship (2021–2022)
* **Bachelor's degree in Mechanical Engineering**, Wuhan University of Science and Technology, China, 2017–2021

## Work experience

* **R&D Engineer**, state-owned enterprise, Beijing, July 2024 – present
  * Lakehouse migration: Flink, Apache Paimon, StarRocks, DolphinScheduler ([details]({{ base_path }}/projects/lakehouse-migration/))
  * Light-ChatBI semantic-layer data agent ([details]({{ base_path }}/projects/light-chatbi-data-agent/))
  * Data quality, data lineage, reporting automation

## Publications

<ul>{% for post in site.publications reversed %}
  {% include archive-single-cv.html %}
{% endfor %}</ul>

## Skills

* Python, SQL, Java, MATLAB
* Flink, Paimon, StarRocks, DolphinScheduler, Hadoop, Hive
* Evolutionary multi-objective optimization, constraint handling
* Data agents, text-to-SQL, semantic layers
