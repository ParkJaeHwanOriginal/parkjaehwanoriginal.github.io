# 박재환의 개발 기록

안녕하세요.

제가 만든 프로젝트와 공부한 내용을 기록하는 공간입니다.

## 프로젝트

개발 프로젝트와 개인 작업을 정리합니다.

- [프로젝트 포트폴리오](/projects/) — 주요 프로젝트와 기술적 성과
- [토이 프로젝트](/toy-projects/) — 소규모 개발 및 개인 도구
- [개인 프로젝트](/personal-projects/) — 장기 프로젝트와 개발 일지

## [블로그](/blog/)

최근 작성한 글입니다.

{% assign recent_posts = site.posts | slice: 0, 5 %}

{% if recent_posts.size > 0 %}
<ul class="recent-posts">
  {% for post in recent_posts %}
    <li>
      <a href="{{ post.url | relative_url }}">
        {{ post.title }}
      </a>
      <small>{{ post.date | date: "%Y-%m-%d" }}</small>
    </li>
  {% endfor %}
</ul>
{% else %}
<p>아직 작성된 글이 없습니다.</p>
{% endif %}

[전체 글 보기 →](/blog/)
