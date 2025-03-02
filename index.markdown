---
layout: default
---

<div class="column-inner">
  <div class="column-inner-2">
    <div class="navigation">
      <h2>記事を探す</h2>
      <div class="category-nav">
        {% for category in site.category_names %}
          <a href="/categories/{{ category[0] }}" class="tag">{{ category[1] }}</a>
        {% endfor %}
      </div>
    </div>

    <h2>新着記事</h2>
    <div class="post-list">
      {% for post in site.posts limit:6 %}
      <div class="post-card">
        {% if post.layout == 'review' %}
          <h3>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h3>
          <div class="post-meta">
            <time datetime="{{ post.date | date_to_xmlschema }}">
              {{ post.date | date: "%Y年%m月%d日" }}
            </time>
            {% if post.rating %}
            <span class="rating">評価: {{ post.rating }}/5</span>
            {% endif %}
          </div>
          {% if post.kit_name %}
          <div class="kit-info">
            <p>{{ post.kit_name }}</p>
            {% if post.maker %}<p class="maker">{{ post.maker }}</p>{% endif %}
          </div>
          {% endif %}
          {% if post.categories %}
          <div class="post-categories">
            {% for cat in post.categories %}
              <span class="tag">{{ site.category_names[cat] }}</span>
            {% endfor %}
          </div>
          {% endif %}
        {% else %}
          <h3>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h3>
          <div class="post-meta">
            <time datetime="{{ post.date | date_to_xmlschema }}">
              {{ post.date | date: "%Y年%m月%d日" }}
            </time>
          </div>
        {% endif %}
      </div>
      {% endfor %}
    </div>

    {% if site.posts.size > 6 %}
    <div class="more-posts">
      <a href="/archive" class="button">もっと見る →</a>
    </div>
    {% endif %}
  </div>
</div>
