---
layout: default
title: アーカイブ
permalink: /archive/
---

<div class="column-inner">
  <div class="column-inner-2">
    <h2>アーカイブ</h2>

    <div class="category-nav">
      {% for category in site.category_names %}
        <a href="/categories/{{ category[0] }}" class="tag">{{ category[1] }}</a>
      {% endfor %}
    </div>

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
            <div class="archive-post">
              <div class="archive-post-inner">
                <div class="post-meta">
                  <span class="post-date">{{ post.date | date: "%-d日" }}</span>
                </div>
                <div class="post-content">
                  <h4 class="post-title">
                    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
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
                    {{ post.kit_name }}
                    {% if post.rating %}
                    <span class="rating">評価: {{ post.rating }}/5</span>
                    {% endif %}
                  </div>
                  {% endif %}
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

<style>
.archive-year {
  margin-bottom: 40px;
}

.archive-year h2 {
  color: var(--text-dark);
  border-bottom: 2px solid var(--main-color);
  padding-bottom: 10px;
  margin: 30px 0 20px;
}

.archive-month {
  margin: 20px 0;
}

.archive-month h3 {
  color: var(--text-dark);
  margin: 0 0 15px;
  font-size: 1.2em;
}

.archive-posts {
  border-left: 3px solid var(--main-color);
  margin-left: 10px;
}

.archive-post {
  margin: 0 0 15px 0;
}

.archive-post-inner {
  display: flex;
  gap: 15px;
  padding: 10px;
  background: white;
  border-radius: 4px;
  margin-left: -3px;
  border-left: 3px solid transparent;
  transition: all 0.3s ease;
}

.archive-post-inner:hover {
  border-left-color: var(--main-color);
  transform: translateX(5px);
}

.post-date {
  color: #666;
  font-size: 0.9em;
  white-space: nowrap;
}

.post-content {
  flex: 1;
}

.post-title {
  margin: 0;
  font-size: 1em;
  font-weight: normal;
}

.post-title a {
  color: var(--text-dark);
  text-decoration: none;
}

.post-title a:hover {
  color: var(--main-color);
}

.kit-info {
  font-size: 0.9em;
  color: #666;
  margin-top: 5px;
}

.post-categories {
  margin-top: 5px;
}

.post-categories .tag {
  font-size: 0.8em;
  padding: 2px 8px;
}
</style>