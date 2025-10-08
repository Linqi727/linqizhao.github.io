---
title: "Projects"
layout: single
permalink: /projects/
author_profile: true
classes: wide
---

<div id="project-filter" class="filter-bar">
  <button class="filter-btn active" data-filter="all">All</button>
  <button class="filter-btn" data-filter="product">Product Design</button>
  <button class="filter-btn" data-filter="research">Design Research</button>
  <button class="filter-btn" data-filter="game">Game</button>
</div>

<div class="project-grid">
  {% assign sorted_projects = site.projects | sort: 'date' | reverse %}
  {% for project in sorted_projects %}
    <div class="project-card" data-category="{{ project.category }}">
      <a href="{{ project.url | relative_url }}">
        {% if project.header.teaser %}
          <img src="{{ project.header.teaser | relative_url }}" alt="{{ project.title }}">
        {% endif %}
        <h3>{{ project.title }}</h3>
        <p class="date">{{ project.date | date: "%b %Y" }}</p>
        <p class="excerpt">{{ project.excerpt | strip_html | truncate: 100 }}</p>
      </a>
    </div>
  {% endfor %}
</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const buttons = document.querySelectorAll(".filter-btn");
    const cards = document.querySelectorAll(".project-card");

    buttons.forEach(btn => {
      btn.addEventListener("click", () => {
        buttons.forEach(b => b.classList.remove("active"));
        btn.classList.add("active");

        const filter = btn.getAttribute("data-filter");
        cards.forEach(card => {
          const cat = card.getAttribute("data-category");
          if (filter === "all" || cat === filter) {
            card.style.display = "block";
          } else {
            card.style.display = "none";
          }
        });
      });
    });
  });
</script>

<style>
.filter-bar {
  display: flex;
  gap: 10px;
  margin-bottom: 1.5rem;
}
.filter-btn {
  padding: 6px 12px;
  border: 1px solid #ccc;
  background: #f7f7f7;
  cursor: pointer;
  border-radius: 20px;
  font-size: 0.9em;
}
.filter-btn.active {
  background: #333;
  color: white;
  border-color: #333;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 20px;
}
.project-card {
  border: 1px solid #eee;
  border-radius: 10px;
  padding: 10px;
  transition: box-shadow .2s ease;
  background: white;
}
.project-card:hover {
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
}
.project-card img {
  width: 100%;
  height: auto;
  border-radius: 6px;
  margin-bottom: 8px;
}
.project-card h3 {
  margin-top: 0;
  font-size: 1.1em;
}
.project-card .date {
  font-size: 0.85em;
  color: #888;
  margin-bottom: 0.5em;
}
.project-card .excerpt {
  font-size: 0.9em;
  color: #555;
}
</style>

