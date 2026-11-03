---
layout: default
title: Blog
permalink: /blog/
---

# Blog

개발하며 경험하고 공부한 내용을 기록합니다.

<div class="blog-list-header">
  <span class="blog-total">
    전체 게시글 <strong>{{ site.posts.size }}</strong>
  </span>
  <a class="blog-write-button"
     href="https://github.com/ParkJaeHwanOriginal/parkjaehwanoriginal.github.io/new/main/_posts">
    + 글쓰기
  </a>
</div>

<div id="blog-post-list">
  {% for post in site.posts %}
    <article class="blog-post-item">
      <h3>
        <a href="{{ post.url | relative_url }}">
          {{ post.title | escape }}
        </a>
      </h3>

      <p class="blog-post-meta">
        {{ post.date | date: "%Y-%m-%d" }}
        {% if post.categories.size > 0 %}
          · {{ post.categories | join: ", " }}
        {% endif %}
      </p>

      <p class="blog-post-excerpt">
        {{ post.excerpt | strip_html | normalize_whitespace | truncate: 140 }}
      </p>
    </article>
  {% endfor %}
</div>

<div id="blog-pagination" class="blog-pagination"></div>

<script>
document.addEventListener("DOMContentLoaded", function () {
  const posts = Array.from(
    document.querySelectorAll(".blog-post-item")
  );

  const pagination = document.getElementById("blog-pagination");
  const pageSize = 10;
  const totalPages = Math.ceil(posts.length / pageSize);

  if (totalPages <= 1) {
    pagination.style.display = "none";
  }

  let currentPage = Math.min(
    Math.max(parseInt(new URLSearchParams(location.search).get("page")) || 1, 1),
    Math.max(totalPages, 1)
  );

  function renderPage(page) {
    currentPage = page;

    posts.forEach((post, index) => {
      const start = (page - 1) * pageSize;
      post.style.display =
        index >= start && index < start + pageSize ? "" : "none";
    });

    pagination.innerHTML = "";

    function addButton(label, targetPage, active, disabled) {
      const button = document.createElement("button");
      button.textContent = label;
      button.className = "page-button";
      if (active) button.classList.add("active");
      button.disabled = disabled;

      button.addEventListener("click", () => {
        renderPage(targetPage);
        history.replaceState(null, "", "?page=" + targetPage);
        window.scrollTo({ top: 0, behavior: "smooth" });
      });

      pagination.appendChild(button);
    }

    addButton("‹", page - 1, false, page === 1);

    for (let i = 1; i <= totalPages; i++) {
      addButton(i, i, i === page, false);
    }

    addButton("›", page + 1, false, page === totalPages);
  }

  if (posts.length > 0) {
    renderPage(currentPage);
  }
});
</script>
