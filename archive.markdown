---
layout: default
title: 記事アーカイブ
description: プラモデル・フィギュアに関する全記事のアーカイブ。レビューや製作例、テクニック解説など、カテゴリー別・年月別で記事を探せます。
permalink: /archive/
---

<div class="archive-content">
  <div class="column-inner">
    <div class="column-inner-2">
      <h1>記事アーカイブ</h1>

      <div class="category-nav">
        {% for category in site.category_names %}
          <a href="/categories/{{ category[0] }}" class="tag">{{ category[1] }}</a>
        {% endfor %}
      </div>

      <div itemscope itemtype="http://schema.org/Blog">
        {% assign postsByYear = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}
        {% for year in postsByYear %}
          <div class="archive-year" id="{{ year.name }}">
            <h2>{{ year.name }}年</h2>
            {% assign postsByMonth = year.items | group_by_exp:"post", "post.date | date: '%m'" %}
            
            {% for month in postsByMonth %}
            <div class="archive-month" id="{{ year.name }}-{{ month.name }}">
              <h3>{{ month.name }}月</h3>
              <div class="archive-posts">
                {% for post in month.items %}
                <div class="archive-post" itemprop="blogPost" itemscope itemtype="http://schema.org/BlogPosting">
                  <div class="archive-post-inner">
                    <div class="post-meta">
                      <span class="post-date">
                        <time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">
                          {{ post.date | date: "%-d日" }}
                        </time>
                      </span>
                    </div>
                    <div class="post-content">
                      <h4 class="post-title">
                        <a href="{{ post.url | relative_url }}" itemprop="url headline">{{ post.title }}</a>
                      </h4>
                      {% if post.categories %}
                      <div class="post-categories">
                        {% for cat in post.categories %}
                          <span class="tag">{{ site.category_names[cat] }}</span>
                        {% endfor %}
                      </div>
                      {% endif %}
                      {% if post.kit_name %}
                      <div class="kit-info">
                        <span itemprop="about" itemscope itemtype="http://schema.org/Product">
                          <span itemprop="name">{{ post.kit_name }}</span>
                        </span>
                        {% if post.rating %}
                        <span class="rating">評価: {{ post.rating }}/5</span>
                        {% endif %}
                      </div>
                      {% endif %}
                      <meta itemprop="author" content="{{ post.author | default: site.author.name }}">
                      <meta itemprop="description" content="{{ post.content | strip_html | truncate: 160 }}">
                    </div>
                  </div>
                </div>
                {% endfor %}
              </div>
            </div>
            {% endfor %}
          </div>
        {% endfor %}
      </div>
    </div>
  </div>
</div>