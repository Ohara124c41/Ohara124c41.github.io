---
layout: pages
title: Industrial Projects
permalink: /projects/industrial/
description: Case studies built with external partners. Filtered view of posts tagged as industrial.
---

<section class="industrial-projects" itemscope itemtype="https://schema.org/CollectionPage">
  <h2>Industrial Projects</h2>
  <p>Selected case studies delivered with external partners. Only posts marked with industrial: true are listed.</p>

  {% assign industrial_posts = site.posts | where_exp: "p", "p.industrial == true" | sort: "date" | reverse %}

  {% for post in industrial_posts %}
    {% assign partner_meta = nil %}
    {% if post.partner_key %}
      {% assign partner_meta = site.data.partners[post.partner_key] %}
    {% endif %}

    <article class="project-card" itemscope itemtype="https://schema.org/CreativeWork">
      <div class="project-logo">
        {% if partner_meta and partner_meta.logo %}
          <img src="{{ partner_meta.logo }}" alt="{{ partner_meta.name }} logo">
        {% endif %}
      </div>
      <div class="project-body">
        <h3 itemprop="name"><a itemprop="url" href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p class="project-meta">
          <span itemprop="datePublished">{{ post.date | date: "%Y-%m-%d" }}</span>
          {% if partner_meta and partner_meta.name %}
            | Partner: <a href="{{ partner_meta.url }}" rel="nofollow noopener" target="_blank">{{ partner_meta.name }}</a>
          {% endif %}
        </p>
        {% if post.excerpt %}
          <p>{{ post.excerpt | strip_html | truncate: 220 }}</p>
        {% else %}
          <p>{{ post.content | strip_html | truncate: 220 }}</p>
        {% endif %}
        <p><a href="{{ post.url | relative_url }}">Read the case study</a></p>
      </div>
    </article>
  {% endfor %}
</section>
